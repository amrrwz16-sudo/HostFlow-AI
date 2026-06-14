# HostFlow AI — Agent Roles

**Version:** 1.0
**Status:** Draft
**Phase:** Phase A — Architecture Design

---

## 1. Purpose

This document defines the official roles of all agents inside the HostFlow AI platform.

It serves as the primary reference for building:
- Prompts
- Workflows
- System execution inside Hermes or any future execution engine

---

## 2. Design Philosophy

HostFlow AI uses a fixed set of core agents.

**Core principles:**
- Agents are permanent and do not change per project type
- Specialization is achieved through Profiles, Prompts, Workflows, and Knowledge
- Each agent has one clear responsibility (Single Responsibility)
- Orchestrator is the only control point
- No direct communication between users and agents other than Orchestrator
- All outputs pass through the Review Layer before final approval

> ⚠️ All tools and system components referenced in this document are logical abstractions. They will be defined in dedicated system design documents.

---

## 3. General Rules

- Each agent operates within a clearly defined scope
- No agent may perform responsibilities belonging to another agent
- All decisions pass through the Orchestrator
- All outputs pass through the Review Layer before final delivery
- Tools and technical systems are implementation details, not core design

---

## 4. Core Agents

The system contains 4 core agents + Review Layer.

---

## Agent 1 — Orchestrator Agent

**Role:** System manager and central decision maker

### Core Objective
Coordinate all platform operations and manage resources to ensure projects are executed efficiently and with high quality.

### Responsibilities
- Analyze user requests
- Identify project type
- Select the appropriate Profile
- Select the execution Workflow
- Assign tasks to agents
- Make execution or stop decisions
- Manage resources (Models + Tools)
- Re-route tasks when needed
- Manage Review Layer decisions

### Inputs
- User request
- Project Context
- Workflow
- Agent outputs
- System status

### Outputs
- Execution plan
- Task assignments
- Final decisions
- Status updates

### Allowed Tools
- Workflow Controller
- Model Router
- Memory System
- Logging System

### Out of Scope
- Does not perform research
- Does not create content
- Does not produce files

### Definition of Done
- Project was executed or stopped correctly
- Tasks were distributed clearly
- Process was managed without errors

---

## Agent 2 — Research Agent

**Role:** Research and knowledge engine

### Core Objective
Reduce uncertainty by gathering, analyzing, and filtering knowledge before execution begins.

### Responsibilities
- Search for required information
- Analyze sources
- Summarize data
- Build Knowledge Package
- Update Knowledge Base
- Reuse existing knowledge when available

### Research Levels
Supports 3 research levels determined by the Orchestrator based on project complexity:
- **Quick** — fast research using existing knowledge
- **Standard** — moderate depth, multiple sources
- **Deep** — comprehensive research for complex projects

> Detailed definitions will be specified in the Workflow Engine document.

### Inputs
- Project Context
- Research task
- Profile
- Orchestrator instructions
- Existing Knowledge Base

### Outputs
- Research Report
- Knowledge Package
- Key insights
- Risks and unknowns

### Allowed Tools
- Web Search
- Knowledge Base
- Document Reader

### Out of Scope
- Does not design
- Does not execute
- Does not produce final products

### Definition of Done
- Sufficient information was gathered
- Information was verified
- Knowledge was converted into a usable package for Builder Agent
- Knowledge Base was updated if new valuable information was found

---

## Agent 3 — Builder Agent

**Role:** System architect and planner

### Core Objective
Transform knowledge into a clear, executable design plan.

### Responsibilities
- Design system Architecture
- Design System Structure
- Design Workflows
- Create Folder Structure
- Convert knowledge into execution plan

### Inputs
- Knowledge Package (from Research Agent)
- Project Context
- Constraints from Orchestrator

### Outputs
- System Architecture Document
- Execution Plan
- Workflow Definition
- Structure Blueprint

### Allowed Tools
- Documentation System
- Architecture Templates
- Knowledge Base

### Out of Scope
- Does not execute
- Does not produce final files
- Does not perform research

### Definition of Done
- A clear and executable design was produced
- Knowledge was converted into an organized plan
- Plan is ready for Creator Agent

---

## Agent 4 — Creator Agent

**Role:** Final production executor

### Core Objective
Transform the design into final outputs ready for use or delivery.

### Responsibilities
- Create final files
- Produce content
- Convert design into output
- Format files according to Profile
- Follow the execution plan strictly

### Core Principle
Creator is a strict executor. It does not innovate, redesign, or make decisions. Any extra creativity is an architectural error.

### Inputs
- Execution Plan (from Builder Agent)
- System Design
- Profile
- Review feedback (if revision required)

### Outputs
- Final Artifacts
- Files: PDF / DOCX / MD / JSON / HTML

### Allowed Tools
- File Generator
- Template Engine
- Formatter

### Out of Scope
- Does not perform research
- Does not design
- Does not make decisions
- Does not evaluate quality

### Interaction Rule
All Creator outputs follow this path only:
```
Creator → Review Layer → Orchestrator
```
No direct path outside this flow.

### Definition of Done
- All required files were produced
- Design was followed exactly
- Output was delivered to Review Layer without structural errors

---

## 5. Review Layer (Quality System)

The Review Layer is not an agent. It is a quality control layer integrated into the workflow.

**Role:** Quality assurance system

### Core Objective
Ensure all system outputs are correct, complete, and consistent with the design before final delivery.

### Responsibilities
- Review output quality
- Detect errors
- Verify consistency with plan and Profile
- Evaluate final result
- Issue decision:
  - **Approve** — output is ready
  - **Reject** — output has critical issues
  - **Revision Required** — output needs specific fixes

### Inputs
- Outputs from agents
- Execution Plan
- Profile
- System rules

### Outputs
- Review Decision
- Feedback Report
- Re-routing instruction (if needed)

### Allowed Tools
- Validation Engine
- Comparison Engine
- Memory Access (read only)

### Out of Scope
- Does not create content
- Does not design
- Does not execute

### Definition of Done
- Every output was evaluated
- A clear decision was made
- No errors were passed to the final output

---

## 6. System Flow

```
User
 ↓
Orchestrator
 ↓
Research Agent
 ↓
Builder Agent
 ↓
Creator Agent
 ↓
Review Layer
 ↓
Final Output → User
```

---

## 7. Key Architecture Decisions

- 4 core agents only
- Review Layer as a quality system, not a separate agent
- Orchestrator is the sole decision maker
- Creator is a strict executor with no creative freedom
- Builder is a designer only, never a producer
- Research is a knowledge gatherer only, never a designer
- All agent behavior is controlled through Profiles, Prompts, Knowledge, and Workflows
- No agent holds private memory — all agents read and write to a shared Memory System
