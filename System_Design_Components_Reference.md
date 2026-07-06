# System Design — Components & Concepts Reference

A study reference of the building blocks you compose in any design interview. Learn these as a vocabulary; then in a problem you just *pick the right ones and justify them*.

**How each entry reads:** what it is → why/when you use it → a concrete example (mostly chess.com, so it links to what you already know).

**Priority key:**
- ⭐ **Must-know** — you'll use these in almost every interview. Learn cold.
- ◆ **Good-to-know** — comes up often; understand the idea.
- ○ **Bonus** — nice depth if asked, don't sweat it first pass.

**The 7-step framework these plug into** (your spine for any prompt):
1. Clarify requirements & scope → 2. Estimate scale → 3. Define API → 4. Data model → 5. High-level architecture → 6. Deep dive → 7. Scale, failure, tradeoffs.

---

## 1. Estimation & Capacity Planning

**Back-of-the-envelope estimation** ⭐
What: rough math on users, requests/sec, storage, bandwidth to justify design choices.
Why: it tells you whether you need 1 DB or 100, a cache, sharding, etc. Don't over-math — 2–3 numbers.
Example: chess.com → 200k concurrent players ⇒ ~100k games ⇒ "lots of persistent connections, modest compute" ⇒ WebSocket tier + in-memory state.

**Numbers worth memorizing** ◆
- 1 server handles ~1k–10k simple requests/sec; a heavy endpoint far fewer.
- Memory read ≈ nanoseconds; SSD ≈ microseconds; network round-trip within a datacenter ≈ ~0.5ms; cross-region ≈ tens–hundreds of ms.
- 1 day ≈ 86,400 sec (~10^5). DAU ÷ 10^5 ≈ average requests/sec if each user makes ~1/day.

---

## 2. Networking & Communication

**DNS** ◆
What: translates a domain (chess.com) into an IP address.
Why: the first hop; can also do geo-routing (send users to the nearest region).
Example: a user in India resolves chess.com to the closest regional entry point.

**Load Balancer (LB)** ⭐
What: distributes incoming traffic across many identical servers; health-checks them and routes around dead ones.
Why: enables horizontal scaling + high availability; no single box is overwhelmed.
Example: chess.com's public entry point spreads HTTP requests across app-server instances (round-robin / least-connections). *L4* balances by TCP/IP (fast, dumb); *L7* understands HTTP (can route by URL path).

**Reverse proxy** ◆
What: a server that sits in front of your app servers, forwarding client requests to them.
Why: centralizes TLS termination, compression, caching, routing. (An LB is often a reverse proxy too; nginx is the classic example.)

**API Gateway** ⭐
What: a smart entry point that does cross-cutting concerns — auth/token validation, rate limiting, TLS, logging — and routes each request to the right backend service by path.
Why: keeps that logic out of every service; one front door.
Example: `/auth/*` → Auth service, `/profile/*` → Profile service. (LB spreads load; API gateway adds routing + auth.)

**CDN (Content Delivery Network)** ◆
What: a globally distributed cache for static content (images, JS, CSS, video) served from a location near the user.
Why: cuts latency and offloads your origin servers.
Example: chess piece images, the web app bundle, opening-theory videos served from the nearest CDN edge.

**HTTP / HTTPS & REST** ⭐
What: HTTP = the web's request/response protocol; HTTPS = encrypted via TLS. REST = the conventional style for HTTP APIs (resources + verbs GET/POST/PUT/DELETE).
Why: the default for request/response APIs; simple, cacheable, universal.
Example: `GET /games/{id}` to fetch a finished game for replay.

**RPC / gRPC** ◆
What: "call a function on another server like it's local." gRPC is a fast binary RPC framework (HTTP/2 + protobuf).
Why: efficient *service-to-service* communication (internal), lower overhead than REST/JSON.
Example: the API gateway → game-history service call could be gRPC internally.

**WebSocket** ⭐
What: a persistent, **two-way** connection (starts as an HTTP "upgrade" handshake, then stays open).
Why: real-time push both directions without re-requesting; low latency.
Example: a player's live game connection — the server pushes the opponent's move instantly.

**Server-Sent Events (SSE)** ◆
What: a **one-way** server→client push stream over HTTP.
Why: simpler than WebSocket when only the server needs to push (client can't send on it).
Example: a live scoreboard / notifications feed (but NOT chess moves, since the client must send moves too).

**Polling (short & long)** ◆
What: client repeatedly asks "anything new?" Short = ask on a timer; long = server holds the request open until there's news.
Why: simple fallback when WebSocket/SSE aren't available; wasteful and laggy.
Example: a basic client checking for a matchmaking result every 2s.

**Webhook** ○
What: a reverse callback — *you* give another service a URL, and it POSTs to you when an event happens.
Why: event notifications between systems without polling.
Example: a payment provider notifying your server that a subscription renewed.

---

## 3. Application Tier & Scaling

**Vertical vs Horizontal scaling** ⭐
What: vertical = bigger machine (more CPU/RAM); horizontal = more machines.
Why: vertical is simple but has a ceiling + single point of failure; horizontal scales near-infinitely and is resilient. Prefer horizontal.
Example: chess.com adds more game-server instances (horizontal) rather than one giant box.

**Stateless vs Stateful services** ⭐
What: stateless = keeps no per-client memory between requests (state lives in a token/DB); stateful = holds state in its own memory.
Why: stateless services scale trivially (any server handles any request — easy load balancing). Stateful ones (like the game server holding a live board) need sticky routing + external backup.
Example: auth/profile servers = stateless (identity in a JWT); game server = stateful (live board), backed by Redis so it's "stateless-ish."

**Monolith vs Microservices** ◆
What: monolith = one deployable app; microservices = many small independently-deployed services.
Why: monolith is simpler to start (do this early — "don't over-engineer"); microservices help large teams scale independently but add complexity (network calls, ops).
Example: chess.com could start as one app, later split out Matchmaking, Game, Rating, History services.

**CPU-bound vs Memory-bound vs I/O-bound** ⭐
What: which resource a component runs out of first.
Why: tells you how to scale it and what hardware to buy — and when to split tiers.
Example: WS gateway = memory-bound (holds idle connections); game server = CPU-bound (move validation). Split them so each scales on its own axis.

---

## 4. Databases & Storage

**SQL / Relational DB** ⭐
What: structured tables with schemas; supports joins and **ACID** transactions (Atomicity, Consistency, Isolation, Durability).
Why: default choice for structured data needing consistency/transactions.
Example: `Users`, `Games`, `RatingHistory` in Postgres. (Postgres, MySQL.)

**NoSQL** ⭐
What: non-relational stores. Types: **key-value** (Redis, DynamoDB), **document** (MongoDB), **wide-column** (Cassandra), **graph** (Neo4j).
Why: flexible schema, easy horizontal scaling, great for huge volume or simple access patterns; usually weaker on joins/multi-row transactions.
Example: append-only move events or a high-volume activity feed in a wide-column store.

**Indexing** ⭐
What: a data structure (usually a B-tree) that makes lookups on a column fast instead of scanning every row.
Why: turns an O(n) table scan into O(log n); essential for query performance.
Example: index `Games.white_id` so "all of this player's games" is fast. (Cost: slower writes + more storage.)

**Replication** ⭐
What: keep copies of the DB on multiple nodes — typically a primary (writes) + read replicas (reads).
Why: scales reads, provides failover/HA, geographic locality.
Example: history-page reads hit Postgres read replicas; replicas are usually *eventually consistent* (slight lag).

**Sharding / Partitioning** ⭐
What: split data across nodes by a key (e.g., `user_id`) so no single node holds everything.
Why: scales writes and storage past one machine.
Example: shard users by `user_id`; shard active games across game servers by `gameId`. Watch for **hot partitions** (one shard getting disproportionate traffic, e.g., a celebrity).

**Consistency models** ⭐
What: **strong** = every read sees the latest write; **eventual** = reads may be briefly stale but converge.
Why: strong is needed for correctness-critical data (money, a game's board); eventual is cheaper and scales better (feeds, view counts).
Example: a single game's state = strong (one authoritative owner); a global "games played today" counter = eventual is fine.

**CAP theorem** ◆
What: under a network **P**artition you must choose **C**onsistency or **A**vailability — can't have both.
Why: forces you to state what matters per data type.
Example: for live game state you'd favor consistency (don't show a wrong board); for a leaderboard you'd favor availability (slightly stale is fine).

**Denormalization** ◆
What: deliberately duplicate data to avoid expensive joins at read time.
Why: trades write complexity/storage for fast reads.
Example: store a player's current rating directly on the game record so the replay page needs no extra join.

**Object / Blob storage** ◆
What: store large files (images, video, backups) in a service like Amazon S3, not in your DB.
Why: cheap, durable, scalable for big binary data; DBs are bad at this.
Example: archived PGN files, profile pictures, video lessons.

---

## 5. Caching

**Caching (general)** ⭐
What: keep frequently-needed data in a fast layer (memory) so you don't recompute or re-fetch it.
Why: cuts latency and load on your DB/services; often the single biggest performance win.
Example: cache a user's profile and rating in Redis so it isn't read from Postgres every request.

**Where caches live** ◆
Browser cache → CDN → API/in-app cache → distributed cache (Redis/Memcached) → DB's own cache. Each layer closer to the user is faster.

**Cache strategies** ⭐
- **Cache-aside (lazy):** app checks cache; on miss, reads DB and populates cache. Most common.
- **Write-through:** write to cache and DB together (cache always fresh; slower writes).
- **Write-back:** write to cache, flush to DB later (fast, risk of loss on crash).
Example: game state uses write-through-ish to Redis so a backup is always current.

**Eviction policies** ◆
What: how the cache decides what to drop when full — **LRU** (least recently used, most common), **LFU** (least frequently used), **TTL** (expire after time).
Example: cached PubMed/opening data with a TTL since it changes slowly.

**Cache invalidation** ⭐
What: keeping the cache from serving stale data after the source changes. ("One of the two hard problems in CS.")
Why: stale data causes bugs; strategy = TTLs, explicit invalidation on write, or versioned keys.
Example: bump the cache key when a user's rating changes so old value isn't served.

**Redis / Memcached** ⭐
What: in-memory data stores used as caches and more. Redis is a multi-tool: strings, **hashes** (game state), **sorted sets** (matchmaking queue, leaderboards), **pub/sub** (move fan-out), TTLs, Lua scripts.
Why: microsecond access; far more than a cache.
Example: in chess it's cache + live state + queue + leaderboard + pub/sub — all at once.

---

## 6. Asynchronous Processing & Messaging

**Message Queue** ⭐
What: a buffer where producers drop tasks and consumers process them later (FIFO-ish, at-least-once delivery). e.g., AWS SQS, RabbitMQ.
Why: decouple slow/spiky work from the request path; smooth out load; retry on failure.
Example: "send game-summary email" dropped on a queue; a worker handles it later — the user isn't blocked.

**Pub/Sub** ⭐
What: publish a message to a *channel*; all current subscribers receive it (one-to-many). Distinct from a queue (one consumer pulls each message).
Why: fan-out an event to many recipients without the publisher knowing who they are.
Example: a game server publishes a move to `game:1234`; every gateway holding that game's players/spectators delivers it locally.

**Event streaming / Kafka** ⭐
What: a durable, replayable, high-throughput log of events that multiple consumers read independently.
Why: backbone of event-driven systems; durable (unlike Redis pub/sub), ordered per partition, lets you add new consumers later.
Example: `gameOver` events → Kafka → consumed by the Rating service AND the Persistence service AND analytics, independently.

**Background workers / job queue** ◆
What: a pool of processes that pull work off a queue and do it asynchronously.
Why: offload CPU-heavy or slow tasks (image resize, report generation, ML inference) off the request tier.
Example: post-game analysis ("you blundered on move 23") run by workers, not inline.

**Idempotency** ⭐
What: designing an operation so doing it twice has the same effect as once.
Why: queues/retries can deliver a message more than once; idempotency prevents double-charges, double-counts.
Example: key the `gameOver` event by `gameId` so a redelivery never applies the rating change twice.

**Event-driven architecture** ◆
What: services communicate by emitting/reacting to events rather than direct calls.
Why: loose coupling, scalability, easy to add new reactions.
Example: "game ended" event triggers rating update, persistence, achievements, and a friend-notification — all independent.

---

## 7. Distributed Systems Patterns

**Consistent hashing** ⭐
What: a hashing scheme (a "ring") that maps keys to servers such that adding/removing a server only remaps a *small fraction* of keys (not all of them, like naive `hash % N` would).
Why: lets you scale a sharded/stateful tier in and out cheaply.
Example: routing `gameId → game server`; when one server dies, only its ~1/N games remap, the rest stay put.

**Coordination service (ZooKeeper / etcd / Consul)** ◆
What: a small, strongly-consistent cluster (3 or 5 nodes, consensus-based) that stores cluster membership/config that everyone agrees on.
Why: a single source of truth for "who's alive and who owns what" so routers don't diverge (split-brain).
Example: gateways read the live game-server ring from etcd (cached + watched) to route consistently. (Often you get this free from Kubernetes/Redis Cluster — don't run your own unless needed.)

**Service discovery** ◆
What: how services find each other's current network addresses as instances come and go.
Why: in a dynamic fleet, you can't hardcode IPs.
Example: the API gateway looks up healthy instances of the profile service.

**Leader election** ◆
What: pick one node to be "in charge" of a task among many.
Why: some jobs need a single owner (avoid duplicate work / split-brain).
Example: electing the single matchmaker that owns the `blitz5` bucket.

**Distributed lock** ◆
What: a lock that works across machines (often via Redis or ZooKeeper).
Why: ensure only one process does a critical operation at a time.
Example: prevent two matchmaker workers from pairing the same waiting player.

**Consensus (Raft / Paxos)** ○
What: algorithms that let a cluster agree on a value despite failures (majority quorum).
Why: the foundation under etcd/ZooKeeper and replicated databases.
Example: how a 5-node etcd agrees on the current ring even if 2 nodes are down. (Know it exists + "quorum"; depth optional.)

---

## 8. Reliability & Resilience

**Redundancy / replication / failover** ⭐
What: run multiple copies so one failure doesn't take you down; promote a standby when the primary dies.
Why: high availability; "every layer assumes the one below can fail."
Example: Redis primary + replica across AZs; if the primary dies, the replica is promoted.

**Health checks** ⭐
What: periodic "are you alive?" probes; unhealthy instances are removed from rotation.
Why: the LB/coordination layer needs to know what's actually up.
Example: LB stops routing to a frozen app server; coordination service drops a dead game server from the ring.

**Timeouts, Retries + exponential backoff** ⭐
What: give up on a slow call after T; retry failures, waiting longer each time (1s, 2s, 4s…), ideally with jitter.
Why: prevents threads piling up on a dead dependency; avoids retry storms.
Example: a call to the rating service times out and retries with backoff instead of hanging the request.

**Circuit breaker** ◆
What: after too many failures to a dependency, "trip" and fail fast for a while instead of hammering it.
Why: stops cascading failures; gives the struggling service room to recover.
Example: if the evidence/analytics service is down, trip the breaker and skip that feature gracefully.

**Graceful degradation** ◆
What: lose a non-critical feature instead of failing the whole request.
Why: partial service beats an error page.
Example: if post-game analysis is down, still show the result and ratings.

**Rate limiting** ⭐
What: cap how many requests a client can make in a window (token bucket / leaky bucket).
Why: protects against abuse, runaway clients, and overload; fairness.
Example: limit login attempts and API calls per user; reject/queue excess.

**Backpressure** ○
What: signal upstream to slow down when a consumer can't keep up.
Why: prevents queues from growing unbounded and crashing.
Example: if persistence can't keep up with `gameOver` events, Kafka buffers and consumers catch up (instead of dropping data).

---

## 9. Real-time Communication (recap as a pattern)

**WebSocket gateway tier** ⭐
What: a fleet of servers whose job is to hold persistent client connections and route messages to backends.
Why: separating connection-holding (memory-bound) from logic (CPU-bound) lets each scale independently.
Example: chess gateways hold sockets; forward moves to the owning game server; deliver pub/sub broadcasts back.

**Sticky sessions / connection affinity** ⭐
What: keep a given client (or game) pinned to the same server for the life of the connection.
Why: stateful connections (WebSockets) and in-memory game state require it.
Example: a player's WebSocket stays on one gateway; a game's traffic stays on one game server.

**Fan-out** ⭐
What: deliver one event to many recipients.
Why: core of feeds, chat, spectators, notifications.
Example: one move → published once → fanned out to opponent + thousands of spectators across gateways.

---

## 10. Observability & Ops

**Logging, Metrics, Tracing** ⭐
What: logs = discrete events; metrics = numbers over time (latency, QPS, error rate); tracing = follow one request across services.
Why: you can't operate or debug what you can't see. Mention request IDs.
Example: structured logs with a `requestId` per move; a metric for p99 move latency; alerts when error rate spikes.

**Monitoring & alerting** ◆
What: dashboards + automatic alerts on thresholds (e.g., CPU > 80%, error rate up).
Why: detect and respond before users do.
Example: alert when active-connections per gateway nears capacity → autoscale.

**CI/CD** ○
What: automated build, test, deploy pipelines.
Why: ship safely and often; enables blue/green or canary releases.
Example: deploy a new game-server version to 5% of traffic first (canary), then ramp.

---

## 11. Security

**Authentication vs Authorization** ⭐
What: authn = *who are you* (login); authz = *what are you allowed to do* (permissions).
Why: every multi-user system needs both, kept distinct.
Example: authn logs you in; authz ensures you can only move in *your* game, on *your* turn.

**OAuth2 / JWT** ◆
What: OAuth2 = standard for delegated authorization (get a token to act on a user's behalf). JWT = a signed token carrying identity/claims, verifiable without a DB lookup.
Why: stateless auth that scales; the basis of "login with…" and API access.
Example: a JWT in each request lets any stateless app server verify identity locally.

**Encryption (in transit & at rest)** ⭐
What: TLS for data on the wire; disk/field encryption for stored data.
Why: protect against interception and breaches; often legally required (PHI/PII).
Example: HTTPS/WSS for all traffic; encrypt the user database at rest.

**RBAC (Role-Based Access Control)** ◆
What: grant permissions by role (admin, user, moderator) rather than per-person.
Why: manageable authorization at scale.
Example: only a moderator role can close a cheating account.

**Secrets management** ◆
What: store API keys/credentials in a vault (AWS Secrets Manager), never in code.
Why: leaked secrets = breaches.
Example: the game server pulls DB credentials from Secret Manager at startup.

---

## 12. Trade-off cheat sheet (say these out loud)

| Choice | Pick A when… | Pick B when… |
|---|---|---|
| SQL vs NoSQL | structured data, joins, transactions | huge scale, flexible schema, simple access |
| Strong vs Eventual consistency | correctness-critical (money, game state) | scale/availability matters, slight staleness OK |
| WebSocket vs SSE vs Polling | two-way realtime (games, chat) | one-way push (SSE) / simple fallback (polling) |
| Sync vs Async (queue) | caller needs the result now | slow/spiky/non-critical work → defer it |
| Monolith vs Microservices | early stage, small team | large org, independent scaling |
| Cache vs no cache | read-heavy, repeated, slow source | write-heavy, must-be-fresh, cheap source |
| Vertical vs Horizontal scaling | quick fix, small scale | real scale + resilience |

**Universal closers:** "There's no free lunch — I'd pick X because [requirement], accepting [cost]." / "I'd start simple and add Y when [metric] becomes the bottleneck."

---

## 13. Suggested study path (you have ~5 days)

1. **Day 1–2 (core):** all ⭐ items — networking, LB/API gateway, SQL/NoSQL, indexing, replication, sharding, consistency, caching, queues/pub/sub, stateless/stateful, horizontal scaling, consistent hashing, the resilience ⭐s. These cover ~90% of interviews.
2. **Day 3 (depth):** the ◆ items + the trade-off cheat sheet. Practice *saying* trade-offs out loud.
3. **Day 4–5 (apply):** stop reading, start designing. Do the practice problems below on a whiteboard (Excalidraw), out loud, timed ~40 min each.

**Practice problems (in rough difficulty order):**
- Design a URL shortener (the classic — LB, cache, DB, ID generation, read-heavy scaling).
- Design a rate limiter (token bucket, distributed counters in Redis).
- Design a chat / messaging app (WebSockets, fan-out, pub/sub — overlaps chess).
- Design a news feed / Twitter timeline (fan-out on write vs read, caching).
- Design a notification system (queues, workers, fan-out, idempotency).
- **Design chess.com** (your real one — you've got the dedicated doc).
- Design TherAlign's medication-review system (domain bonus — ties to the role).

**Rule for problems:** always run the 7-step framework, think out loud, state assumptions, and name a trade-off at every decision. The components above are the menu; the framework is how you order from it.
