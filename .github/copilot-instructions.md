# >>> agent-instructions-react
Read and follow agent/master-instructions.md as the primary instruction set for React development.

## Workflow
- Plan first: 'plan frontend for TICKET-ID'
- Execute one phase at a time: 'execute plan N for TICKET-ID'
- Verify after each phase, then stop for human review
- Never auto-continue to the next phase without explicit approval

## Rules
- Planning and execution are separate phases - never write code during planning
- Read agent/workflow/context-router.md FIRST to load only relevant files
- Save plans to docs/TICKET-ID-plan.md
- Read tickets from tickets/TICKET-ID.md or fetch via agent/fetch-ticket.sh

## Key Files
- agent/master-instructions.md - Main instructions and workflow
- agent/workflow/context-router.md - Task type → required files mapping
- agent/workflow/initialise.md - Project onboarding (first-time setup)
- agent/workflow/planning.md - Planning rules
- agent/workflow/execution.md - Execution discipline
- agent/workflow/implementation.md - React coding conventions
- agent/workflow/testing.md - Verification commands
- agent/workflow/reviewer.md - Structured code review checklist
- agent/workflow/ticketing-systems.md - Ticket fetching helpers (Linear/Jira/GitHub)
- agent/architecture/patterns.md - Design patterns and standards
- agent/architecture/component-design.md - Component patterns and composition
- agent/architecture/accessibility.md - WCAG, ARIA, keyboard navigation
- agent/infrastructure/security.md - XSS prevention, auth tokens, CSP
# <<< agent-instructions-react
