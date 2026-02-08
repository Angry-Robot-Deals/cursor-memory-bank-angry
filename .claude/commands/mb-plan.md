---
description: Create detailed implementation plan (Phases 4-6, Appendix A Security).
globs:
  - memory-bank/tasks.md
  - memory-bank/activeContext.md
  - memory-bank/prd/*.md
---

# PLAN Command

This command generates a detailed implementation plan in `memory-bank/tasks.md`, strictly following the **Enhanced Design Process** (Phases 4-6).

## Instructions

1.  **Analyze Context**:
    -   Read `memory-bank/tasks.md` (Complexity, Requirements).
    -   Read `memory-bank/activeContext.md` (Current Context).
    -   Review `memory-bank/prd/*.md` if available.

2.  **Detailed Design (Phase 4)**:
    -   **Component Breakdown**: List every modified and new file.
    -   **Interface Design**: Define function signatures, API contracts.
    -   **Data Flow**: Trace input -> processing -> output.
    -   **Security Design**: Perform **Threat Modeling** and map to **Security Controls** (Appendix A).

3.  **Create Implementation Plan (Phase 5)**:
    -   Update `memory-bank/tasks.md` using the **Design Document Template**.
    -   Include: **Security Summary** (Attack Surface, Risks), **Architecture Impact**, **Detailed Design** (API, DB, Config), **Security Design** (Threats, Controls), **Implementation Steps**, **Test Plan** (Unit/Integration/Security), **Rollback Strategy**, **Validation Checklist**.

4.  **Technology Validation**:
    -   Document technology stack selection.
    -   Verify dependencies and build configuration.

5.  **Output Summary**:
    -   Confirm task status update.
    -   List next steps: `/mb-do` (or `/do`).

## Template Structure (Design Document)

The plan in `memory-bank/tasks.md` MUST follow the `Implementation Plan Template` defined in `.cursor/commands/plan.md`.

## Security Requirements (Appendix A)

-   **Principles**: Fail-closed, Least privilege, No secrets in code/logs.
-   **Anti-Patterns**: Trusting user input, Logging sensitive data, Hardcoding secrets, SQL concatenation, Unvalidated file paths.

## Usage

Run: `/mb-plan`
