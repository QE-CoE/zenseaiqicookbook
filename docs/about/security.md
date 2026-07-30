# Security

## Secret handling

- **All integration secrets** (LLM API keys, Jira tokens, Git PATs, qTest credentials) are stored AES-256-GCM encrypted with the `v1:iv:tag:ct` envelope under the backend's `ENCRYPTION_KEY`.
- **Decryption is just-in-time** per-request; decrypted values live only in the request scope and are zeroed when the response is written.
- **API responses** expose only `apiKeyHint` masks (e.g. `sk-…7Hp2`) — never plaintext.
- **Browser** never receives a raw key for any provider. All LLM calls are server-side.
- **Source-integration tokens are resolved server-side.** The browser holds no integration credentials, and legacy values were purged from `localStorage` in June 2026.

## Tenant isolation

- Every row in `pipeline_runs`, `agent_outputs`, `integrations`, `knowledge_base_chunks` is scoped to a `tenantId` column.
- Postgres row-level-security policies enforce isolation even if app-layer logic regressed.

## Auth

- JWT via `POST /api/auth/login` → token in `zenseai_api_token` localStorage key
- Access tokens are valid for 3 hours, with silent refresh so long-running agent work does not expire mid-run
- `install.sh` generates a random `DEFAULT_ADMIN_PASSWORD` per install — there are no shipped default credentials
- `BYPASS_AUTH=true` in dev accepts an empty token as the seeded admin user. It is **silently ignored when `NODE_ENV=production`**, so a stray flag cannot disable auth on a live deployment.
- **Internal service token** authenticates backend-to-agent calls, and self-heals on existing deployments

## Transport and request hardening

- **Helmet** security headers with a tightened Content-Security-Policy
- **CSRF protection** on state-changing routes
- **SSRF guards** on outbound calls to user-supplied URLs
- **TLS verification** enforced on outbound integration calls
- **Rate limiting**, with correct client identification behind a loopback proxy
- **Safe download headers** on proxied file responses
- **Scoped request body limits** — the agent proxy routes accept larger payloads, everything else does not

## OWASP posture

| Top 10 | Mitigation |
|---|---|
| A01 Broken Access Control | RLS + JWT subject claim + internal service token |
| A02 Cryptographic Failures | AES-256-GCM for secrets, TLS for transit and outbound calls |
| A03 Injection | Prisma parameterised queries throughout |
| A05 Security Misconfiguration | Helmet + CSP headers, no default credentials, prod-safe auth bypass |
| A07 Identification/Auth Failures | Short-lived JWT with rotated refresh, rate-limited auth routes |
| A08 Software & Data Integrity | Dependency audit in CI, pull-request gate on the development branch |
| A09 Logging/Monitoring | Structured logs with correlation IDs per pipeline run |
| A10 Server-Side Request Forgery | SSRF guards on user-supplied URL handling |

## Assessment history

- **July 2026** — VAPT assessment findings closed, plus a follow-up review covering the backend-for-frontend image route and TLS verification.
- **June 2026** — External security audit findings closed across P0, P1 and P2 severities.

Self-audited on an ongoing basis; we also dogfood **[Secure-Xi](../agents/secure-xi.md)** against the platform.
