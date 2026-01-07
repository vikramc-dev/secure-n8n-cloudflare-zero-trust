---
title: Secure n8n with Cloudflare Zero Trust
---

# 🔐 Secure Self-Hosted Automation Platform  
## n8n + Cloudflare Zero Trust

This site documents a secure, production-style setup to expose a **locally hosted n8n instance** to the internet **without opening inbound ports**, using:

- Cloudflare Tunnel
- Cloudflare Zero Trust Access (OTP)
- Dockerized n8n with persistent storage

---

## ✅ Solution Overview

- Cloudflare Tunnel to expose a local service securely  
- Identity-based access via Cloudflare Zero Trust  
- Webhook bypass for machine-to-machine traffic  
- No inbound ports exposed on the host  

---

## 🏗 Architecture

```mermaid
flowchart LR
    User["User Browser"]
    External["External Services\n(GitHub, Jira, Slack)"]
    CF["Cloudflare Edge"]
    Access["Cloudflare Zero Trust\nAccess (OTP)"]
    Tunnel["Cloudflare Tunnel\n(cloudflared)"]
    Host["Local Windows Host"]
    Docker["Docker"]
    N8N["n8n\n127.0.0.1:5678"]

    User --> Access --> CF --> Tunnel --> Host --> Docker --> N8N
    External --> CF --> Tunnel --> Host --> Docker --> N8N
