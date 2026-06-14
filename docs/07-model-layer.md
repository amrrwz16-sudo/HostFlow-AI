# HostFlow AI — Model Layer

**Version:** 1.0
**Status:** Draft
**Phase:** Phase A — Architecture Design

---

## 1. Purpose

Defines how AI models are selected and used across the system.

---

## 2. Core Principle

One system, multiple models — selected dynamically based on task type.

Models are not fixed per agent. Agents use models dynamically depending on task context and complexity.

---

## 3. Model Categories

### Fast Model
- Quick responses
- Routing decisions
- Simple classification
- Low cost

### Reasoning Model
- Planning and logic breakdown
- Orchestration decisions
- Complex problem decomposition
- Used by: Orchestrator, Review Layer

### Research Model
- Analysis of large information sets
- Synthesis and summarization
- Used by: Research Agent

### Builder Role Model
> Note: Not a separate model type. Builder Agent uses a Reasoning Model with a specialized Builder Prompt Profile.

- System design reasoning
- Architecture planning
- Workflow structuring

### Creator Model
- Final output generation
- Content creation and formatting
- Used by: Creator Agent

---

## 4. Model Router

The Orchestrator contains a Model Router responsible for:

- Selecting the appropriate model per task
- Optimizing between speed and quality
- Reducing cost by using Fast Models when sufficient
- Escalating to Reasoning Models when needed

**Selection criteria:**
- Task complexity
- Agent type
- Execution stage
- Available budget

---

## 5. Model Assignment (Default)

| Agent | Default Model Type |
|---|---|
| Orchestrator | Reasoning Model |
| Research Agent | Research Model |
| Builder Agent | Reasoning Model + Builder Prompt |
| Creator Agent | Creator Model |
| Review Layer | Reasoning Model / Fast Model |

---

## 6. Key Rules

- No agent is permanently bound to one model
- Orchestrator decides model selection at task initialization
- Models can be swapped without changing agent architecture
- The platform is provider-agnostic (OpenRouter, direct APIs, etc.)

---

## 7. Future Extensions

- Adaptive model selection engine
- Cost optimization layer
- Performance scoring per model
- Automatic fallback when a model is unavailable
