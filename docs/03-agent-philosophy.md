# HostFlow AI — Agent Philosophy

**Version:** 1.1
**Status:** Draft
**Phase:** Phase A — Architecture Design

> ⚠️ Update from v1.0: The system now uses 4 core agents + Review Layer (not 5 agents). The Reviewer Agent has been replaced by a Review Layer — a lightweight quality control system managed by the Orchestrator.

---

## 1. Core Concept

HostFlow AI uses a fixed set of specialized agents. Agents do not change when the project domain changes.

**What changes per project:**
- Profile
- Prompt
- Knowledge
- Workflow

**What stays the same:**
- Agent identities
- Agent responsibilities
- Core architecture

---

## 2. Why Fixed Agents?

Building a new agent for every project type would require:
- Redesigning the system for every new domain
- Duplicating logic across agents
- Increasing maintenance cost over time

Fixed agents with contextual configuration avoids all of these problems.

---

## 3. The Four Core Agents (Version 1)

### Orchestrator Agent
**Role:** Central decision maker and system manager

- Routes tasks to the correct agent
- Selects appropriate model per task
- Controls workflow sequence
- Handles errors and retries
- Manages the Review Layer decisions

---

### Research Agent
**Role:** Knowledge gatherer

- Researches market, niche, or domain
- Synthesizes findings into structured knowledge
- Feeds knowledge to Builder agent

---

### Builder Agent
**Role:** Structure designer

- Designs product or project structure
- Creates outlines and frameworks
- Defines what the Creator will produce

---

### Creator Agent
**Role:** Output generator

- Generates the actual content or product
- Follows structure defined by Builder
- Produces PDF, DOCX, Markdown, or other formats
- All outputs go to Review Layer before final delivery

---

## 4. Review Layer (Quality System)

The Review Layer is not an agent. It is a quality control layer built into the workflow.

**What it does:**
- Validates every output before it moves to the next stage
- Issues Approve / Reject / Revision Required decisions
- Sends feedback back through the Orchestrator

**Why a layer and not an agent:**
- Lighter and simpler
- Avoids unnecessary complexity
- Keeps the agent count minimal
- Easier to maintain and expand

---

## 5. How Context Changes Agent Behavior

The same agent can serve completely different domains without any changes to the agent itself.

**Example — Research Agent:**
- Today: researches short-term rental products for Airbnb hosts
- Tomorrow: researches SaaS market opportunities
- Next year: researches mobile application trends

The agent did not change. The Profile, Prompt, and Knowledge changed.

---

## 6. Expansion Rule

New agents will only be introduced when:
1. A new responsibility cannot be covered by existing agents
2. There is a strong architectural justification
3. The new agent follows the same fixed-role philosophy

Examples of potential future agents: Security Agent, Deployment Agent, Analytics Agent.

---

## 7. Relationship to Other Documents

- **Architecture Layers** — defines where agents live (Intelligence Layer)
- **Agent Roles** — defines the detailed responsibilities, inputs, and outputs of each agent
- **Profile System** — defines how agent behavior changes per domain
