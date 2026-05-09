# Repository Assessment

**The diagnostic layer for creating better engineering standards from real code.**

Repository Assessment is a GitHub Copilot skill for evaluating one checked-out Java/Spring Boot repository at a time and producing a structured engineering assessment at `docs/assessments/<repo-name>-assessment.md`.

For most standards work, this detailed report is the input to the companion **cross-repository-engineering-synthesis** skill, which turns several repository assessments into a more readable, decision-oriented output for broader audiences.

The goal is not to generate generic advice. The goal is to create evidence you can trust when you want to:

- identify recurring engineering risks
- compare patterns across repositories
- draft better engineering standards
- turn painful findings into focused learning recommendations

Used well, the output supports engineering enablement: clearer standards, better reference examples, targeted coaching, and better support for teams doing hard work in difficult codebases. It is not a grading tool or a verdict on the people who have worked in a repository.

## The problem it solves

Standards built on opinions, isolated incidents, or quick codebase scans usually fail. They produce generic rules, turn local quirks into organization-wide guidance, and make standards discussions feel personal.

Repository Assessment gives you a better starting point: a repeatable, evidence-based diagnosis of one repository that you can compare and synthesize across many repositories before turning findings into standards.

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
2. Run the companion **cross-repository-engineering-synthesis** skill on the completed assessment reports.
3. Use the synthesis to compare recurring patterns and identify the strongest repeated findings.
4. Turn those findings into concise engineering standards, learning recommendations, and remediation priorities.
5. Use the learning signals to plan coaching, workshops, katas, or reference material.

The assessment report is intentionally the most detailed artifact in that chain. It exists to feed the companion synthesis step, which produces the more user-friendly artifact you will usually want to socialize more broadly.

| Artifact | Purpose | Audience | Level of detail |
|---|---|---|---|
| Repository assessment | Diagnose risks in one repository | Reviewers, leads, standards authors | High detail |
| Cross-repository synthesis | Turn multiple assessment reports into more readable cross-repository guidance | Leads, architects, engineering managers, broader stakeholders | Medium detail |
| Engineering standards | Define shared team expectations | All developers | Concise and practical |
| Learning recommendations | Help developers improve specific skills | Team members, mentors | Supportive and targeted |

## End-to-end adoption flow

If you are using this workflow to improve engineering standards across a portfolio, a healthy sequence looks like this:

1. Assess 3 to 5 representative repositories with **Repository Assessment**.
2. Run the companion **cross-repository-engineering-synthesis** skill on the completed assessment reports.
3. Use that synthesis as the more readable output for leaders, standards authors, and broader audiences.
4. Select 2 to 3 high-leverage standards candidates instead of trying to standardize everything at once.
5. Turn the learning recommendations and remediation outputs into concrete enablement actions such as examples, pairing, workshops, checklists, and refactoring time.

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
4. Repeat across representative repositories, then run the companion **cross-repository-engineering-synthesis** skill to turn those detailed reports into a more user-friendly synthesis.

See [usage-guide.md](usage-guide.md) for the recommended operating workflow.

## Which skill do I use?

| Situation | Best next step |
|---|---|
| You want a diagnostic report for one checked-out repository | Use **Repository Assessment** |
| You already have multiple completed assessment reports and want standards candidates, learning recommendations, or remediation priorities | Use the companion **cross-repository-engineering-synthesis** skill in the `cross-repository-synthesis` repository |
| You are focused on one obvious local issue in one repository | Fix it directly; you may not need the full assessment-and-synthesis workflow |

## If you're new to this tool

These questions will help you get oriented quickly.

### When would I use this instead of a normal code review?

Use Repository Assessment when you want to understand recurring engineering patterns across a repository, not just comment on a specific pull request or one local change. It is meant to surface structural issues, strengths, and standards candidates that ordinary review workflows often miss.

### What kinds of problems is this especially good at finding?

It is most useful for finding repeatable design and maintainability issues such as weak architectural boundaries, anemic domain models, hard-to-test orchestration, reliability risks, and complexity that slows teams down over time.

### What can I do with the output once I have it?

Use the report to support standards discussions, refactoring priorities, coaching plans, and cross-repository comparisons. In most portfolio-level workflows, the next step is to feed completed reports into the companion **cross-repository-engineering-synthesis** skill, which turns the detailed diagnostics into a more readable synthesis for decision-making and broader sharing.

### What should I not use it for?

Do not use it as a developer scorecard, a performance review input, or a quick way to turn one repository's problems into organization-wide policy. The report is evidence, not a verdict.

### What would a good first pilot look like?

A good pilot usually starts with 3 to 5 representative repositories: one relatively healthy, one average, and one painful or high-friction repository. That gives you enough contrast to spot patterns that are worth turning into broader standards.

### Who should read the report first?

Start with engineering leads, reviewers, architects, and standards authors. For broader audiences, it is usually better to share the output from the companion **cross-repository-engineering-synthesis** skill than a raw single-repository assessment.

### What should I ask if I disagree with a finding?

Good follow-up questions include: What is the strongest evidence for this claim? Is this issue systemic or local? Does it show up in other repositories? Would this be a standards candidate, a learning issue, or just repository cleanup?

### How does this relate to engineering standards or audit requirements?

Repository Assessment can help you discover and justify standards, but it does not define mandatory organization-wide controls by itself. Shared rules such as platform versions, approval requirements, or required repository files should live in a separate standards or controls baseline.

### What is the next step after the report?

The next step is usually to run the companion **cross-repository-engineering-synthesis** skill on a representative set of completed reports. That synthesis helps you identify repeated patterns and separate them into standards candidates, learning recommendations, and repository-specific remediation work.

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

Because standards written without evidence tend to be generic, political, or too specific to one repository. Repository Assessment gives you concrete examples, repeated patterns, and comparable signals before you ask the organization to change behavior.

### How do I get from assessment report(s) to standards?

Use the companion `cross-repository-engineering-synthesis` skill from the `cross-repository-synthesis` repository once you have a representative set of assessment reports. Repository Assessment produces the diagnostic inputs, including the `Synthesis Input Summary` section that the synthesis workflow expects. The synthesis step then compares reports, identifies recurring patterns, separates standards candidates from learning recommendations and repository-specific remediation, and produces the package you can use to draft final standards.

### Which output should I share with a broader audience?

Usually the output from the companion `cross-repository-engineering-synthesis` skill, not a raw single-repository assessment. Repository Assessment is intentionally detailed and diagnostic. The synthesis step is the more readable, decision-oriented artifact for leaders, standards authors, and broader communication.

### Does this tool define mandatory audit or compliance requirements?

No. Repository Assessment helps you identify recurring engineering risks and candidate standards from repository evidence. It does not decide organization-wide controls such as required Java or Spring Boot versions, minimum pull request approvals, required repository files like `README.md`, or similar audit-oriented requirements.

### Where should mandatory controls such as Java 25, Spring Boot 4, two approvals, or a required README live?

Put those in a separate engineering standards or controls baseline that acts as the source of truth for organization-wide requirements. A practical structure is:

- **Platform standards** - approved runtime and framework expectations such as Java 25 or Spring Boot 4
- **Governance controls** - workflow requirements such as minimum code review approvals
- **Repository hygiene** - required repository artifacts such as `README.md`, ownership files, or contribution guidance
- **Structural engineering standards** - design, architecture, reliability, testability, and maintainability expectations informed by repository evidence

Repository Assessment can help justify or refine those standards, but one repository report should not become the rule by itself.

### How should I share these reports?

Start with leads, reviewers, and standards authors. For broader team communication, prefer a cross-repository synthesis over a raw single-repository report. That keeps the discussion focused on themes, standards candidates, and learning needs instead of one repository's rough edges.

## Repository contents

- [SKILL.md](SKILL.md) - the main skill definition and assessment instructions
- [templates/repository-assessment-template.md](templates/repository-assessment-template.md) - the exact report structure
- [usage-guide.md](usage-guide.md) - how to use the skill effectively and review the output
- [references/how-to-read-repository-assessment-reports.md](references/how-to-read-repository-assessment-reports.md) - framing guidance for socializing detailed reports
- [references/](references/) - assessment guidance for architecture, design, readability, reliability, testability, complexity, recurring risks, and application archetypes
