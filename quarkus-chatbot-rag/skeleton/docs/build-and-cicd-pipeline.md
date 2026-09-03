# Build and CI/CD Pipeline

## Overview

Your application uses **Tekton Pipelines** for CI/CD. Pushing code to Git triggers pipelines that build, test, scan, and deploy your application.

## Pipeline Stages

When you push to `main`, the pipeline executes:

1. **Clone Repository** — Checks out the triggering commit
2. **Package Application** — `mvn clean package` with unit tests
3. **Build Container Image** — Buildah builds and pushes to Quay
4. **Image Scanning** — ACS scans for CVEs and policy violations
5. **SBOM Generation** — Software Bill of Materials uploaded to Trusted Profile Analyzer
6. **Deploy Check** — ACS validates deployment against security policies
7. **Update GitOps Repository** — Commits new image tag, triggering Argo CD deployment

## Security Features

| Feature | Purpose |
|---------|---------|
| ACS Image Scan | Detect known vulnerabilities (CVEs) |
| ACS Image Check | Enforce security policies |
| Tekton Chains Signing | Cryptographic image signing |
| SBOM | Track all dependencies and their versions |

## Viewing Pipeline Runs

In **Red Hat Developer Hub**, navigate to your component and select the **CI** tab to see:

- Recent pipeline runs with status
- Duration of each stage
- Logs for debugging failures

## Production Promotion

Create a git tag to promote to production:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

The release pipeline performs Enterprise Contract verification before promoting the image.
