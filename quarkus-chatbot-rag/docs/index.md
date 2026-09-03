# Quarkus REST API Golden Path

This Software Template provides a golden path for creating new Quarkus REST API applications with built-in
security, compliance, and deployment best practices enforced by the platform engineering team.

## What It Creates

The template scaffolds a complete application environment:

- **Source repository** — Quarkus REST API project with Maven build, health checks, and a sample endpoint
- **GitOps repository** — Helm-based manifests for build pipeline and application deployment
- **Infrastructure bootstrap** — Namespaces, RBAC, and Argo CD Applications for three environments

## Environments

| Environment | Managed By | Purpose |
|-------------|------------|---------|
| Build | `rhdh-gitops` | Secured CI/CD pipeline with Tekton |
| Dev | `rhdh-gitops` | Auto-deployed on push to `main` |
| Prod | `rhdh-gitops` | Promoted via git tag |

Namespaces and RBAC are managed by `openshift-gitops` (cluster-level) to enforce separation of concerns.

## Security Features

The build pipeline automatically enforces:

- **SonarQube scanning** — static code analysis
- **ACS image scanning** — vulnerability detection in container images
- **ACS image check** — policy compliance verification
- **Tekton Chains signing** — cryptographic image signing
- **SBOM generation** — software bill of materials uploaded to Trusted Profile Analyzer

## Usage

1. Open Red Hat Developer Hub and navigate to the **Create** page
2. Select the **Quarkus REST API** template
3. Fill in the application details:
   - **Application Name** — lowercase, hyphens allowed
   - **Owner** — the team that owns this component
   - **Developer Group** — the group granted edit access to all namespaces
   - **Description** — shown in the Backstage catalog
4. Choose the Quay image organization
5. Review and create

## After Creation

- The Argo CD Applications may take a moment to reconcile and deploy the initial environment
- Push code to the source repository to trigger the build pipeline
- Create a git tag to promote a build to production
- View CI/CD status in the Backstage component page (CI and CD tabs)
- Open the application in Dev Spaces using the link in the component overview
