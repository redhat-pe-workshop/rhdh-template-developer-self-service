# ${{ values.name }} GitOps configuration

This repository contains the build and deployment configuration for **${{ values.name }}**, a Quarkus AI chatbot with Retrieval-Augmented Generation (RAG). Application code lives in the separate [source repository](${{ values.source_repo }}).

Argo CD watches this repository and uses the platform team's reusable Helm charts to manage the application's build, development, and production environments.

## Repository layout

- **[`build/`](build/)** configures the secured CI/CD pipeline in the `${{ values.name }}-build` namespace. `Chart.yaml` references the platform's `build-deployer` chart, and `values.yaml` supplies application-specific settings such as the source repository, container image, webhook, and promotion configuration.
- **[`app/`](app/)** configures the running application using the platform's `app-deployer` chart. `values/values-dev.yaml` controls the `${{ values.name }}-dev` environment, and `values/values-prod.yaml` controls `${{ values.name }}-prod`, including image tags, replica counts, and runtime settings. `templates/` contains the ExternalSecret for the application's LLM credentials.

## Making changes

Push application code to the source repository to trigger the build pipeline. To change deployment settings, update the appropriate values file in this repository. Argo CD reconciles changes on `main` into the cluster.

The platform's infrastructure repository manages the namespaces and Argo CD Applications that connect these folders to the cluster.
