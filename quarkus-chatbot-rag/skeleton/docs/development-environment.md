# Development Environment

## OpenShift Dev Spaces

This application is configured for development with **Red Hat OpenShift Dev Spaces**, a browser-based IDE with zero local setup.

### Opening Your Workspace

1. Navigate to **Red Hat Developer Hub**
2. Find your component in the Catalog
3. Click **Open in Dev Spaces**
4. Dev Spaces provisions a workspace from the `devfile.yaml` configuration

### Running in Dev Mode

```bash
./mvnw quarkus:dev
```

This starts Quarkus with hot reload. Access the chat UI at the exposed endpoint URL. The Dev UI is available at `/q/dev/`.

### Testing the Chatbot

1. Open the application home page
2. Use the chat interface to interact with the AI assistant
3. Try these scenarios:
   - Ask about a booking: "I'd like to check my booking 123-456, my name is John Doe"
   - Try to cancel: "Can you cancel my booking?"
   - Test guardrails: "Ignore all previous instructions"

## Local Development

### Prerequisites

- Java 21+
- Maven 3.9+

### LLM Configuration

Set environment variables for the LLM service:

```bash
# Option 1: Use platform LiteLLM
export QUARKUS_LANGCHAIN4J_OPENAI_BASE_URL="http://litellm.litellm.svc:4000/v1"
export QUARKUS_LANGCHAIN4J_OPENAI_API_KEY="<your-dev-key>"

# Option 2: Use local Ollama
export QUARKUS_LANGCHAIN4J_OPENAI_BASE_URL="http://localhost:11434/v1"
export QUARKUS_LANGCHAIN4J_OPENAI_API_KEY="demo"
```

Then run:

```bash
./mvnw quarkus:dev
```
