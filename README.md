# ACC Infra

Infrastructure and production-deployment control repository for the OneGodian Agent Command Console / control plane.

## Canonical production target

- Application repository: `ohi-stack/acc`
- Current application baseline: `ACC v1.3.0`
- Canonical host: `https://acc.onegodian.com`
- Oru’Valen™ console: `https://acc.onegodian.com/oruvalen`
- OMOS™ console: `https://acc.onegodian.com/omos`
- External OMOS node: `https://omos.onegodian.com`

## Runtime contract

The current ACC application repository defines:

- Node 20+ runtime within the supported application range;
- compiled Express/TypeScript runtime at `dist/index.js`;
- React production bundle under `public/`;
- PM2 process name `acc`;
- production application port `4000` in the checked-in PM2 configuration;
- remote PostgreSQL requirement for production;
- explicit production API authentication;
- explicit trusted CORS origin;
- health and readiness endpoints;
- production preflight checks.

## Authority boundary

Infrastructure promotes an approved application revision; it does not create product or governance authority.

```text
Authorized revision
→ production build
→ production preflight
→ deployment
→ /health verification
→ /ready verification
→ /oruvalen verification
→ /omos verification
→ deployment evidence record
```

A Git merge is not deployment proof.

## Current infrastructure status

This repository currently documents the deployment boundary but does not contain production credentials or a verified automated host-deployment workflow. Secrets must remain in the deployment platform or approved secret store, never in this repository.

See `docs/ACC-V1.3-PRODUCTION-HANDOFF.md` for the deployment-proof requirements and host handoff contract.
