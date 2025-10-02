# async-sdd-slashes

This project provides a framework for developing a collection of CLI commands inspired by tools like Codex CLI, Claude CLI, and Gemini CLI, using the Specification-Driven Development (SDD) process.

## Overview

The SDD process is structured around specialized roles, each contributing to a phase of development. This ensures transparency, thorough analysis, and systematic implementation.

## SDD Files

- **sdd-0-rq.md**: Business Analyst - Extracts and defines requirements from discussion logs into a clear document.
- **sdd-1-d.md**: Software Architect - Outlines the solution architecture and implementation plan.
- **sdd-2-td.md**: QA Engineer - Plans testing strategies and coverage.
- **sdd-3-tk.md**: Engineering Manager - Breaks down tasks into phases and assigns agents.
- **sdd-4-pm.md**: Prompt Engineer - Creates activation prompts for agents based on tasks.
- **sdd-5-or.md**: Engineering Manager - Orchestrates parallel agent execution using Jujutsu (jj) for version control.
- **sdd-6-dc.md**: Document Manager - Recommends documentation integration and updates.

## Dependencies

- **Jujutsu (jj)**: Version control system for parallel agent workflow management
- **CodeRabbit CLI**: AI code review tool for final quality assurance

## Workflow

```mermaid
graph TD
    A[sdd-0-rq: Requirements] --> B[sdd-1-d: Design]
    B --> C[sdd-2-td: Test Design]
    C --> D[sdd-3-tk: Task Breakdown]
    D --> E[sdd-4-pm: Generate Prompts]
    E --> F[sdd-5-or: Orchestration Start]

    F --> G[git checkout branch<br/>jj git init --colocate]

    G --> H1[Phase 1: Parallel Agents]
    H1 --> I1[jj merge changesets]
    I1 --> J1[Orchestrator Review & Fix]
    J1 --> K1[Build & Test]
    K1 --> L1[git commit 'Phase 1']

    L1 --> H2[Phase 2: Parallel Agents]
    H2 --> I2[jj merge changesets]
    I2 --> J2[Orchestrator Review & Fix]
    J2 --> K2[Build & Test]
    K2 --> L2[git commit 'Phase 2']

    L2 --> H3[Phase N: Parallel Agents]
    H3 --> I3[jj merge changesets]
    I3 --> J3[Orchestrator Review & Fix]
    J3 --> K3[Build & Test]
    K3 --> L3[git commit 'Phase N']

    L3 --> M[CodeRabbit Final Review]
    M --> N{Issues?}
    N -->|Yes| O[Create Fix Phase]
    O --> H3
    N -->|No| P[sdd-6-dc: Documentation]
    P --> Q[git push / Create PR]

    style H1 fill:#e1f5ff
    style H2 fill:#e1f5ff
    style H3 fill:#e1f5ff
    style M fill:#ffe1e1
    style P fill:#e1ffe1
```

## Usage

Follow the SDD process by activating each role in sequence, using the `.tmp/` directory for intermediate artifacts like `minutes.md`, `requirements.md`, etc. This framework helps build robust CLI tools through structured development.

### Key Points
- Each phase creates parallel jj changesets for agents
- Orchestrator reviews and fixes after each phase merge
- Each phase becomes a separate git commit
- CodeRabbit reviews final implementation
- Documentation updates based on all phase changes
