<h1 align="center">Johnny Endrihs</h1>
<h3 align="center">Building the agentic mesh — runtime · memory · voice · tools</h3>

<p align="center">
  <a href="https://www.thehumble.dev">thehumble.dev</a> ·
  <a href="https://www.linkedin.com/in/johnnyendrihs">LinkedIn</a>
</p>

---

18 years from USMC to director-level security. Now building the infrastructure that agentic AI runs on — not as an end user, but as the person writing the runtime, the memory system, and the wire protocol.

My work is a self-hosted mesh of composable systems: each piece is independently useful, but together they form a fully autonomous, voice-controlled, memory-persistent agent environment running entirely on local hardware. Security is a design constraint from the first commit — sandboxes, policy gates, audit hooks, and loop detection are not features, they are architecture.

I build microservices based architecture that maps cleanly to cloud environments with infrastructure that can be dictated for policy as code.

---

### The Mesh

The flagship is not a single repo — it's a suite of systems that compose:

| Layer | What It Does |
|-------|-------------|
| **[agnt](https://github.com/hmbldv/agnt)** — Agent Runtime | Production Rust engine. Zero-I/O kernel, multi-backend inference (OpenAI · Anthropic · Ollama), parallel tool dispatch, NATS wire protocol, SQLite persistence. Security: `FilesystemRoot` sandbox (path traversal rejected at the type level), `should_dispatch` policy gate for HITL approval, loop detection via `(tool_name, args)` fingerprinting, per-step token audit. 7 crates. 9/9 on formal end-to-end eval. |
| **voicectl** — Voice Layer | Always-on voice pipeline. Silero VAD, faster-whisper-large-v3 STT, Kokoro TTS — all self-hosted, no cloud. Transcripts dispatch to named agents over NATS. Treated as an adversarial input surface: sandboxed at dispatch. |
| **memctl** — Memory System | FSRS-6 spaced-repetition memory with session search, auto-ingest, and decay scoring. Agents recall prior decisions, corrections, and context without ballooning prompt size. |
| **vlt** — Secrets Manager | Hardware-bound secrets manager. Tiered KEK hierarchy: Argon2id (passphrase) → YubiKey HMAC-SHA1 → FIDO2 hmac-secret. AES-256-GCM encryption, append-only HMAC-chained audit log, caller registration with binary hash verification. The credential layer the mesh trusts. |

These run on a self-hosted 3-node Talos K8s cluster with HashiCorp Vault HA for secrets and NATS for messaging.

---

### Also Building

| Project | What It Is |
|---------|-----------|
| **[sia](https://github.com/hmbldv/sia)** | Self-improving agent loop in Rust. Give it a target artifact, an eval script, and a metric — it runs LLM-driven hypothesis-generate-evaluate cycles with git-native checkpointing. Built-in security guards: forbidden path enforcement, secret pattern detection, dangerous command rejection. |
| **[jc](https://github.com/hmbldv/jc)** | Jira + Confluence CLI built for AI consumption. JSON-first output, full markdown-to-ADF converter, dry-run mutations. An agent reads tickets, reasons over them, executes changes, and updates Jira — no human in the loop. |
| **[claude-sec](https://github.com/hmbldv/claude-sec)** | Enterprise security framework for Claude Code. Approval gates, architecture guardrails, governance controls for teams running AI coding assistants at scale. |
| **[aws-sec](https://github.com/hmbldv/aws-sec)** | Multi-account AWS security foundation — credential-less CI/CD via OIDC, Terraform-managed controls, GitLab pipelines. Production-grade. |

---

### Stack

<p>
  <img src="https://img.shields.io/badge/Rust-000000?style=flat-square&logo=rust&logoColor=white" />
  <img src="https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white" />
  <img src="https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white" />
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" />
</p>
<p>
  <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white" />
  <img src="https://img.shields.io/badge/AWS-FF9900?style=flat-square&logo=amazonaws&logoColor=white" />
  <img src="https://img.shields.io/badge/NATS-27AAE1?style=flat-square&logo=natsdotio&logoColor=white" />
  <img src="https://img.shields.io/badge/Vault-FFEC6E?style=flat-square&logo=vault&logoColor=black" />
  <img src="https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white" />
</p>

---

<p align="center"><em>Security is a design constraint, not a feature.</em></p>