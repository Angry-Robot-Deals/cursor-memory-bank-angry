# Design Improvements for Initialization & Planning (DEV-0008)

## Overview
This task integrates the "Feature Design and Planning Workflow" from [extractum-skills/run_design.md](https://github.com/extractumio/extractum-skills/blob/main/domain-specific/vibecoding/commands/run_design.md) into the core Memory Bank system.

## Source Analysis & Gap Analysis

The source document defines a 6-phase workflow:
1.  **Context Gathering**: Study docs, scope, constraints.
2.  **Solution Brainstorming**: 3+ approaches, evaluation, rejection criteria.
3.  **User Consultation**: Present options, get approval.
4.  **Detailed Design**: Component breakdown, Security design (Appendix A).
5.  **Design Document**: Detailed implementation plan template.
6.  **Documentation Updates**: Identify updates.

**Current Implementation Gaps (Addressed):**
-   **Security**: `Appendix A` (Threat Model, Controls Checklist) added to `/plan` and `/mb-plan`.
-   **Detailed Design**: `/plan` now requires rigorous component breakdown.
-   **Templates**: PRD template aligned with Phases 1-3; Plan template aligned with Phase 5.
-   **Anti-Patterns**: Added to instructions in `/prd` and `/plan`.

## Implementation Strategy

### 1. Cursor `/prd` Command
*   **Focus**: Phases 1, 2, and 3.
*   **Updates**:
    *   Include "Design Principles" and "Anti-Patterns".
    *   Refine "Context Gathering" prompt.
    *   Refine "Solution Exploration" to use the "Approaches" template.
    *   Refine "User Consultation" to use the "Alternatives" template.

### 2. Cursor `/plan` Command
*   **Focus**: Phases 4, 5, and 6.
*   **Updates**:
    *   Integrate "Detailed Design" instructions (Component breakdown, Interface, Data flow).
    *   Integrate "Security Design" (Appendix A requirements).
    *   Update "Implementation Plan Template" to match Phase 5 template (Security Summary, Architecture Impact, Detailed Design, Security Design, Implementation Steps, Test Plan, Rollback, Validation).

### 3. Claude Commands (`/mb-*`) & Agents
*   Sync all changes from Cursor commands to Claude commands.
*   Update `Architect` to own Phases 1-3 (PRD).
*   Update `Planner` to own Phases 4-6 (Plan).

## Action Plan
- [x] **Analyze**: Review source document.
- [x] **Update `/prd`**: Align with Phases 1-3.
- [x] **Update `/plan`**: Align with Phases 4-6 and Appendix A.
- [x] **Update Claude Commands**: `mb-prd.md`, `mb-plan.md`.
- [x] **Update Agents**: `architect.md`, `planner.md`.
- [x] **Update Documentation**: `README.md` to reflect the rigorous workflow.
- [ ] **Verify**: Check templates and prompts.

## References
- Source: https://github.com/extractumio/extractum-skills/blob/main/domain-specific/vibecoding/commands/run_design.md
