# Configuration Management

## Configuration Sources

### Application Properties

Non-sensitive configuration lives in `src/main/resources/application.properties`:

```properties
quarkus.langchain4j.openai.chat-model.model-name=granite-3-2-8b-instruct
quarkus.langchain4j.openai.embedding-model.model-name=nomic-embed-text-v1-5
quarkus.langchain4j.openai.chat-model.temperature=0
```

### Secrets from Vault

Sensitive configuration (API keys, endpoints) is stored in **HashiCorp Vault** and injected at runtime via the **External Secrets Operator**:

```
Vault → External Secrets Operator → Kubernetes Secret → Pod Environment Variables
```

Your application receives:

- `QUARKUS_LANGCHAIN4J_OPENAI_API_KEY` — LLM API key
- `QUARKUS_LANGCHAIN4J_OPENAI_BASE_URL` — LLM service endpoint

These are managed by the platform team. Developers never need to handle API keys directly.

## ExternalSecret

An `ExternalSecret` resource in the GitOps repository maps Vault paths to Kubernetes Secret keys:

```yaml
spec:
  secretStoreRef:
    name: vault-secret-store
    kind: ClusterSecretStore
  data:
    - secretKey: QUARKUS_LANGCHAIN4J_OPENAI_API_KEY
      remoteRef:
        key: kv/litellm
        property: virtual_key
    - secretKey: QUARKUS_LANGCHAIN4J_OPENAI_BASE_URL
      remoteRef:
        key: kv/litellm
        property: base_url
```

Secrets are refreshed automatically every hour.

## Local Development

For local development, set environment variables directly:

```bash
export QUARKUS_LANGCHAIN4J_OPENAI_API_KEY="your-key"
export QUARKUS_LANGCHAIN4J_OPENAI_BASE_URL="http://localhost:11434/v1"
./mvnw quarkus:dev
```
