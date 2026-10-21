# Agent team

I will use this custom agent team to build Mona's Project Pulse dashboard, with GitHub Copilot CLI in a Codespace orchestrating the work.

| Agent | Target model | Responsibility | Definition |
| --- | --- | --- | --- |
| Orchestrator | Claude Opus 5.5 (copilot) | Breaks the project into phases, delegates work to specialists with clear file scopes, coordinates dependencies, and verifies the integrated result. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 5.5 (copilot) | Researches the repository, documentation, dependencies, and edge cases, then creates an actionable implementation plan. | `.github/agents/planner.agent.md` |
| Designer | Gemini 3.7 Flash (copilot) | Shapes the dashboard's user experience, accessibility, information hierarchy, interactions, visual design, and responsive behavior. | `.github/agents/designer.agent.md` |
| Coder | GPT-5.5 (copilot) | Implements assigned application code and logic, follows repository patterns, and validates the changes. | `.github/agents/coder.agent.md` |
