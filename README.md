# 🔐 MCP Security Checklist

> A practical, community-maintained security checklist for teams building and deploying **Model Context Protocol (MCP)** servers and AI agent infrastructure.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Maintained by Helixar](https://img.shields.io/badge/maintained%20by-Helixar-00C2B2)](https://helixar.ai)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen)](CONTRIBUTING.md)
[![GitHub Stars](https://img.shields.io/github/stars/helixar-ai/mcp-security-checklist?style=social)](https://github.com/helixar-ai/mcp-security-checklist)

---

## Why This Exists

MCP is being adopted rapidly. Security guidance is lagging behind.

This checklist gives security engineers, platform teams, and technical leaders a **clear, actionable baseline** for securing MCP deployments — whether you're shipping an internal tool or a customer-facing AI agent.

It is **not** vendor-specific, complete, or a replacement for a full security review. It is a starting point.

---

## 📋 The Checklists

| Checklist | Audience | Description |
|-----------|----------|-------------|
| [Authentication & Authorization](docs/01-auth.md) | All | Identity, token scope, and access control |
| [Input Validation & Prompt Injection](docs/02-input-validation.md) | Engineers | Sanitizing inputs before tool execution |
| [Tool & Resource Exposure](docs/03-tool-exposure.md) | Engineers / Architects | Limiting blast radius of MCP tools |
| [API Session Security](docs/04-api-session.md) | Platform Teams | Securing inbound sessions from agents |
| [Monitoring & Observability](docs/05-monitoring.md) | SecOps | What to log, alert on, and review |
| [Network & Infrastructure](docs/06-network.md) | Platform Teams | Network-layer hardening |
| [CISO Summary](docs/07-ciso-summary.md) | CISOs / Leadership | Non-technical risk summary |

---

## ✅ Quick-Start: Top 10 Controls

If you do nothing else, cover these:

1. **Protect remotely reachable MCP servers with HTTPS, caller authentication, and tool-level authorization.** Consider mTLS when you need mutual certificate identity.
2. **Scope every tool to the minimum necessary permissions.**
3. **Validate and sanitize all inputs before they reach tool execution.**
4. **Log every tool invocation with the originating session context.**
5. **Set rate limits on both the MCP server and any downstream APIs it calls.**
6. **Treat agent sessions as untrusted by default — validate intent, not just auth tokens.**
7. **Separate read and write tool categories; require explicit approval for write operations in sensitive contexts.**
8. **Rotate credentials used by MCP servers on a defined schedule.**
9. **Monitor for behavioral anomalies: unusual tool chains, high-frequency calls, off-hours access.**
10. **Conduct a tool inventory review before every production deployment.**

---

## 🗂️ Machine-Readable Version

A JSON and YAML version of the checklist is available for integration into CI/CD pipelines, compliance tooling, or custom dashboards:

- [`checklist.json`](checklist.json)
- [`checklist.yaml`](checklist.yaml)

---

## 🌐 GitHub Pages Site

Browse the checklist in a friendlier format at:
**[helixar-ai.github.io/mcp-security-checklist](https://helixar-ai.github.io/mcp-security-checklist)**

---

## 🤝 Contributing

This checklist improves through community input. If you've encountered a gap, misconfiguration, or attack pattern in real-world MCP deployments — we want to hear about it.

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to get involved.

---

## 📌 Scope & Limitations

This checklist covers:
- MCP server deployment and configuration security
- Inbound session and API request security
- Agent-to-tool interaction surface
- Operational monitoring and detection

This checklist **does not** cover:
- Model weights or training pipeline security
- End-user data privacy compliance (GDPR, CCPA, etc.)
- General cloud infrastructure hardening

---

## 🏷️ License

MIT. Use it freely. Attribution appreciated.

---

*Maintained by the [Helixar](https://helixar.ai) security research team.*
*Helixar builds AI-native endpoint and API security for agentic infrastructure.*
