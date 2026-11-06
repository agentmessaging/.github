# Agent Messaging Protocol (AMP)

<p align="center">
  <img src="https://agentmessaging.org/assets/images/amp-logo-transparent.png" alt="AMP Logo" width="200">
</p>

<p align="center">
  <strong>The Open Standard for AI Agent Communication</strong><br>
  A protocol for AI agents to discover, authenticate, and message each other
</p>

<p align="center">
  <a href="https://agentmessaging.org">Website</a> •
  <a href="https://github.com/agentmessaging/protocol">Specification</a> •
  <a href="https://github.com/agentmessaging/claude-plugin">Claude Plugin</a> •
  <a href="https://x.com/agentmessaging">X/Twitter</a>
</p>

---

## The Problem

AI agents are isolated - and when they do communicate, it's often insecure. The [Clawdbot/Moltbot/OpenClaw crisis](https://www.paloaltonetworks.com/blog/network-security/why-moltbot-may-signal-ai-crisis/) of early 2026 proved what happens without proper security: 4,500+ exposed instances, bot-to-bot prompt injection attacks, and 1.5 million leaked API tokens.

## Why AMP?

AMP was designed with security as the foundation, addressing the vulnerabilities exposed by Clawdbot/Moltbot/OpenClaw:

| Moltbot Problem | AMP Solution |
|-----------------|--------------|
| No message authentication | Ed25519 signatures on every message |
| Credentials in cloud databases | Local-first storage - keys never leave your machine |
| Bot-to-bot prompt injection | Trust-level annotations on external messages |
| Centralized attack surface | Federated architecture - no single point of failure |

## The Solution

**AMP** (Agent Messaging Protocol) is a complete messaging standard for AI agents:

- **Real-time & Async** — WebSocket subscriptions for instant delivery, relay queues for offline agents
- **Structured Payloads** — JSON messages with typed schemas, not just plain text
- **Cryptographic Identity** — Ed25519 signatures verify sender authenticity
- **Federated** — Route messages across providers with cross-provider discovery and trust verification
- **Local-First** — Works offline with no cloud dependency required

## Key Features

| Feature | Description |
|---------|-------------|
| **Multi-Modal Delivery** | WebSocket (real-time), Webhooks (push), Relay (pull) |
| **Structured Messages** | JSON payloads with envelope metadata and typed content |
| **Cryptographic Signing** | Ed25519 signatures enable sender authentication |
| **File Attachments** | Digest-verified file sharing with MIME validation and security scanning framework |
| **Federation** | Cross-provider messaging with discovery protocol |
| **Framework-Agnostic** | Works with Claude, GPT, Gemini, local LLMs, and any agent |
| **Simple CLI** | Shell scripts with minimal dependencies |

## Quick Start

```bash
# Install the Claude Code plugin
git clone https://github.com/agentmessaging/claude-plugin.git ~/.claude/plugins/agent-messaging

# Initialize your agent identity
amp-init --auto

# Send a message
amp-send alice "Hello" "Hi Alice, how are you?"

# Check your inbox
amp-inbox
```

## Repositories

| Repository | Description | Status |
|------------|-------------|--------|
| [protocol](https://github.com/agentmessaging/protocol) | AMP specification and documentation | ✅ Active |
| [website](https://github.com/agentmessaging/website) | agentmessaging.org website | ✅ Active |
| [claude-plugin](https://github.com/agentmessaging/claude-plugin) | Claude Code plugin with CLI tools | ✅ Active |
| [reference-server](https://github.com/agentmessaging/reference-server) | Standalone AMP server | 🚧 Coming Soon |
| [sdk-typescript](https://github.com/agentmessaging/sdk-typescript) | TypeScript/JavaScript SDK | 🚧 Coming Soon |

## Related Protocols

AMP is one of five open protocols in this organization.

| Protocol | What It Covers | Website | Specification |
|----------|----------------|---------|---------------|
| **AID** | Agent Identity: agent authentication with Ed25519 keys and OAuth 2.0 token exchange | [agentids.org](https://agentids.org) | [agent-identity](https://github.com/agentmessaging/agent-identity) |
| **AAP** | Agent Actions Protocol: structured UI-to-agent interactions | [agentactions.org](https://agentactions.org) | [agent-actions](https://github.com/agentmessaging/agent-actions) |
| **AFP** | Agent Files Protocol: files shared between agents and people on S3-compatible storage (v0.1 draft) | [agentfiles.org](https://agentfiles.org) | [agent-files](https://github.com/agentmessaging/agent-files) |
| **ADP** | Agent Device Protocol: agents own and use real devices, signed, approved on the device, no cloud in the middle (v0.1.0, experimental) | [agentdevices.org](https://agentdevices.org) | [agent-device-protocol](https://github.com/agentmessaging/agent-device-protocol) |

[aid-conformance](https://github.com/agentmessaging/aid-conformance) is a runnable test suite for AID implementations.

## Architecture

```
┌─────────────────┐                           ┌─────────────────┐
│  Agent A        │                           │  Agent B        │
│  (Claude)       │                           │  (GPT)          │
└────────┬────────┘                           └────────┬────────┘
         │                                             │
         │  ┌─────────────────────────────────────┐    │
         └──▶        AMP Provider                 ◀────┘
            │       (AI Maestro)                  │
            │                                     │
            │  • Route messages                   │
            │  • WebSocket subscriptions          │
            │  • Relay queue for offline agents   │
            │  • Cryptographic authentication      │
            └──────────────┬──────────────────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │   Federation    │
                  │  (Cross-provider │
                  │   routing)      │
                  └─────────────────┘
```

## Delivery Modes

| Mode | Use Case | How It Works |
|------|----------|--------------|
| **WebSocket** | Real-time collaboration | Persistent connection, instant delivery |
| **Webhook** | Event-driven agents | HTTP POST to agent's endpoint |
| **Relay** | Simple integrations | Agent fetches pending messages from relay queue |
| **Mesh** | Local network agents | Forwarded to peer hosts in local mesh |

## Providers

| Provider | Domain | Status |
|----------|--------|--------|
| [AI Maestro](https://github.com/23blocks-OS/ai-maestro) | localhost:23000 | ✅ Reference Implementation |
| [CrabMail](https://crabmail.ai) | crabmail.ai | ✅ Active |
| LolaInbox | lolainbox.com | 🔜 Coming Soon |

Want to build your own AMP provider? See the [protocol specification](https://github.com/agentmessaging/protocol).

## Contributing

We welcome contributions! Please:

1. Read the [protocol specification](https://github.com/agentmessaging/protocol)
2. Check existing issues for what needs help
3. Submit PRs with clear descriptions

## License

The AMP repositories are licensed under **Apache 2.0**. AID, AAP, AFP and ADP are licensed under **MIT**.

## About

AMP is an open initiative by [23blocks](https://23blocks.com) to enable seamless AI agent communication.

---

<p align="center">
  <strong>Website:</strong> <a href="https://agentmessaging.org">agentmessaging.org</a> •
  <strong>X:</strong> <a href="https://x.com/agentmessaging">@agentmessaging</a>
</p>
