# Application Overview

## What Does This Application Do?

This is an AI-powered customer support chatbot for **Miles of Smiles**, a fictional car rental company. It demonstrates how to build intelligent, conversational applications using Large Language Models (LLMs) with Quarkus and LangChain4j.

### Core Features

1. **Intelligent Conversation** — Uses an LLM to understand natural language queries and provide helpful responses about car rental bookings

2. **RAG (Retrieval-Augmented Generation)** — The chatbot uses Easy RAG to incorporate the company's Terms of Service into its knowledge base, ensuring accurate policy information

3. **Function Calling (Tools)** — The AI assistant can execute real business operations:
   - Look up booking details
   - Cancel bookings (with proper validation)

4. **Security Guardrails**:
   - **Prompt Injection Detection** — Protects against malicious attempts to manipulate the AI
   - **Business Logic Validation** — Enforces cancellation policies (e.g., no cancellations within 7 days of booking start date)

5. **Real-time WebSocket Communication** — Bidirectional communication for a smooth chat experience

## Technical Architecture

### Key Components

| Component | File | Purpose |
|-----------|------|---------|
| Chat Interface | `ChatSocket.java` | WebSocket endpoint for real-time chat |
| AI Assistant | `AssistantForCustomerSupport.java` | Core AI service with system prompts and guardrails |
| Booking Tools | `BookingTools.java` | LLM-callable tools for booking operations |
| Booking Service | `BookingService.java` | Business logic for bookings |
| Prompt Guard | `PromptInjectionGuard.java` | Detects and blocks prompt injection attacks |
| RAG Data | `catalog/miles-of-smiles-terms-of-use.txt` | Knowledge base for the AI |

### LLM Configuration

The application connects to an **OpenAI-compatible LLM API** managed by the platform team via a LiteLLM proxy:

- **Chat Model**: `granite-3-2-8b-instruct` — IBM's Granite model
- **Embedding Model**: `nomic-embed-text-v1-5` — For vector embeddings (RAG)

API credentials are injected at runtime from Vault via External Secrets. See [Configuration Management](./configuration-management.md).

## Customizing the Application

1. **Modify the System Prompt** — Edit `AssistantForCustomerSupport.java` to change the AI's role and behavior
2. **Add Your Own Tools** — Create new `@Tool` methods for your business logic
3. **Update the Knowledge Base** — Replace content in `src/main/resources/catalog/` with your own documents
4. **Adjust Guardrails** — Tune the injection detection threshold in `PromptInjectionGuard.java`
