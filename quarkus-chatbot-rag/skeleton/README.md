# ${{ values.name }}

${{ values.description }}

An AI-powered customer support chatbot built with [Quarkus](https://quarkus.io/) and
[LangChain4j](https://docs.langchain4j.dev/), scaffolded by the Quarkus REST API golden path
template in Red Hat Developer Hub.

## Features

- **RAG chatbot** — Uses Retrieval-Augmented Generation to answer questions grounded in company policy
- **Prompt injection guardrails** — Detects and blocks prompt injection attacks using a secondary LLM
- **Function calling** — AI assistant can look up and cancel bookings through tool integration
- **WebSocket chat UI** — Real-time bidirectional communication

## Environments

| Environment | Namespace | Purpose |
|-------------|-----------|---------|
| Build | `${{ values.name }}-build` | Secured CI/CD pipeline with scanning, signing, and SBOM generation |
| Dev | `${{ values.name }}-dev` | Development deployment (auto-deployed on push) |
| Prod | `${{ values.name }}-prod` | Production deployment (promoted via git tag) |

## Running locally in dev mode

```shell
./mvnw quarkus:dev
```

You'll need an OpenAI-compatible LLM endpoint. Set these environment variables:

```shell
export QUARKUS_LANGCHAIN4J_OPENAI_BASE_URL="http://localhost:11434/v1"
export QUARKUS_LANGCHAIN4J_OPENAI_API_KEY="demo"
```

The chat UI is available at <http://localhost:8080>. Dev UI is at <http://localhost:8080/q/dev/>.

## Building

```shell
./mvnw package
```

The application is runnable with `java -jar target/quarkus-app/quarkus-run.jar`.

## CI/CD Pipeline

Pushing to the `main` branch triggers the build pipeline which:

1. Builds the application with Maven
2. Builds and pushes a container image to Quay
3. Scans the image with ACS (Advanced Cluster Security)
4. Signs the image with Tekton Chains
5. Generates and uploads an SBOM to TPA (Trusted Profile Analyzer)
6. Deploys to the dev environment via GitOps

### Production Promotion

Create a git tag to promote to production.

## Learn More

- [Quarkus documentation](https://quarkus.io/)
- [Quarkus LangChain4j extension](https://docs.quarkiverse.io/quarkus-langchain4j/dev/index.html)
- [LangChain4j documentation](https://docs.langchain4j.dev/)
