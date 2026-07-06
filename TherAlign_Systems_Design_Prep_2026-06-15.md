# TherAlign Health — Systems Design Interview Prep
**Round:** Technical — Systems Design & Architecture
**When:** Monday June 15, 2026, 11:00 AM ET
**Interviewer:** Eric Swidler — CTO / tech lead (Staff Software Engineer @ Panorama Education)
**Format:** One open-ended design question (Vishnu got *"design chess.com"* — deliberately vague, you drive the structure)

> **The #1 thing to internalize:** an open-ended question is a test of *how you think and communicate*, not whether you reach one "right" answer. Eric wants to see you take a vague prompt, impose structure, ask sharp questions, reason about tradeoffs out loud, and know what's in vs out of scope. A messy "correct" answer loses to a clear, well-reasoned one. **You drive the conversation.**

---

## 1. The framework — run *every* design question through these 7 steps

Memorize this order. It works for chess.com, a URL shortener, or TherAlign's own product. Spend the first ~5 min on steps 1–2 before drawing anything.

**Step 1 — Clarify requirements & scope (ask, don't assume).**
Pin down *functional* requirements (what it does) and *non-functional* ones (how well: latency, scale, availability, consistency, security). Then explicitly agree what's **out of scope** so you don't drown. Say: *"Let me make sure I'm solving the right problem — can I ask a few questions first?"*

**Step 2 — Back-of-the-envelope estimates (only if useful).**
Rough numbers: how many users, requests/sec (QPS), reads vs writes, data size. This justifies later choices (e.g., "~10k concurrent games → we need horizontal scaling + a cache"). Don't overdo math; a couple of figures is enough.

**Step 3 — Define the API / core operations.**
List the handful of key endpoints or operations (e.g., `createGame`, `makeMove`, `getAlternatives(patient, drug)`). This forces clarity on inputs/outputs and the contract between client and backend.

**Step 4 — Data model.**
Key entities, their relationships, and **SQL vs NoSQL** with a one-line reason. Mention what's the source of truth.

**Step 5 — High-level architecture (draw boxes & arrows).**
Clients → load balancer → services → datastores/cache/queue. Keep it simple first; you'll deepen specific parts next. Narrate as you draw.

**Step 6 — Deep dive (where you earn the offer).**
Pick the 1–2 most interesting/risky components and go deep — or, better, ask *"Which part would you like me to drill into?"* Eric will steer; follow his lead (coachability matters here too).

**Step 7 — Scale, failure modes, tradeoffs, wrap-up.**
Bottlenecks, caching, sharding/replication, what happens when component X dies, consistency tradeoffs, monitoring. Close with a 30-second summary and *"with more time I'd also look at…"*

**Throughout:** think out loud, state assumptions ("I'll assume read-heavy, correct me if not"), and constantly name tradeoffs ("A or B; I'd pick A because…").

---

## 2. Building-blocks cheat sheet (your vocabulary)

Have these ready so you can reach for the right tool and justify it:

- **Load balancer** — spreads traffic across many stateless app servers; enables horizontal scaling. Sticky sessions when a client must keep hitting the same instance (e.g., a WebSocket).
- **Horizontal vs vertical scaling** — add more machines (preferred, resilient) vs a bigger machine (simple, limited). Keep services **stateless** so you can scale horizontally.
- **Caching** — Redis/Memcached or CDN. Use for read-heavy, slow, or repeated lookups. Know **cache-aside**, TTLs, and the hard part: **invalidation**. (For TherAlign: drug/formulary/literature data caches well; live patient data does not.)
- **SQL vs NoSQL** — SQL (Postgres/MySQL): relational, ACID, joins, strong consistency — default for structured data + transactions. NoSQL (Mongo/Dynamo/Cassandra): flexible schema, easy horizontal scale, great for huge volume / simple access patterns / key-value. Pick per access pattern and say why.
- **Replication** — read replicas to scale reads + survive failures (usually eventually consistent on replicas).
- **Sharding / partitioning** — split data across nodes by a key (e.g., `gameId`, `userId`) to scale writes/storage. Watch for **hot partitions**.
- **Message queue / event streaming** (Kafka, Pub/Sub, SQS) — decouple producers/consumers, absorb spikes, run work async (e.g., update ratings, send notifications, run a slow model). Enables **event sourcing**.
- **WebSockets vs polling vs SSE** — WebSocket = persistent two-way, low latency (real-time games/chat). Polling = simple but wasteful. SSE = server→client stream only.
- **Consistency** — **strong** (everyone sees the latest write; needed for money, game state) vs **eventual** (fast, scalable; fine for feeds, counts). Nod to **CAP**: under a network partition you trade consistency for availability.
- **Reliability patterns** — timeouts, retries with backoff, **idempotency** keys, circuit breakers, graceful degradation (fail soft, not hard).
- **Observability** — logs, metrics, traces, alerts. (Eric values documentation/operability — mention it.)
- **Security** — OAuth2/OIDC auth, encryption in transit + at rest, secrets in a vault/Secret Manager, least privilege. For TherAlign add **PHI / HIPAA**, audit logging.

---

## 3. ⭐ Worked example A — "Design chess.com" (most likely; it's what they asked Vishnu)

A real-time, stateful, multiplayer system — rich because it forces low latency, consistency, and anti-cheat. Walk it like this:

**Step 1 — Requirements.**
- *Functional:* matchmaking (pair players by skill), play a live game (make a move, alternate turns), **server-side move validation** (legality + whose turn), per-player clocks, game-over detection (checkmate/resign/timeout/draw), game history & replay, Elo ratings, spectators, chat (optional).
- *Non-functional:* **low latency** on moves (feels instant), **strong consistency** of game state (both players must see the same board), high availability, scale to many concurrent games, **anti-cheat** (never trust the client).
- *Out of scope (say so):* the chess AI engine, payments, video — focus on real-time play.

**Step 2 — Scale guess.** Say ~1M daily users, ~50k concurrent games at peak, each game a few moves/min → modest QPS but lots of **long-lived connections** and strict latency. That points to WebSockets + in-memory game state.

**Step 3 — Core operations.** `findMatch(userId, rating)`, `makeMove(gameId, move)`, `resign(gameId)`, plus server→client events `opponentMove`, `clockUpdate`, `gameOver`.

**Step 4 — Data model.**
- `Users(id, rating, ...)`, `Games(id, whiteId, blackId, moves[], result, timeControl, startedAt)`, `Ratings`. **Key insight:** a chess game is naturally **event-sourced** — the *list of moves IS the source of truth* (store moves as PGN), and the current board (FEN) is a derived/materialized view you can replay. Persist finished games to SQL/durable store; keep active games hot in memory/Redis.

**Step 5 — High-level architecture.**
```
            ┌───────────────┐
 Clients ──►│ WebSocket      │   (memory-bound: holds many
 (browser)  │ Gateway layer  │    long-lived connections)
            └──────┬─────────┘
                   │ (route by gameId, e.g. pub/sub or sticky)
            ┌──────▼─────────┐
            │ Game Service   │   (CPU-bound: validates moves,
            │ = state machine│    enforces turns + clocks)
            └──┬─────────┬───┘
        ┌──────▼──┐  ┌───▼──────────┐
        │ Redis   │  │ Kafka/queue  │──► Rating service (Elo, async)
        │ (live   │  └──────────────┘──► Persistence (game history DB)
        │  state) │
        └─────────┘
   Matchmaking Service ──► pairs queued players, creates a game
```
**Key design point Eric will like:** *split the WebSocket gateway from the game logic.* Connection-handling is **memory-bound** (tons of idle sockets); game logic is **CPU-bound** (validation). Separating them lets each scale independently.

**Step 6 — Deep dive: the move flow (the heart of it).**
1. Player A sends `makeMove` over their WebSocket.
2. The **game server is the authority**: it checks *is it A's turn? is the move legal? has A's clock expired?* (Server-side validation = your anti-cheat — never trust the client's claim.)
3. Update game state (append move, switch turn, update clocks). Server is the source of truth for the **clock** (handle network latency fairly).
4. Broadcast the new state to Player B (and spectators) over their WebSockets.
5. Append the move to the durable log (event sourcing); on game end, enqueue a rating update (async via Kafka).

**Step 7 — Scale, failure, tradeoffs.**
- **Sticky routing:** a WebSocket lives on one gateway instance for the whole game; both players in a game must coordinate on the same game state — route by `gameId` (consistent hashing) or share state via Redis + pub/sub so any server can fan out.
- **Sharding:** games are independent → shard by `gameId` and scale game servers horizontally.
- **Resilience / reconnection:** if a game server crashes, **Redis** holds the live state so the game survives; if a player drops, they **reconnect** and rehydrate state from the move log. Every layer assumes the one below can fail.
- **Matchmaking:** queue players, pair by close rating within a widening range over time; needs a big enough pool for fast matches.
- **Don't over-engineer:** chess.com famously ran on a single MySQL for years. Start simple (one DB), add Redis → sharding → multi-region *as traffic demands*. Saying this shows maturity.
- **Spectators / leaderboard:** pub/sub fan-out for spectators; Redis sorted sets for leaderboards.

---

## 4. ⭐ Worked example B — "Design TherAlign's medication-review / CDS system"

Be ready for this — Eric is the architect of exactly this, and even if the prompt is generic chess.com-style, weaving in their domain shows fit and lets you flex your **grounded-AI** strength. (Also a strong thing to *offer*: "I could also walk through how I'd architect something like your product.")

**Step 1 — Requirements.**
- *Functional:* provider launches the app inside the EHR (**SMART on FHIR**); app pulls patient context (current meds, conditions, allergies, insurance/coverage) via **FHIR**; for a chosen drug, return **covered, clinically-appropriate alternatives** with formulary/coverage status, **PA-approval likelihood**, **comparative-efficacy evidence**, and a plain reason; provider reviews and chooses.
- *Non-functional:* **trust/explainability** (clinical safety — never a black box), **low-ish latency** (provider is waiting at point of care), **security/PHI/HIPAA**, **auditability**, availability, graceful degradation when an external source is down.
- *Out of scope:* training the ML models themselves, the EHR's own UI.

**Step 3 — Core operation.** `getAlternatives(patientContext, drug) → [ {alt, coverageStatus, paLikelihood, evidence[], rationale, confidence} ]`.

**Step 5 — High-level architecture.**
```
 EHR (Epic) ──SMART-on-FHIR launch (OAuth2/PKCE + OIDC)──► TherAlign App (Next.js/React)
                                                                  │ getAlternatives
                                                          ┌───────▼─────────┐
                                                          │ Orchestrator    │ (fan-out/fan-in)
                                                          └─┬───┬───┬───┬───┘
        ┌───────────────────┬──────────────────┬──────────┘   │   │   │
        ▼                   ▼                  ▼               ▼   ▼   ▼
  FHIR client        Drug normalize     Coverage/Formulary  Evidence   Prediction
 (patient meds,       (→ RxNorm)         + PA-rules service  service     models
  conditions,                                                (PubMed     (efficacy,
  allergies)                                                  RAG)        PA-likelihood)
        └──────────────► Safety guardrails (allergy / interaction / contraindication) ──┐
                                                                                         ▼
                                        Gemini structured output + verification + provenance
                                                                                         │
                                              Audit log (PHI), Secret Manager, GCP/Firebase
```

**Step 6 — Deep dive: making the AI trustworthy (your sweet spot).**
- **Grounding, not guessing:** retrieve real evidence (formulary rules, PubMed abstracts) and feed it to the LLM (**RAG**); force **structured output** (validated JSON), not free text.
- **Verification + rule-based fallback:** validate the LLM's output against the retrieved facts; if it's uncertain or the LLM is down, fall back to deterministic rules. *(This is literally your AgenticSearch design.)*
- **Provenance:** every recommendation links to its source (which guideline, which formulary entry) so a clinician — and an auditor — can see *why*. (Your "cell-level provenance.")
- **Hard safety guardrails:** deterministic allergy/contraindication/interaction checks that can veto an LLM suggestion. **Human-in-the-loop:** suggest, never auto-prescribe.

**Step 7 — Scale, latency, failure, tradeoffs.**
- **Latency:** the per-alternative lookups (coverage, evidence, prediction) are independent → **fan out in parallel and join**; stream partial results to the UI; precompute/cache the slow-moving stuff.
- **Caching:** drug data (RxNorm), formulary tables, and literature retrieval are highly cacheable (they change slowly). **Live patient data is PHI — don't cache carelessly.**
- **External-dependency failure:** EHR, formulary API, PubMed, and the LLM can all fail → timeouts + **graceful degradation** (e.g., still show coverage + alternatives even if evidence retrieval times out, clearly marked).
- **Security:** OAuth2/OIDC, encryption in transit + at rest, **audit logging** of every PHI access, secrets in **Secret Manager**, least privilege — HIPAA posture. (Tie to your Wysa security work.)
- **Tradeoff to name:** real-time computation (fresh, slower) vs precomputed alternatives (fast, possibly stale) — and LLM richness vs deterministic safety. State your default and why.

---

## 5. A couple more prompts to have a skeleton for

If Eric throws something else, the framework + cheat sheet carry you. Quick scaffolds:

- **Real-time chat / notifications:** WebSockets/SSE for delivery, a message queue for fan-out, store messages in a write-optimized store, presence via Redis, push notifications async. (Overlaps heavily with chess.com.)
- **A read-heavy web service (e.g., URL shortener / a CRUD product at scale):** the classic scaling story — LB → stateless app servers → **cache** in front of the DB → read replicas → shard when the single DB is the bottleneck. Hash/counter for ID generation; consistency mostly eventual.
- **A "design our product" / domain prompt:** reuse Worked Example B.

You don't need to memorize these — recognize the shape and apply Section 1.

---

## 6. Delivery tips (especially for an open-ended, remote round)

- **Drive it.** They give vagueness on purpose; *you* supply structure. Lead with "Here's how I'll approach this," then run the 7 steps.
- **Clarify before designing.** 5 minutes of good questions prevents 30 minutes of solving the wrong problem. Eric (and Dachuan) explicitly value asking questions and coachability — this round rewards it.
- **State assumptions and move on.** "I'll assume X; flag me if not." Don't freeze on missing info.
- **Think out loud.** Silence reads as stuck. Narrate your reasoning and tradeoffs continuously.
- **Breadth first, then depth.** Get a working end-to-end design on the board, *then* deep-dive. Don't rat-hole on one component early.
- **Name tradeoffs constantly** — that's the senior signal Eric is listening for. There's rarely one right answer; there are choices with consequences.
- **Follow his steer.** When he asks "what about when this fails?" or "how would you scale this?", he's handing you the deep-dive — take it.
- **Don't bluff.** If you don't know a specific tech, reason from fundamentals or say "I'd evaluate X vs Y." Staff engineers smell bluffing instantly; honesty + reasoning beats fake confidence.
- **Use their domain when natural** — even on a generic prompt, a healthcare/PHI aside shows you're already thinking like a TherAlign engineer.
- **Manage time** (~45 min): ~5 clarify, ~5 high-level, ~20 deep-dive, ~10 scale/failure, ~5 wrap-up.
- **Wrap up cleanly:** 30-sec recap + "with more time I'd also tackle…". Mirrors the documentation/clarity Eric praised in Vishnu.

**Logistics to set up beforehand:**
- Confirm **11 AM ET Monday** with Eric (reply + accept the invite).
- Have a **drawing tool** ready and *practice on it*: [Excalidraw](https://excalidraw.com) (free, no login) or draw.io. Be ready to share your screen, or ask at the start "would you like me to share a diagram?"
- Quiet space, camera/mic tested, resume + this doc open on a second screen.
- Do **1–2 timed practice runs** out loud this week (chess.com + TherAlign-CDS). Talking through it is a different skill than reading it.

---

## 7. Questions to ask Eric (technical-peer flavor)

- "What does your architecture look like today, and where's the biggest scaling or reliability challenge right now?"
- "How do you balance LLM-driven flexibility against the determinism and safety a clinical tool needs?"
- "How are you handling the Epic / FHIR integration — directly, or through an aggregator like Redox?"
- "What does the path from prototype to production-in-a-clinic look like technically — what worries you most?"
- "How do you think about testing and trust for the AI/ML pieces as real outcome data comes in?"
- "What would make someone a great fit on the engineering side here over the summer?"

---

### One-line framing to open with
> "Since it's open-ended, let me start by clarifying the requirements and scope, throw out a couple of scale assumptions, sketch a high-level design, and then we can deep-dive wherever you find most interesting — sound good?"
