# ACC v1.3 Production Handoff

## Source of truth

- Repository: `ohi-stack/acc`
- Branch: `main`
- Canonical host: `https://acc.onegodian.com`
- Oru’Valen route: `/oruvalen`
- OMOS route: `/omos`

## Required pre-deployment evidence

Before promoting a revision, verify that the exact candidate SHA has passed:

```bash
npm run check
npm run build
npm run test:smoke
npm run test:auth
npm run preflight:production
```

The production environment must supply protected values outside Git, including at minimum the remote PostgreSQL connection, API key, authorized operator identity/role, and explicit trusted CORS origin.

## Host runtime

The current application repository contains a PM2 runtime definition using:

- process name: `acc`
- entry point: `dist/index.js`
- production port: `4000`

Reverse-proxy and TLS configuration must terminate the public host at `acc.onegodian.com` and forward only to the intended ACC runtime.

## Post-deployment verification

Record non-secret evidence for the exact deployed SHA:

1. deployment timestamp in UTC;
2. deployed commit SHA;
3. runtime version (`1.3.0`);
4. `/health` response;
5. `/ready` response;
6. `/oruvalen` route resolution;
7. `/omos` route resolution;
8. production database classification without credentials;
9. authentication-contract status;
10. rollback target;
11. approving human/operator reference.

## Security rule

Never place passwords, API keys, SSH private keys, database credentials, WordPress Application Passwords, tokens, or other production secrets in this repository.

## Deployment status language

Use these states precisely:

- **Merged** — source code is in the canonical branch.
- **CI Verified** — repository tests and preflight passed.
- **Deployed** — the revision was promoted to the production host.
- **Production Verified** — the exact deployed revision passed live health, readiness, route, state-persistence, and deployment-evidence checks.

Do not call a revision Production merely because it was merged or because CI passed.
