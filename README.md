🌐 **Live Project:** https://projects.vikramc.com

# 🔐 Secure Self-Hosted Automation Platform (n8n + Cloudflare Zero Trust)

This project demonstrates how to securely expose a **locally hosted automation platform (n8n)** to the internet **without opening any inbound ports**, using **Cloudflare Tunnel and Zero Trust Access**.

The setup is designed to reflect **real-world DevSecOps and SaaS-style architecture**, not a simple lab deployment.

---

## 🧠 Problem Statement

Exposing internal tools to the internet usually requires:
- Public IPs
- Port forwarding
- Firewall changes

These approaches increase attack surface and operational risk.

---

## ✅ Solution Overview

This project uses:

- **Cloudflare Tunnel** to expose a local service securely
- **Cloudflare Zero Trust Access** for identity-based authentication
- **Dockerized n8n** with persistent storage
- **Selective webhook bypass** for machine-to-machine traffic

No inbound ports are opened on the host system.

---

## 🏗 Architecture

```mermaid
flowchart LR
    User[User Browser]
    External[External Services<br/>(GitHub, Jira, Slack)]
    CF[Cloudflare Edge]
    Access[Cloudflare Zero Trust<br/>Access (OTP)]
    Tunnel[Cloudflare Tunnel<br/>(cloudflared)]
    Host[Local Windows Host]
    Docker[Docker]
    N8N[n8n<br/>127.0.0.1:5678]

    User --> Access --> CF --> Tunnel --> Host --> Docker --> N8N
    External --> CF --> Tunnel --> Host --> Docker --> N8N
