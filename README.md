# Software Templates for Developer Self Service

This repository contains the Backstage Templates which provide self-service capabilities for developers.

## Available Templates

### Quarkus Chatbot with RAG and Secure CI/CD
**Location:** `./quarkus-chatbot-rag/template.yaml`

A golden-path template that provisions a web-based AI chatbot application with:
- Retrieval-Augmented Generation (RAG) for context-aware responses
- Prompt injection detection and guardrails
- Secure CI/CD pipeline with Tekton (image scanning, SBOM generation, policy checks)
- Multi-environment GitOps deployment (build, dev, prod) via ArgoCD
- RBAC integration with Keycloak groups
- DevSpaces support via devfile
- TechDocs documentation

### PostgreSQL 15 Database
**Location:** `./postgres15/template.yaml`

Request a PostgreSQL 15 database instance.

### Namespace Provisioning
**Locations:**
- `./namespace/template-small.yaml` - Small namespace
- `./namespace/template-large.yaml` - Large namespace with resource quotas