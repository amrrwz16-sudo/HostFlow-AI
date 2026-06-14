# HostFlow AI — Memory System

**Version:** 1.0
**Status:** Draft
**Phase:** Phase A — Architecture Design

---

## 1. Purpose

Stores and manages system knowledge across projects and agents to enable continuous improvement and knowledge reuse.

---

## 2. Core Principle

Selective memory, not full logging.

The system stores only valuable, reusable knowledge. Raw execution logs are handled separately by the Logging System.

---

## 3. Memory Types

### Project Memory
Stores per-project information:
- Project goals and constraints
- Execution progress
- Agent outputs
- Decisions made during execution

**Scope:** Per project. Cleared or archived when project completes.

---

### Knowledge Base (Global Memory)
Stores reusable knowledge across all projects:
- Research insights
- Successful patterns
- Domain knowledge
- Reusable templates and structures

**Scope:** Global. Persists across all projects.

---

> **MVP Decision (v1.0):** Agent Memory is merged into Project Memory in this version. It will be separated into its own memory type in a future version when the need arises.

---

## 4. Memory Operations

### Save
Triggered when:
- A valuable insight is produced by Research Agent
- A reusable pattern is identified
- A key decision is made by Orchestrator

### Retrieve
Triggered when:
- A new project starts (load relevant context)
- An agent needs prior knowledge for a similar task
- Orchestrator checks for existing work before assigning research

### Update
Triggered when:
- Existing knowledge becomes outdated
- A better pattern or insight replaces an old one

---

## 5. Memory Rules

- No raw execution data is stored in Memory System (use Logging System instead)
- Only knowledge with reuse value is saved
- Orchestrator decides what gets saved — agents do not save independently
- Every memory entry must include source, type, and timestamp

---

## 6. Memory Structure

```json
{
  "memory_id": "unique_id",
  "type": "project | knowledge",
  "content": "insight or structured data",
  "source": "agent_name",
  "project_id": "optional",
  "timestamp": "ISO_DATE",
  "tags": ["topic", "domain", "type"]
}
```

---

## 7. Memory Flow

```
Agent Execution
   ↓
Output Generated
   ↓
Orchestrator Evaluates (Save / Ignore)
   ↓
Memory System (if Save)
```

---

## 8. Future Extensions

- Vector database for semantic memory search
- Cross-project learning engine
- Automatic memory scoring (relevance decay over time)
- Self-improving memory prioritization
