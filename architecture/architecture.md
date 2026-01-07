# 🏗 Architecture Diagram

The following diagram represents the secure architecture used to expose a locally hosted n8n instance using Cloudflare Zero Trust and Cloudflare Tunnel.

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
