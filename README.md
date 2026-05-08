# Repository Assessment

**The diagnostic layer for creating better engineering standards from real code.**

Repository Assessment is a GitHub Copilot skill for evaluating one checked-out Java/Spring Boot repository at a time and producing a structured engineering assessment at `docs/assessments/<repo-name>-assessment.md`.

The goal is not to generate generic advice. The goal is to create evidence you can trust when you want to:

- identify recurring engineering risks
- compare patterns across repositories
- draft better engineering standards
- turn painful findings into focused learning recommendations

Used well, the output supports engineering enablement: clearer standards, better reference examples, targeted coaching, and better support for teams doing hard work in difficult codebases. It is not a grading tool or a verdict on the people who have worked in a repository.

## The problem it solves

Most standards work starts from the wrong inputs: strong opinions, one dramatic incident, or a quick skim of a codebase. That usually leads to one of three outcomes:

- standards that are too generic to change behavior
- one repository's quirks getting mistaken for organization-wide guidance
- uncomfortable discussions that feel personal because the evidence is thin

Repository Assessment creates a repeatable diagnostic step before standards work begins. It inspects the code in depth, captures recurring patterns across six engineering dimensions, and produces a normalized summary that can be synthesized across repositories.

## Why teams use it

- **Evidence before policy.** Standards candidates come from recurring code patterns, not taste.
- **Consistent evaluation.** Every repository is assessed across the same engineering dimensions and named checks.
- **Faster synthesis.** Each report includes standards candidates, learning signals, and normalized risk tags for later aggregation.
- **Better conversations.** The output frames problems as design, architecture, and maintainability issues rather than personal judgment.
- **Enablement, not indictment.** Findings should drive support such as standards, examples, refactoring time, pairing, and coaching.
- **Sharper standards.** Detailed repository evidence lets the eventual standards stay concise, practical, and teachable.

## What the report contains

Each assessment includes:

- an executive summary suitable for socialization
- six dimension assessments: Architecture, Design, Readability, Reliability, Testability, and Complexity
- recurring engineering risk patterns
- likely underlying skill or standards gaps
- recommended candidate examples for future engineering standards
- a normalized `Synthesis Input Summary` for cross-repository comparison

## How it fits into a standards workflow

Use Repository Assessment as the first step in a broader standards workflow:

1. Assess several representative repositories.
2. Compare recurring patterns across those assessments.
3. Turn the strongest repeated findings into concise engineering standards.
4. Use the learning signals to plan coaching, workshops, katas, or reference material.

The assessment report is intentionally the most detailed artifact in that chain. It exists to feed higher-level, simpler outputs later.

| Artifact | Purpose | Audience | Level of detail |
|---|---|---|---|
| Repository assessment | Diagnose risks in one repository | Reviewers, leads, standards authors | High detail |
| Cross-repository synthesis | Identify recurring patterns across repositories | Leads, architects, engineering managers | Medium detail |
| Engineering standards | Define shared team expectations | All developers | Concise and practical |
| Learning recommendations | Help developers improve specific skills | Team members, mentors | Supportive and targeted |

## End-to-end adoption flow

If you are using this workflow to improve engineering standards across a portfolio, a healthy sequence looks like this:

1. Assess 3 to 5 representative repositories with **Repository Assessment**.
2. Run the companion **cross-repository-engineering-synthesis** skill on the completed assessment reports.
3. Select 2 to 3 high-leverage standards candidates instead of trying to standardize everything at once.
4. Turn the learning recommendations and remediation outputs into concrete enablement actions such as examples, pairing, workshops, checklists, and refactoring time.

This keeps the workflow practical. The outcome should be a small number of better standards plus better support for the teams expected to apply them.

## Healthy response to uncomfortable findings

Uncomfortable findings are normal in a useful diagnostic. A repository reflects legacy constraints, delivery pressure, ownership changes, missing examples, and inconsistent standards, not just individual skill.

When a report surfaces painful patterns, the healthy response is to ask what support would help: clearer standards, better examples, pairing, workshops, checklists, or refactoring time. Keep the conversation centered on recurring patterns and enablement actions, not on assigning blame. If the report is used to rank people, the workflow has been misused.

## Quick start

1. Open a checked-out target repository in your IDE or Copilot CLI session.
2. Ask Copilot to assess it naturally, for example:
   ```
   Assess this repository for engineering quality.
   ```
3. Let the skill inspect the repository and write the report to:
   `docs/assessments/<repo-name>-assessment.md`
4. Repeat across representative repositories before drafting standards from the results.

See [usage-guide.md](usage-guide.md) for the recommended operating workflow.

## Which skill do I use?

| Situation | Best next step |
|---|---|
| You want a diagnostic report for one checked-out repository | Use **Repository Assessment** |
| You already have multiple completed assessment reports and want standards candidates, learning recommendations, or remediation priorities | Use the companion **cross-repository-engineering-synthesis** skill in the `cross-repository-synthesis` repository |
| You are focused on one obvious local issue in one repository | Fix it directly; you may not need the full assessment-and-synthesis workflow |

## Frequently asked questions

### Why is the report so detailed?

Because the report is a diagnostic artifact, not the final engineering standard. The detail helps reviewers understand where patterns actually appear, which findings are systemic versus local, and which examples are strong enough to reuse later. The standards that come after this step should be much shorter.

### Is the report itself the engineering standard?

No. The report is evidence. The cross-repository synthesis step decides which patterns are common or important enough to become shared guidance.

### Is this meant to grade developers or embarrass repository owners?

No. The point is to identify repeatable engineering risks and learning opportunities, not to create a scorecard for people. A repository usually reflects many forces besides individual skill, including legacy design, delivery pressure, shifting ownership, and unclear standards. Treat the findings as input for standards, refactoring priorities, and coaching conversations that help teams succeed.

### What if the findings feel blunt or uncomfortable?

Candid findings are useful only when they are framed correctly. Start by treating the report as a repository diagnostic, not a public judgment. Then ask what enablement or support would help most: standards, examples, pairing, training, or time to improve high-friction areas. If the audience is new to this workflow, use the framing in [references/how-to-read-repository-assessment-reports.md](references/how-to-read-repository-assessment-reports.md) before sharing raw reports broadly.

### What if I do not understand the report or parts of it are hard to follow?

Ask Copilot for help. A good next step is to ask it to explain a section in plainer language, summarize the most important findings, point back to the code evidence behind a claim, or suggest the best follow-up questions to ask. Needing help interpreting a detailed diagnostic is normal, and using Copilot to walk through the report is part of using the workflow effectively.

### Why not skip straight to writing standards?

Because standards written without evidence tend to be generic, political, or overfit to one repository. Repository Assessment gives you concrete examples, repeated patterns, and comparable signals before you ask the organization to change behavior.

### How do I get from assessment report(s) to standards?

Use the companion `cross-repository-engineering-synthesis` skill from the `cross-repository-synthesis` repository once you have a representative set of assessment reports. Repository Assessment produces the diagnostic inputs, including the `Synthesis Input Summary` section that the synthesis workflow expects. The synthesis step then compares reports, identifies recurring patterns, separates standards candidates from learning recommendations and repository-specific remediation, and produces the package you can use to draft final standards.

### How should I share these reports?

Start with leads, reviewers, and standards authors. For broader team communication, prefer a cross-repository synthesis over a raw single-repository report. That keeps the discussion focused on themes, standards candidates, and learning needs instead of one repository's rough edges.

## Repository contents

- [SKILL.md](SKILL.md) - the main skill definition and assessment instructions
- [templates/repository-assessment-template.md](templates/repository-assessment-template.md) - the exact report structure
- [usage-guide.md](usage-guide.md) - how to use the skill effectively and review the output
- [references/how-to-read-repository-assessment-reports.md](references/how-to-read-repository-assessment-reports.md) - framing guidance for socializing detailed reports
- [references/](references/) - assessment guidance for architecture, design, readability, reliability, testability, complexity, recurring risks, and application archetypes
