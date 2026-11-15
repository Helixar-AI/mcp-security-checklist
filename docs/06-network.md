# 🌐 Network & Infrastructure

**Audience:** Platform and infrastructure engineers
**Risk level if skipped:** High

---

## Why It Matters

An MCP server is a privileged execution layer. Its network posture determines what can reach it and what it can reach. Weak network controls mean a compromised agent — or any other caller who obtains a valid token — has access to everything the server can touch.

---

## Checklist

### Ingress (Incoming Traffic)

- [ ] **Do not expose MCP servers directly to the public internet** unless there is a specific, justified use case.
- [ ] **Place MCP servers behind a gateway or reverse proxy** that handles TLS termination, auth enforcement, and rate limiting.
- [ ] **Use TLS 1.2 minimum; prefer TLS 1.3** for all MCP traffic.
- [ ] **Use mTLS for server-to-server links when mutual certificate identity is required**. This is an added control, not a protocol requirement or a replacement for OAuth authorization on protected HTTP MCP requests.
- [ ] **Apply network-level allow-listing** for which source IPs or CIDR ranges can call the MCP server (where operationally feasible).
- [ ] **Segment MCP servers into their own network zone** — they should not share a subnet with general application infrastructure.

### Egress (Outgoing Traffic)

- [ ] **Apply egress filtering to MCP servers** — they should not be able to make arbitrary outbound connections.
- [ ] **Allow-list outbound destinations** that MCP tools legitimately need to reach.
- [ ] **Block outbound connections to metadata endpoints** (e.g., AWS/GCP/Azure IMDS) unless there is an explicit requirement.
- [ ] **Monitor outbound traffic volume and destinations** — unusual egress is a key indicator of exfiltration.
- [ ] **Do not allow MCP tools to resolve and connect to addresses supplied directly by agent inputs** without strict validation.

### Infrastructure Hardening

- [ ] **Run MCP server processes as a non-root, dedicated service account.**
- [ ] **Do not colocate MCP servers with sensitive data stores** on the same host or container unless there is a specific justification.
- [ ] **Apply container/VM hardening standards** (read-only filesystems where possible, no privileged containers).
- [ ] **Keep MCP server dependencies up to date** — supply chain vulnerabilities in libraries are a real risk.
- [ ] **Enable audit logging at the OS/container level** in addition to application-level logging.
- [ ] **Define and test an incident response runbook** for a compromised MCP server — know who does what and how fast.

---

## Quick Network Architecture Reference

```
[Agent Orchestrator]
        │
        ▼ (TLS / mTLS)
[Gateway / Reverse Proxy]  ← rate limiting, auth enforcement
        │
        ▼ (internal network only)
[MCP Server]  ← no public IP, egress-filtered
        │
        ▼ (allow-listed only)
[Downstream APIs / DBs]
```

---

## References

- [MCP Authorization (2026-07-28)](https://modelcontextprotocol.io/specification/2026-07-28/basic/authorization)
- [NIST SP 800-41 — Guidelines on Firewalls and Firewall Policy](https://csrc.nist.gov/publications/detail/sp/800-41/rev-1/final)
- [CIS Benchmarks for container and cloud hardening](https://www.cisecurity.org/cis-benchmarks)

---

*[← Monitoring](05-monitoring.md) | [Back to README](../README.md) | [Next: CISO Summary →](07-ciso-summary.md)*
