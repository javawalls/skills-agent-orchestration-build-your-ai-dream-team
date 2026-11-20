# Agent team

I am using GitHub Copilot CLI in a Codespace to orchestrate Mona's Project Pulse dashboard team.

- **Orchestrator** - **Claude Opus 5.5 (copilot)**. Coordinates the Planner, Coder, and Designer, turns the implementation plan into dependency-aware phases, assigns file scopes, and verifies the integrated result. Its definition is at `.github/agents/orchestrator.agent.md`.
- **Planner** - **Claude Opus 5.5 (copilot)**. Researches the repository and requirements, identifies edge cases and dependencies, and produces an ordered implementation plan with file assignments and validation expectations. It does not write code. Its definition is at `.github/agents/planner.agent.md`.
- **Designer** - **Gemini 3.7 Flash (copilot)**. Owns UI/UX, accessibility, information hierarchy, interaction flow, responsive behavior, and the polished visual treatment for the Project Pulse dashboard. Its definition is at `.github/agents/designer.agent.md`.
- **Coder** - **GPT-5.5 (copilot)**. Implements the dashboard and application logic, creates assigned support configuration such as the launch configuration, and validates the changes with explicit, testable behavior. Its definition is at `.github/agents/coder.agent.md`.
