# 🔑 Authentication & Authorization

**Audience:** All teams deploying MCP servers
**Risk level if skipped:** Critical

---

## Why It Matters

MCP servers execute tools on behalf of AI agents. Without strong authentication and authorization, any caller — legitimate or malicious — can invoke those tools. This is the single highest-risk surface in an MCP deployment.

---

## Checklist

### Authentication

- [ ] **Require authentication on all MCP endpoints** — no unauthenticated tool invocation, ever.
- [ ] **Use short-lived tokens** — API keys and session tokens should expire. Long-lived static keys are a liability.
- [ ] **Consider mTLS for server-to-server connections that need mutual certificate identity**. This adds transport-level identity checks but does not replace endpoint authorization.
- [ ] **Do not embed credentials in agent prompts or tool descriptions** — agents can leak these in responses.
- [ ] **Rotate credentials on a defined schedule** — and immediately on any suspected compromise.
- [ ] **Use a secrets manager** (e.g., Vault, AWS Secrets Manager) rather than environment variables for MCP server credentials.

### Authorization

- [ ] **Apply least-privilege scoping to every tool** — a tool that reads files should not have write permissions.
- [ ] **Separate read-only and write/execute tools** — require explicit elevated authorization for destructive or sensitive tools.
- [ ] **Enforce per-agent identity** — do not allow a shared credential to act on behalf of multiple agents if individual traceability matters.
- [ ] **Validate that the calling agent is authorized for the specific tool being invoked**, not just authenticated to the server.
- [ ] **Restrict which tools are visible to which agents** — tool discovery itself is an attack surface.
- [ ] **Audit authorization rules before every production deployment** — tools added during development often carry over-permissive access.

---

## Common Mistakes

| Mistake | Risk |
|--------|------|
| Single shared API key for all agents | Compromise of one agent exposes all |
| Tools scoped to server-level permissions | One tool invocation can escalate to full server access |
| No expiry on session tokens | Stolen tokens are valid indefinitely |
| Auth checks only at the gateway, not the tool layer | Bypass via direct MCP calls |

---

## References

- [OWASP API Security Top 10](https://owasp.org/www-project-api-security/)
- [MCP Authorization (2026-07-28)](https://modelcontextprotocol.io/specification/2026-07-28/basic/authorization)
- [NIST SP 800-63B — Digital Identity Guidelines](https://pages.nist.gov/800-63-3/sp800-63b.html)

---

*[← Back to README](../README.md) | [Next: Input Validation →](02-input-validation.md)*
