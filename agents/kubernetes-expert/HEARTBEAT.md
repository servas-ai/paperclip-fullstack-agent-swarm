# HEARTBEAT.md — Kubernetes Expert

## 1. Identity + Setup
- `GET /api/agents/me`
- Read `../SHARED_CONFIG.md`, `../../MEMORY.md`
- `kubectl cluster-info` · `kubectl get nodes` · `helm list -A`

## 2. Helm Chart
```
helm/[app]/
├── Chart.yaml · values.yaml · values-staging.yaml · values-prod.yaml
└── templates/
    ├── deployment.yaml · service.yaml · ingress.yaml
    ├── configmap.yaml · hpa.yaml · networkpolicy.yaml
```

## 3. Pre-Deploy Checklist
- [ ] `helm template` renders cleanly · Image version pinned (no `latest`)
- [ ] Resource requests + limits set · Health probes configured
- [ ] Secrets from K8s Secrets (not hardcoded) · Network policies defined
- [ ] HPA configured with thresholds

## 4. Health Probes
- Readiness: `/api/health` 200 → receives traffic
- Liveness: `/api/health` 200 → stays alive
- Startup: grace period for slow-starting apps

## 5. Resources
```yaml
requests: { cpu: "250m", memory: "256Mi" }
limits: { cpu: "500m", memory: "512Mi" }
```
- HPA: minReplicas 2, maxReplicas 10, cpu target 70%

## 6. Pre-Delivery
- [ ] Pods start + pass probes · Service/Ingress accessible · TLS configured
- [ ] HPA responds to load · Network policies active · SYSTEM_STATE.md updated

## Rules
- NEVER `latest` tag · ALWAYS requests + limits · ALWAYS health probes
- `helm template` before `helm install` · Namespace isolation mandatory
