# HostFlow AI — Architecture Layers

**Version:** 1.0
**Status:** Draft
**Phase:** Phase A — Architecture Design

---

## 1. Purpose

This document defines the layered architecture of the HostFlow AI platform.

The purpose of this architecture is to create a scalable, modular, maintainable, and extensible AI platform that can support multiple project types without requiring major architectural changes.

Each layer has a clearly defined responsibility and communicates through well-defined boundaries.

---

## 2. Architecture Principles

- Separation of Concerns
- Single Responsibility
- Modularity
- Scalability
- Maintainability
- Model Agnostic Design
- Tool Agnostic Design
- Knowledge Persistence
- Reusability
- Extensibility

Each layer is responsible for one specific concern only. No layer performs responsibilities that belong to another layer.

---

## 3. High-Level Architecture

```
User
│
▼
User Layer
│
▼
Interface Layer
│
▼
Orchestration Layer
│
▼
Intelligence Layer
│
▼
Model Layer
│
▼
Capability Layer
│
▼
Storage Layer
│
▼
Response
```

---

## 4. Layer Specifications

---

### 4.1 User Layer

**Purpose**
Represents every external actor that interacts with HostFlow AI.

**Responsibilities**
- Receive user requests
- Deliver final responses
- Support multiple access channels

**Examples**
- Telegram (current)
- Web Application
- REST API
- Mobile Application (future)

**Out of Scope**
- AI reasoning
- Business logic
- Model selection
- Tool execution

---

### 4.2 Interface Layer

**Purpose**
Transforms external requests into a standardized internal format. Acts as the communication bridge between users and the platform.

**Responsibilities**
- Validate requests
- Normalize incoming data
- Create structured internal project requests
- Forward requests to the Orchestration Layer

**Inputs:** User messages
**Outputs:** Structured Project Request

**Out of Scope**
- AI execution
- Decision making
- Workflow selection
- Agent management

---

### 4.3 Orchestration Layer

**Purpose**
Acts as the central coordinator of the entire platform. Responsible for managing project execution from start to finish.

**Responsibilities**
- Understand project requests
- Select the appropriate Project Profile
- Select the execution workflow
- Select AI agents
- Select AI models
- Select tools
- Manage execution order
- Retry failed tasks
- Monitor project progress
- Coordinate communication between agents
- Invoke Human-in-the-Loop when needed
- Return the final result

**Inputs:** Structured Project Request
**Outputs:** Tasks assigned to AI Agents

**Out of Scope**
- Writing content
- Research
- Building outputs
- Reviewing artifacts

---

### 4.4 Intelligence Layer

**Purpose**
Contains the specialized AI Agents responsible for executing project tasks. Each agent focuses on one responsibility.

**Core Agents**
- Orchestrator Agent
- Research Agent
- Builder Agent
- Creator Agent
- Reviewer Agent

**Responsibilities**
- Execute assigned tasks
- Collaborate through the Orchestration Layer
- Produce project outputs

**Core Principle**
Agents remain permanent. Only the following change between projects:
- Profiles
- Prompts
- Knowledge
- Workflows

The platform does not create new agents for every project.

---

### 4.5 Model Layer

**Purpose**
Provides AI models independently from the agents. Agents request model capabilities rather than being permanently connected to a specific model.

**Responsibilities**
- Provide the appropriate model per task
- Support multiple providers
- Allow model replacement without affecting agents
- Optimize model selection based on task type

**Example Model Types**
- Reasoning Model
- Research Model
- Writing Model
- Evaluation Model
- Fast Model

**Core Principle**
Agents are independent of model providers. Changing the AI provider should never require redesigning the architecture.

---

### 4.6 Capability Layer

**Purpose**
Provides all external capabilities required to execute real-world tasks. Agents request capabilities instead of implementing them internally.

**Responsibilities**
Provide services such as:
- Web Search
- Browser Automation
- PDF Generation
- DOCX Generation
- Markdown Export
- Image Generation
- GitHub
- Google Drive
- Telegram
- Email
- External APIs

**Core Principle**
Agents think. Capabilities act.

This separation keeps agents simple, reusable, and maintainable.

---

### 4.7 Storage Layer

**Purpose**
Provides persistent storage for all platform knowledge, project data, execution history, and reusable assets.

**Components**

**Project Storage**
- Projects and their status
- Generated outputs
- Project metadata

**Knowledge Storage**
- Reusable research and domain knowledge
- Allows future projects to reuse previous findings instead of starting from zero

**Prompt Storage**
- All system prompts used by agents

**Profile Storage**
- Domain-specific project profiles
- Examples: Digital Products, Websites, SaaS, AI Services

**Execution Logs**
- Agent activity
- Tool usage
- Model selection
- Errors and retry history
- Execution timeline

Supports debugging, monitoring, and continuous improvement.

---

## 5. End-to-End Request Flow

1. The user submits a request.
2. The User Layer receives the request.
3. The Interface Layer validates and standardizes it.
4. The Orchestration Layer analyzes the request.
5. The appropriate workflow, profile, models, and agents are selected.
6. Tasks are executed by the Intelligence Layer agents.
7. Agents request external capabilities through the Capability Layer.
8. All project data is stored in the Storage Layer.
9. The Orchestration Layer collects the final outputs.
10. The completed result is returned to the user.

---

## 6. Key Design Decisions

- Agents remain permanent across all projects.
- Project specialization is achieved through Profiles, Prompts, Knowledge, and Workflows.
- AI Models are separated from AI Agents.
- External tools are abstracted behind the Capability Layer.
- Knowledge is preserved and reused across projects.
- All execution is coordinated through the Orchestration Layer.
- Layers communicate only through defined responsibilities.

---

## 7. Future Documents

The following topics are covered in dedicated documents:

- Agent Roles
- Communication Protocol
- Memory System
- Tool Registry
- Prompt System
- Workflow Engine
