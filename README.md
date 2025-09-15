# The Stack-Driven Agentic Backlog Framework
*A 13‑step, AI‑native playbook to generate a complete, tailored software backlog — as code.*

> **License:** This repository is licensed under a **single license: Apache License 2.0**.  
> See the `LICENSE` file for the full text. All code, prompts, and documentation in this repo are covered by Apache‑2.0 unless a file explicitly states otherwise.

---

## Why this exists
ABF turns your delivery method into a **runnable, inspectable workflow**. Each of the 13 aspects of backlog delivery lives in its own directory with:
- Modular prompts (planner → researcher → synthesizer → critic)
- Example outputs and acceptance criteria
- Stack profiles and sub‑techstacks (e.g., DBMS variations)
- Minimal tests and CI hooks to keep results consistent

It’s designed for **human readers** and **AI agents** (ChatGPT, Claude, Gemini, etc.). Use it as a public showcase and a repeatable engine you tailor for each client.

---

## Table of Contents
- [What’s inside](#whats-inside)
- [Repository structure](#repository-structure)
- [The 13 aspects](#the-13-aspects)
- [Quickstart](#quickstart)
  - [Human mode (manual)](#human-mode-manual)
  - [Agent mode (orchestrated)](#agent-mode-orchestrated)
- [Client overlays & privacy](#client-overlays--privacy)
- [Contributing](#contributing)
- [Roadmap](#roadmap)
- [License](#license)
- [FAQ](#faq)

---

## What’s inside
- **aspects/** — 13 self‑contained modules; each has a spec, prompts, variants, and example outputs.
- **stacks/** — cross‑cutting stack profiles (e.g., `web-node-postgres-aws.yml`).
- **orchestration/** — optional runner configs (`workflow.yaml`, roles, budgets, evals).
- **templates/** — reusable templates (ADR, PR, Runbook, Issue).
- **examples/** — finished runs you can show to prospects.
- **.github/workflows/** — basic CI to lint specs and run tiny evals on PRs.
- **docs/** — optional Markdown docs site (if you wire up Docusaurus or similar).

---

## Repository structure

```
agentic-backlog-framework/
├─ README.md
├─ LICENSE
├─ docs/
├─ orchestration/
│  ├─ workflow.yaml
│  ├─ roles.yaml
│  ├─ budgets.yaml
│  ├─ eval.yaml
│  └─ tools/
├─ stacks/
│  ├─ web-node-postgres-aws.yml
│  ├─ web-python-django-azure.yml
│  └─ mobile-kotlin-firebase.yml
├─ examples/
│  ├─ b2b-saas-nextjs-postgres/
│  └─ fintech-api-go-gcp/
├─ templates/
│  ├─ ISSUE_TEMPLATE.md
│  ├─ PR_TEMPLATE.md
│  ├─ ADR_TEMPLATE.md
│  └─ RUNBOOK_TEMPLATE.md
├─ .github/workflows/
│  ├─ validate-aspects.yml
│  └─ build-docs.yml
└─ aspects/
   ├─ 01-core-design/
   │  ├─ aspect.yaml
   │  ├─ prompt/
   │  │  ├─ 00_planner.md
   │  │  ├─ 10_researcher.md
   │  │  ├─ 20_synthesizer.md
   │  │  └─ 90_critic.md
   │  ├─ stack-range.md
   │  ├─ variants/
   │  ├─ subtech/
   │  │  └─ dbms/
   │  │     ├─ postgres.md
   │  │     ├─ mysql.md
   │  │     └─ aurora.md
   │  ├─ example-output.md
   │  ├─ checklists/
   │  │  ├─ DoR.md
   │  │  └─ DoD.md
   │  ├─ tests/
   │  │  └─ golden.json
   │  └─ references/
   ├─ 02-style-guide/
   ├─ 03-user-journey/
   ├─ 04-backlog-organization/
   ├─ 05-technical-architecture/
   ├─ 06-dev-workflow/
   ├─ 07-project-management/
   ├─ 08-quality-governance/
   ├─ 09-maintenance-lifecycle/
   ├─ 10-measurement-analytics/
   ├─ 11-risk-compliance/
   ├─ 12-stakeholder-change/
   └─ 13-budget-resourcing/
```

> **Note:** This structure is intentionally language/tooling‑agnostic. You can drive it with any LLM or orchestrator.

---

## The 13 aspects
1. **Core Design Philosophy & Strategy** — vision, principles, personas/JTBD, outcomes, risks.  
2. **Style Guide** — tokens, components, interaction patterns, a11y, content style, i18n.  
3. **User Journey** — flows, scenarios, roles, empty/error states, analytics mapping.  
4. **Backlog Organization & Prioritization** — taxonomy, DoR, prioritization model, intake.  
5. **Technical Architecture & Constraints** — system/data diagrams, APIs, NFRs, security.  
6. **Development Workflow & Standards** — branching, code style, testing, CI/CD, flags.  
7. **Project Management & Collaboration** — ceremonies, RACI, workflow states, SLAs.  
8. **Quality & Governance** — DoD, QA, a11y, performance, observability, change control.  
9. **Maintenance & Lifecycle** — release/versioning, incidents, backups, cost, licensing.  
10. **Measurement & Analytics** — metric tree, OKRs, event spec, experiments, privacy.  
11. **Risk Management & Compliance** — risk register, threat model, regulatory mapping.  
12. **Stakeholder & Change Enablement** — comms plan, training, feedback loops, notes.  
13. **Budget & Resourcing** — team topology, hiring, vendors, infra/tooling budgets.  

Each aspect’s `aspect.yaml` defines **inputs**, **outputs**, **dependencies**, **acceptance criteria**, and allowed **tools**. Prompts are split into planner/researcher/synthesizer/critic roles for reliability.

---

## Quickstart

### Human mode (manual)
1. **Pick a stack profile** in `/stacks/*.yml` (or create one).  
2. **Start with Aspect 01** (`aspects/01-core-design/`).  
3. Open `prompt/00_planner.md` → follow the instructions to produce a plan.  
4. Move through `10_researcher.md` → `20_synthesizer.md` → `90_critic.md`.  
5. Compare your output to `acceptance_criteria` in `aspect.yaml` and the DoD checklist.  
6. Save the deliverable in `example-output.md` (or export to your client repo).  
7. Repeat for the next aspect, honoring declared dependencies.

### Agent mode (orchestrated)
- Use `orchestration/workflow.yaml` to run the 13 aspects in order with your preferred LLM/orchestrator.  
- Supply **inputs** (business context, stack profile, constraints).  
- Configure **budgets** and **evals** (`orchestration/*.yaml`).  
- Gate progress on each aspect’s **DoD**; fail‑fast if criteria aren’t met.

> Tip: Add a thin CLI (e.g., `scripts/abl.py`) with commands like `abl run 05` or `abl run all` to automate local runs.

---

## Client overlays & privacy
Keep this repo **public** as your method & lead magnet. For client work:
- Create a **private overlay repo** (client specifics, credentials, internal links).  
- Reference this framework as a Git submodule or pin to a release tag.  
- Never commit secrets. Prompts and tools warn against pasting sensitive data.

---

## Contributing
- PRs welcome for new **stack profiles**, **sub‑techstacks**, or **aspect variants**.  
- Please read `CONTRIBUTING.md` and `CODE_OF_CONDUCT.md` before submitting.  
- Add/update `tests/golden.json` when changing prompts to keep outputs stable.

---

## Roadmap
- More stack profiles (Rust/Actix, Rails/Postgres, JVM/Ktor, etc.).  
- Orchestrator adapters (LangGraph, OpenAI Assistants, CrewAI, custom CLI).  
- Built‑in diagram generation (Mermaid/PlantUML).  
- Stronger evals and red‑team prompts per aspect.  
- Interactive docs site with runnable snippets.

---

## License
**Apache License 2.0** — a single, permissive license that covers code **and** documentation, includes a patent grant, and requires preservation of notices. See `LICENSE` for details.

> If you prefer to keep client deliverables proprietary, generate them into a separate private repo and keep this framework open.

---

## FAQ

**Why one license?**  
Simplicity. Apache‑2.0 cleanly covers both code and docs, encourages adoption, and protects contributors with a patent grant.

**Can I use this commercially?**  
Yes. Apache‑2.0 allows commercial use. Keep the license and notice files intact.

**Do I need to attribute you?**  
Apache‑2.0 requires preservation of notices; attribution beyond that is appreciated but not required.

**How do I stop AI output drift?**  
Each aspect includes acceptance criteria, DoR/DoD checklists, and optional small “golden” tests. Changes to prompts should update the tests.

**What about trademarks and brand assets?**  
Any logos or trademarks are property of their respective owners and are **not** licensed by Apache‑2.0.

---

_Updated: 2025-09-15_
