# HostFlow AI — Communication Protocol

**Version:** 1.0
**Status:** Draft
**Phase:** Phase A — Architecture Design

---

## 1. Purpose

Defines how agents communicate inside HostFlow AI to ensure:

- Structured communication
- Predictable execution
- No chaotic agent interaction
- Full traceability of decisions

---

## 2. Core Principle

All communication is structured, hierarchical, and routed through the Orchestrator.

No agent communicates directly with another agent outside the defined routing rules.

---

## 3. Communication Flow

```
User Request
   ↓
Orchestrator
   ↓
Agents (Research / Builder / Creator)
   ↓
Review Layer
   ↓
Orchestrator (Final Decision)
   ↓
User
```

---

## 4. Message Format

All internal messages must follow this structure:

```json
{
  "from": "agent_name",
  "to": "agent_name",
  "type": "task | result | request | feedback",
  "content": "message body",
  "context": {
    "project_id": "",
    "stage": "",
    "priority": "low | medium | high"
  }
}
```

---

## 5. Message Types

| Type | Description |
|---|---|
| task | Orchestrator assigns work to an agent |
| result | Agent returns output to Orchestrator |
| feedback | Review Layer sends validation result |
| request | Agent requests additional context or resources |

---

## 6. Communication Rules

- All requests must pass through Orchestrator
- No direct agent-to-agent communication
- Every message must include context metadata
- Review Layer validates all final outputs before completion
- All messages are logged for traceability

---

## 7. Exception Rule

Review Layer may send feedback directly to Creator Agent during revision cycles. All other routing goes through Orchestrator.

---

## 8. Future Extensions

- Async message queue
- Priority-based routing
- Real-time execution monitoring
