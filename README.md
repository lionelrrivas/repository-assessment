# Repository Assessment

**The diagnostic layer for creating better engineering standards from real code.**

Repository Assessment is a GitHub Copilot skill for evaluating one checked-out Java/Spring Boot repository at a time and producing a structured engineering assessment at `docs/assessments/<repo-name>-assessment.md`.

Use it when you want evidence you can trust before drafting standards, planning refactors, or deciding where teams need better examples, coaching, or support. In most portfolio workflows, each repository assessment then feeds the companion **[cross-repository-engineering-synthesis](https://github.com/lionelrrivas/cross-repository-synthesis)** skill, which turns several detailed reports into a more readable, decision-oriented synthesis.

## The problem it solves

Standards built on opinions, isolated incidents, or quick codebase scans usually fail. They produce generic rules, turn local quirks into organization-wide guidance, and make standards discussions feel personal.

Repository Assessment gives you a better starting point: a repeatable, evidence-based diagnosis of one repository that you can compare and synthesize across many repositories before turning findings into standards.

## Why teams use it

- **Evidence before policy.** Standards candidates come from recurring code patterns, not taste.
- **Consistent evaluation.** Every repository is assessed across the same engineering dimensions and named checks.
- **Better synthesis inputs.** Each report includes normalized findings, standards candidates, and learning signals for later aggregation.
- **Better conversations.** The output frames problems as engineering patterns and support needs rather than personal judgment.
- **Sharper standards.** Detailed repository evidence helps teams write standards that are concise, practical, and teachable.

## What the report contains

Each assessment includes:

- an executive summary
- six dimension assessments: Architecture, Design, Readability, Reliability, Testability, and Complexity
- recurring engineering risk patterns
- likely underlying skill or standards gaps
- candidate examples for future engineering standards
- a normalized `Synthesis Input Summary` for cross-repository comparison

## How it fits into the workflow

Use Repository Assessment as the diagnostic first step in a broader standards workflow:

1. Assess 3 to 5 representative repositories.
2. Run the companion **cross-repository-engineering-synthesis** skill on the completed reports.
3. Use the synthesis to identify repeated patterns, high-leverage standards candidates, and repository-specific remediation.
4. Turn the strongest repeated findings into concise standards, learning recommendations, and enablement actions.

The repository assessment is intentionally the most detailed artifact in that chain. For broader audiences, the synthesis output is usually the better document to share.

| Artifact | Purpose | Audience | Level of detail |
|---|---|---|---|
| Repository assessment | Diagnose risks in one repository | Reviewers, leads, standards authors | High detail |
| Cross-repository synthesis | Compare patterns across multiple repositories and surface standards candidates | Leads, architects, engineering managers, broader stakeholders | Medium detail |
| Engineering standards | Define shared expectations | All developers | Concise and practical |
| Learning recommendations | Help developers improve specific skills | Team members, mentors | Supportive and targeted |

## Quick start

1. Open a checked-out target repository in your IDE or Copilot CLI session.
2. Ask Copilot to assess it naturally, for example:
   ```
   Assess this repository for engineering quality.
   ```
3. Let the skill inspect the repository and write the report to `docs/assessments/<repo-name>-assessment.md`.
4. Repeat across representative repositories, then run the companion **cross-repository-engineering-synthesis** skill on the completed reports.

See [usage-guide.md](usage-guide.md) for the recommended operating workflow.

## Which skill do I use?

| Situation | Best next step |
|---|---|
| You want a diagnostic report for one checked-out repository | Use **Repository Assessment** |
| You already have multiple completed assessment reports and want standards candidates, learning recommendations, remediation priorities, or a broader synthesis | Use the companion **cross-repository-engineering-synthesis** skill in the `cross-repository-synthesis` repository |
| You are focused on one obvious local issue in one repository | Fix it directly; you may not need the full assessment-and-synthesis workflow |

## FAQ

### When would I use this instead of a normal code review?

Use Repository Assessment when you want to understand recurring engineering patterns across a repository, not just comment on one pull request or one local change. It is designed to surface structural issues, strengths, and standards candidates that ordinary review workflows often miss.

### What should I not use it for?

Do not use it as a developer scorecard, a performance review input, or a shortcut to organization-wide policy from one repository. The report is evidence, not a verdict.

### What should I do after the report?

If your goal is standards work, assess a representative set of repositories and then run the companion **cross-repository-engineering-synthesis** skill. That is the step that helps you separate repeated standards candidates from learning recommendations and repository-specific cleanup.

### What if I disagree with or do not understand a finding?

Ask Copilot to explain the section in plainer language, show the strongest code evidence behind the claim, or help you decide whether the issue is systemic or local. A useful diagnostic should be explainable.

### What if the findings feel blunt or uncomfortable?

Treat the report as a repository diagnostic, not a public judgment. When it surfaces painful patterns, ask what support would help: clearer standards, better examples, pairing, workshops, checklists, or refactoring time. For broader sharing, use the framing in [references/how-to-read-repository-assessment-reports.md](references/how-to-read-repository-assessment-reports.md).

### Does this tool define mandatory audit or compliance requirements?

No. Repository Assessment helps you discover recurring engineering risks and candidate standards from repository evidence. Organization-wide controls such as approved platform versions, pull request approvals, or required repository files should live in a separate standards or controls baseline.

## Repository contents

- [SKILL.md](SKILL.md) - the main skill definition and assessment instructions
- [templates/repository-assessment-template.md](templates/repository-assessment-template.md) - the exact report structure
- [usage-guide.md](usage-guide.md) - how to use the skill effectively and review the output
- [references/how-to-read-repository-assessment-reports.md](references/how-to-read-repository-assessment-reports.md) - framing guidance for socializing detailed reports
- [references/](references/) - assessment guidance for architecture, design, readability, reliability, testability, complexity, recurring risks, and application archetypes
