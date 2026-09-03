# ${{ values.name }}

${{ values.description }}

## Key Features

- **AI-Powered Customer Support** — LLM-based chatbot using Quarkus and LangChain4j
- **RAG (Retrieval-Augmented Generation)** — Terms of service automatically embedded for accurate responses
- **Prompt Injection Guardrails** — Security layer that detects and blocks prompt injection attacks
- **Function Calling** — AI assistant can look up and cancel bookings through tool integration
- **Real-time WebSocket Chat** — Instant bidirectional communication via WebSocket

## Architecture

| Component | Technology |
|-----------|------------|
| Framework | Quarkus |
| AI Integration | LangChain4j (OpenAI-compatible API) |
| Chat Transport | WebSocket |
| LLM Provider | Platform-managed LiteLLM proxy |
| Deployment | Argo CD (GitOps) |
| CI/CD | Tekton Pipelines |

## Environments

| Environment | Namespace | Purpose |
|-------------|-----------|---------|
| Build | `${{ values.name }}-build` | Secured CI/CD pipeline |
| Dev | `${{ values.name }}-dev` | Auto-deployed on push to `main` |
| Prod | `${{ values.name }}-prod` | Promoted via git tag |

## Quick Links

- [Application Overview](./application-overview.md) — How the chatbot works
- [Development Environment](./development-environment.md) — Getting started with Dev Spaces
- [Deployment with Argo CD](./deployment-with-argocd.md) — GitOps deployment model
- [Build and CI/CD Pipeline](./build-and-cicd-pipeline.md) — Pipeline stages and security scanning
- [Configuration Management](./configuration-management.md) — Secrets and runtime configuration
