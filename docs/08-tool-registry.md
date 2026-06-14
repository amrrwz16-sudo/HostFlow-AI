# HostFlow AI — Tool Registry

**Version:** 1.0
**Status:** Draft
**Phase:** Phase A — Architecture Design

---

## 1. Purpose

Defines all tools available in HostFlow AI and controls agent access permissions.

---

## 2. Core Principle

Tools are permissions, not freedom.

Every agent has a defined set of allowed tools. Any tool not listed in an agent's allowed set is forbidden.

---

## 3. Tool Categories

### Information Tools
- Web Search
- Document Reader
- Knowledge Base Access

### Reasoning Tools
- Model Router
- Planning Engine
- Decision Engine

### Creation Tools
- File Generator (PDF / DOCX / MD / JSON)
- Template Engine
- Formatter

### Memory Tools
- Save Memory
- Retrieve Memory
- Update Memory

### System Tools
- Logging System
- Workflow Engine
- Task Tracker

---

## 4. Tool Access per Agent

### Orchestrator Agent
**Allowed:**
- Model Router
- Workflow Engine
- Memory System (full access)
- Logging System
- Task Tracker

**Forbidden:**
- File Generation
- Web Search (direct)

---

### Research Agent
**Allowed:**
- Web Search
- Document Reader
- Knowledge Base (read + write)
- Save Memory (limited)

**Forbidden:**
- File Generation
- Decision Engine
- Workflow Engine

---

### Builder Agent
**Allowed:**
- Knowledge Base (read)
- Template Engine
- Architecture Tools
- Planning Engine

**Forbidden:**
- Web Search
- File Generation (final outputs)
- Save Memory (direct)

---

### Creator Agent
**Allowed:**
- File Generator (PDF / DOCX / MD / JSON)
- Template Engine
- Formatter

**Forbidden:**
- Web Search
- Decision Engine
- Memory Write

---

### Review Layer
**Allowed:**
- Logging System (read only)
- Memory Access (read only)
- Validation Engine

**Forbidden:**
- Content creation
- File generation
- Memory write

---

## 5. Execution Rules

- Tools are assigned at task initialization by Orchestrator
- After assignment, agents execute tools directly within allowed scope
- No re-routing required per individual tool action
- Any tool not listed in the Registry is forbidden by default

---

## 6. Future Extensions

- External APIs (Notion, Stripe, GitHub)
- Plugin system for custom tools
- Per-project tool configuration
- Tool usage analytics
