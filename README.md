<h1 align="center">Johnny Endrihs</h1>
<h3 align="center">Building AI infrastructure from the runtime up</h3>

<p align="center">
  <a href="https://www.thehumble.dev">thehumble.dev</a> ·
  <a href="https://www.linkedin.com/in/johnnyendrihs">LinkedIn</a>
</p>

---

18 years from USMC to director-level security. Now building the agentic layer — not as an end user, but as the person writing the runtime.

My work sits at the intersection of AI systems and security architecture: designing the control surfaces, sandboxes, policy gates, and audit hooks that make autonomous agents safe to run in production. I don't bolt security on after the fact. It's a design constraint from commit one.

---

### Flagship

**[agnt](https://github.com/hmbldv/agnt)** — A production Rust agent runtime I designed and wrote from scratch. Seven crates: a zero-I/O kernel, multi-backend inference (OpenAI · Anthropic · Ollama · any OpenAI-compat), parallel tool dispatch via `thread::scope`, SQLite session persistence, and a NATS wire protocol for multi-agent routing. Security-forward by design: every filesystem tool routes through a `FilesystemRoot` sandbox that rejects path traversal at the type level; a `should_dispatch` observer gate fires before every tool call for HITL approval and policy enforcement; loop detection prevents adversarial prompts from spinning the agent in resource-exhausting cycles. Token tracking with `UsageStats` makes every inference step auditable. Running on a self-hosted 3-node Talos K8s cluster. 9/9 on a formal end-to-end eval including multi-turn coherence probes.

---

### Also Building

| Project | What It Is |
|---------|-----------|
| **[sia](https://github.com/hmbldv/sia)** | Self-improving agent loop in Rust. Give it a target artifact, an eval script, and a metric — it runs LLM-driven hypothesis-generate-evaluate cycles with git-native checkpointing and its own security guard layer (forbidden paths, secret detection, dangerous command rejection). |
| **[jc](https://github.com/hmbldv/jc)** | Jira + Confluence CLI built for AI consumption. JSON-first output, full markdown-to-ADF converter, dry-run-by-default mutations. Designed so an agent can read tickets, reason over them, execute changes, and update Jira — all without human hand-holding. |
| **[claude-sec](https://github.com/hmbldv/claude-sec)** | Enterprise security framework for Claude Code deployment. Approval gates, architecture guardrails, and governance controls for teams running AI coding assistants at scale. |
| **[syntor](https://github.com/hmbldv/syntor)** | Multi-agent orchestration system in Go. Kafka messaging, Redis registry, Jaeger tracing, Prometheus metrics. 34K lines. The earlier iteration of the orchestration work now evolved in agnt. |
| **[aws-sec](https://github.com/hmbldv/aws-sec)** | Multi-account AWS security foundation — credential-less CI/CD via OIDC, Terraform-managed controls, GitLab pipelines. Production-grade, not a demo. |

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
  <img src="https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white" />
  <img src="https://img.shields.io/badge/Vault-FFEC6E?style=flat-square&logo=vault&logoColor=black" />
</p>

---

<p align="center"><em>Security is a design constraint, not a feature.</em></p>
