# Usage Guide

Repository Assessment works best as a repeatable evidence-gathering workflow, not a one-off audit. Use this guide to trigger the skill effectively, review the report for real signal, and move from single-repository diagnostics to cross-repository standards work.

## When and how to use it

Use the skill when you want to understand the engineering health of a checked-out Java/Spring Boot repository and turn that assessment into better standards, learning plans, or refactoring priorities.

Ask naturally from inside the target repository:

```
Assess this repository for engineering quality.
```

```
Review this codebase and give me an assessment report.
```

```
Audit this microservice - I'm particularly interested in architecture and testability.
```

You do not need to name the skill or paste a long system prompt.

## What the skill produces

The skill writes a markdown report to `docs/assessments/<repo-name>-assessment.md` that includes:

- an executive summary
- ratings across Architecture, Design, Readability, Reliability, Testability, and Complexity
- recurring risk patterns, likely capability gaps, and candidate examples for future standards
- a normalized `Synthesis Input Summary` for cross-repository comparison

The report is intentionally detailed. In most multi-repository workflows, it becomes input to the companion **cross-repository-engineering-synthesis** skill, which produces the more readable artifact for standards discussions and broader sharing.

## Recommended workflow

### 1. Pick representative repositories

If your goal is standards creation, start with 3 to 5 repositories that give you contrast:

- one relatively healthy repository
- one average repository
- one painful or high-friction repository
- more than one archetype if possible

### 2. Run the assessment from inside each target repository

The skill inspects the local file system directly, so run it from the checked-out repository you want assessed. Let it inspect the repository before trying to steer the conclusions.

### 3. Review the report for signal quality

Before using the report downstream, check that it:

- finds recurring patterns rather than isolated trivia
- uses real code evidence with exact class names
- captures both strengths and weaknesses
- distinguishes systemic issues from local issues
- identifies the archetype sensibly
- keeps the `Synthesis Input Summary` consistent with the final ratings

If the first pass feels weak or hard to follow, use follow-up prompts like:

- Show stronger evidence for the architecture concerns.
- Which findings are structural versus local?
- Which examples are the strongest candidates for future standards?
- Explain the Design section in plainer language.
- Summarize this report for an engineering manager who is new to this workflow.

### 4. Synthesize before drafting standards

Do not turn one repository's report directly into organization-wide policy. Review multiple assessments first, then run the companion **cross-repository-engineering-synthesis** skill to compare repeated patterns and separate standards candidates from repository-specific cleanup.

For leaders, standards authors, and wider communication, the synthesis output is usually the better artifact to share.

## Use the output responsibly

The report is diagnostic evidence, not a verdict on the people who worked in the repository. Repository state often reflects legacy constraints, delivery pressure, evolving ownership, missing examples, and inconsistent standards as much as individual skill.

Use the output to:

- identify recurring risks worth standardizing
- separate repository cleanup from broader standards work
- spot learning opportunities and coaching needs
- identify where teams need clearer examples, pairing, workshops, checklists, or refactoring time

Do not use the report to grade developers, support performance reviews, or define mandatory organization-wide controls by itself. If your organization also has audit or compliance expectations, keep those in a separate standards or controls baseline.

For broader sharing, pair raw reports with [references/how-to-read-repository-assessment-reports.md](references/how-to-read-repository-assessment-reports.md).
