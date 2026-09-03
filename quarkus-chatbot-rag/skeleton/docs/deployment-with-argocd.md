# Deployment with Argo CD

## GitOps Model

Your application is deployed using **GitOps** with **Argo CD**. The desired state is declared in a companion GitOps repository, and Argo CD ensures the cluster matches.

## Environments

| Environment | Namespace | Trigger |
|-------------|-----------|---------|
| Dev | `${{ values.name }}-dev` | Push to `main` branch |
| Prod | `${{ values.name }}-prod` | Git tag creation |

## How It Works

```
Code Push → Tekton Pipeline → Build & Scan → Update GitOps Repo → Argo CD Sync → Deploy
```

1. Push code to the source repository
2. Tekton pipeline builds, scans, and pushes the container image
3. Pipeline updates the image tag in the GitOps repository
4. Argo CD detects the change and deploys automatically

## Viewing Status

In **Red Hat Developer Hub**, navigate to your component and select the **CD** tab. You'll see:

- **Sync Status** — Whether deployed state matches Git
- **Health Status** — Application health across environments
- **Resource Tree** — All Kubernetes resources managed by Argo CD

## Rollback

Since everything is in Git, rollback is straightforward:

```bash
git revert <commit-hash>
git push origin main
```

Argo CD automatically deploys the previous version.
