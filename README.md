# Copilot Repository Assessment Bundle

This bundle is designed for GitHub Copilot Chat in your IDE or Copilot CLI on a local checked-out code repository.

## Goal

Analyze one repository at a time and produce a structured engineering assessment at:

`docs/assessments/<repo-name>-assessment.md`

The assessment is intended to feed a later orchestration step for:
- cross-repository synthesis
- learning recommendations
- engineering standards drafting

Each report now includes a `Synthesis Input Summary` section that normalizes repository signals, risk pattern tags, standards candidates, and learning recommendation signals for easier aggregation across repositories.

## What is included

- [SKILL.md](SKILL.md) — the main skill definition and assessment instructions
- [references/application-archetypes.md](references/application-archetypes.md) — how to assess different Spring Boot app shapes
- [references/architecture.md](references/architecture.md) — how to assess architectural separation of concerns and modularity
- [references/design.md](references/design.md) — how to assess design patterns and principles
- [references/readability.md](references/readability.md) — how to assess code clarity and understandability
- [references/reliability.md](references/reliability.md) — how to assess exception handling and failure modes
- [references/testability.md](references/testability.md) — how to assess test structure and design-for-testability
- [references/complexity.md](references/complexity.md) — how to assess code complexity and maintainability
- [references/recurring-risk-patterns.md](references/recurring-risk-patterns.md) — recurring engineering problems to watch for
- [templates/repository-assessment-template.md](templates/repository-assessment-template.md) — the exact report structure
- [usage-guide.md](usage-guide.md) — recommended workflow for running the assessment in Copilot

## Recommended usage

1. Open the target repository in your IDE or Copilot CLI session.
2. Ask Copilot to assess the repository using natural language — for example:
   ```
   Assess this repository for engineering quality.
   ```
   The skill triggers automatically. You do not need to paste any prompt.
3. If needed, follow up with targeted prompts to surface weak or shallow findings.
4. The final report is written to:
   `docs/assessments/<repo-name>-assessment.md`

See [usage-guide.md](usage-guide.md) for more example prompts and recommended workflow.

## Intended output characteristics

Each assessment should:
- detect the primary application archetype automatically
- include an executive summary and a detailed engineering assessment
- include real code snippets with exact names
- include a normalized `Synthesis Input Summary` for later aggregation
- focus on recurring patterns rather than isolated trivia
- distinguish structural issues from local issues
- call out likely cause categories with appropriate caution

## Notes

This bundle is intentionally focused on engineering quality, not procedural coding rules.
It is designed to support practical standards around architecture, design, readability,
reliability, testability, and complexity.
