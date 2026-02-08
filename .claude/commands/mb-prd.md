---
description: Generate a Product Requirements Document (PRD) with rigorous design analysis (Context, Solution Exploration, Consultation).
globs:
  - memory-bank/projectbrief.md
  - memory-bank/techContext.md
  - memory-bank/systemPatterns.md
  - .cursor/templates/prd-template.md
---

# PRD Generation Command

This command generates a structured Product Requirements Document (PRD) following the **Feature Design Workflow** (Phases 1-3).

## Instructions

1.  **Analyze Context (Phase 1)**:
    -   Read `memory-bank/projectbrief.md`, `techContext.md`, and `systemPatterns.md`.
    -   Identify affected components and constraints (Security, Performance).
    -   Read relevant source code files to understand current implementation.

2.  **Explore Solutions (Phase 2)**:
    -   Generate **3+ distinct technical approaches**.
    -   Evaluate each against criteria: Security, Pattern Alignment, DRY, Testability.
    -   Reject approaches with **Anti-Patterns** (e.g., hardcoded secrets, raw SQL).

3.  **Consult User (Phase 3)**:
    -   Present the alternatives clearly.
    -   Wait for user approval on the selected approach.

4.  **Generate PRD**:
    -   Use the structure from `.cursor/templates/prd-template.md`.
    -   Include: Problem Statement, Scope, Context Analysis, Technical Approach (Selected + Alternatives), Success Criteria, Risks.
    -   Save to `memory-bank/prd/PRD-{slug}.md`.

5.  **Output Summary**:
    -   Confirm file location.
    -   List next steps: `/mb-init` (or `/van`), `/mb-plan`.

## Template Structure

The PRD MUST include:
-   **Context & Analysis**: Existing code insights, Constraints.
-   **Technical Approach**: Proposed solution, Alternatives considered (Pros/Cons).
-   **Risks & Mitigation**: Security and technical risks.
-   **Success Criteria**: Measurable outcomes.

## Usage

Run: `/mb-prd "Brief description of the task"`
