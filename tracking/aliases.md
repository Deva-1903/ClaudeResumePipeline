# Keyword aliases

Canonical-name map for the skill-gap aggregator (`skill_gaps.jsonl`).

`/lean-apply` and `/revise-resume` apply this map (case-insensitive) before incrementing counts so spellings like `k8s`, `K8S`, `kubernetes`, and `Kubernetes` collapse to one entry.

## Format

```
<alias>  =>  <canonical>
```

One mapping per line. Comments start with `#`. The canonical name on the right is what shows up in `skill_gaps.jsonl` and `/skill-gaps` output.

If a keyword does not match any alias, it is kept as-typed (after trimming whitespace and surrounding punctuation).

## Aliases

# Languages
k8s              => Kubernetes
kubernetes       => Kubernetes
golang           => Go
go-lang          => Go
nodejs           => Node.js
node             => Node.js
node.js          => Node.js
typescript       => TypeScript
ts               => TypeScript
javascript       => JavaScript
js               => JavaScript
py               => Python
python3          => Python

# Databases
postgres         => PostgreSQL
postgresql       => PostgreSQL
psql             => PostgreSQL
mongo            => MongoDB
mongodb          => MongoDB
mysql            => MySQL

# Cloud
aws              => AWS
amazon web services => AWS
gcp              => GCP
google cloud     => GCP
google cloud platform => GCP
azure            => Azure
microsoft azure  => Azure

# Infra / Containers
docker           => Docker
containers       => Docker
container orchestration => Kubernetes
ci/cd            => CI/CD
ci               => CI/CD
cd               => CI/CD
github actions   => GitHub Actions

# Data / Streaming
kafka            => Kafka
apache kafka     => Kafka
spark            => Spark
apache spark     => Spark
pyspark          => Spark
airflow          => Airflow
apache airflow   => Airflow
snowflake        => Snowflake
databricks       => Databricks

# AI/ML
llm              => LLM
llms             => LLM
large language models => LLM
genai            => Generative AI
generative ai    => Generative AI
gen ai           => Generative AI
rag              => RAG
retrieval augmented generation => RAG
retrieval-augmented generation => RAG
mcp              => MCP
model context protocol => MCP
pytorch          => PyTorch
tensorflow       => TensorFlow
hugging face     => Hugging Face
huggingface      => Hugging Face
transformers     => Hugging Face Transformers

# Frontend
react            => React
react.js         => React
reactjs          => React
next             => Next.js
nextjs           => Next.js
next.js          => Next.js

# Backend
graphql          => GraphQL
grpc             => gRPC
rest             => REST APIs
rest api         => REST APIs
rest apis        => REST APIs
restful          => REST APIs

# Concepts
distributed systems => Distributed Systems
microservices    => Microservices
observability    => Observability
sre              => SRE
site reliability => SRE
