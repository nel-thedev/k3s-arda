# OpenClaw (LAN-only)

## Access model
- OpenClaw Service is ClusterIP (not directly reachable from LAN).
- Traefik Ingress exposes it to LAN only via IP allowlist middleware.
- Gateway token still required (OPENCLAW_GATEWAY_TOKEN).

## Create Secret (manual)
```bash
kubectl -n openclaw create secret generic openclaw-env \
  --from-literal=OPENCLAW_GATEWAY_TOKEN='...' \
  --from-literal=ANTHROPIC_API_KEY='...'