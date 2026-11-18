# Agent team

I am using GitHub Copilot CLI in a Codespace to orchestrate Mona's Project Pulse dashboard team.

| Agent | Target model | Responsibility | Agent definition |
| --- | --- | --- | --- |
| Orchestrator | Claude Opus 5.5 (copilot) | Breaks the dashboard request into phases, delegates work to the specialist agents, separates file scopes, and verifies that the integrated result is coherent. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 5.5 (copilot) | Researches the repository and requirements, identifies dependencies and edge cases, and produces an ordered implementation plan with file assignments and validation expectations. | `.github/agents/planner.agent.md` |
| Coder | GPT-5.5 (copilot) | Implements the dashboard code and application support files, following repository patterns and validating behavior with clear, testable changes. | `.github/agents/coder.agent.md` |
| Designer | Gemini 3.7 Flash (copilot) | Defines the dashboard UI/UX, visual hierarchy, accessibility, responsive layout, interaction flow, and Project Pulse styling within the assigned file scope. | `.github/agents/designer.agent.md` |
