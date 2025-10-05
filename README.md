## Step 1 — Create Namespace

We begin by creating a dedicated namespace to isolate all HAProxy ingress components.

**YAML:** [manifests/01-namespace.yaml](manifests/01-namespace.yaml)

```bash
kubectl apply -f manifests/01-namespace.yaml
kubectl get ns
