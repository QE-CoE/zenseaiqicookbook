# Security

## Secret handling

- **All integration secrets** (LLM API keys, Jira tokens, Git PATs) are stored AES-256-GCM encrypted with the `v1:iv:tag:ct` envelope under the backend's `ENCRYPTION_KEY`.
- **Decryption is just-in-time** per-request; decrypted values live only in the request scope and are zeroed when the response is written.
- **API responses** expose only `apiKeyHint` masks (e.g. `sk-…7Hp2`) — never plaintext.
- **Browser** never receives a raw key for any provider. All LLM calls are server-side.

## Tenant isolation

- Every row in `pipeline_runs`, `agent_outputs`, `integrations`, `knowledge_base_chunks` is scoped to a `tenantId` column.
- Postgres row-level-security policies enforce isolation even if app-layer logic regressed.

## Auth

- JWT via `POST /api/auth/login` → token in `zenseai_api_token` localStorage key
- `BYPASS_AUTH=true` in dev accepts an empty token as the seeded admin user

## OWASP posture

| Top 10 | Mitigation |
|---|---|
| A01 Broken Access Control | RLS + JWT subject claim |
| A02 Cryptographic Failures | AES-256-GCM for secrets, TLS for transit |
| A03 Injection | Prisma parameterised queries throughout |
| A05 Security Misconfiguration | CSP headers, no default credentials |
| A07 Identification/Auth Failures | JWT short-lived, refresh rotated |
| A09 Logging/Monitoring | Structured logs with correlation IDs per pipeline run |

Self-audited; we also dogfood **Secure-Xi** against the platform.
