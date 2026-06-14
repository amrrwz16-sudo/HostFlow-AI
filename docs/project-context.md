# HostFlow AI — Project Context

**Version:** 1.0
**Status:** Draft
**Phase:** Phase A — Architecture Design

---

## 1. Origin

Started as a Digital Product Generator for the Airbnb / short-term rental niche.

The initial goal was to produce digital products (Workbooks, Checklists, Templates, PDF Guides, DOCX Documents) as a revenue source, with the system operating through intelligent AI agents with minimal manual intervention.

---

## 2. Why the Direction Changed

During system design, a key question emerged:

> Build a system specialized for digital products only, or build a platform that can execute any type of project in the future?

The second option was chosen. A single-purpose system would require significant redesign with every expansion. A platform approach avoids that cost.

---

## 3. Current Direction

HostFlow AI is now a general-purpose multi-agent AI platform — not a single-purpose tool.

It functions as a virtual AI company operated by specialized agents under a central orchestrator.

**The first business implementation:** Digital product generation for the short-term rental niche.

---

## 4. Core Architecture Idea

Instead of one AI doing everything:

- Specialized agents handle specific responsibilities
- A central orchestrator manages routing and decisions
- A shared knowledge system improves output over time

**Agents remain fixed. Only context changes per project.**

What changes per project:
- Profile
- Prompt
- Knowledge
- Workflow

---

## 5. The Five Core Agents (Version 1)

| Agent | Responsibility |
|---|---|
| Orchestrator | Central decision maker — routes tasks, controls workflow |
| Research | Gathers and synthesizes market knowledge |
| Builder | Designs product structure and outline |
| Creator | Generates the actual output content |
| Reviewer | Validates quality and flags issues |

> Note: Version 1 uses five agents. Additional agents may be introduced in future versions if architecturally justified.

---

## 6. Design Philosophy

- Hermes is not the project
- n8n is not the project
- OpenRouter is not the project

These are implementation tools. They can be replaced without changing the platform architecture.

**HostFlow AI is the project.**

---

## 7. Expansion Model

When adding a new domain in the future:

- No changes to core agents
- No changes to core architecture
- Create a new Profile + Prompt + Knowledge + Workflow

The platform scales through configuration, not redesign.

---

## 8. MVP Scope

Version 1 focuses exclusively on:

- Digital product generation for the short-term rental niche
- Validate the platform before expanding to additional domains

---

## 9. Current Phase

**Phase A — Architecture Design**

No code is being written. No workflows are being built.

Current focus: completing the architectural design before implementation begins.
