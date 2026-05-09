# Usage Guide

Repository Assessment works best when you use it as a repeatable evidence-gathering workflow, not a one-off audit. This guide focuses on how to trigger the skill effectively, how to review the output, and how to move from detailed findings to the companion synthesis step and then into useful standards work.

## When to use it

Use the skill when you want to understand the engineering health of a checked-out Java/Spring Boot repository and turn that assessment into better standards, learning plans, or refactoring priorities.

It is especially useful when you want to:

- assess a repository for engineering quality
- compare multiple repositories before drafting standards
- understand recurring design or architecture risks
- gather evidence for coaching or learning recommendations

## How to trigger the skill

With the skill installed, Copilot will invoke it automatically when you ask to assess, review, evaluate, analyze, or audit a repository. Ask naturally from inside the target checked-out repository:

```
Assess this repository for engineering quality.
```

```
Review this codebase and give me an assessment report.
```

```
Audit this microservice - I'm particularly interested in architecture and testability.
```

```
Analyze this repo and produce a structured report at docs/assessments/.
```

You do not need to name the skill or paste a long system prompt. The skill handles the workflow automatically.

## What the skill does

Once triggered, the skill:

1. Reads the reference guides before interpreting repository evidence.
2. Detects the primary application archetype.
3. Inspects the repository structure and representative flow paths.
4. Reviews service, domain, controller/listener, error-handling, configuration, and representative test code.
5. Runs mandatory named checks for recurring risk patterns and rating consistency.
6. Writes the final report to `docs/assessments/<repo-name>-assessment.md`, including a normalized `Synthesis Input Summary`.

That detailed report is usually not the final artifact you want to share broadly. In most multi-repository workflows, it becomes the input to the companion **cross-repository-engineering-synthesis** skill, which produces a more readable, cross-repository output for standards discussions and leadership communication.

## The six assessment dimensions

| Dimension | What it covers |
|---|---|
| **Architecture** | Layer separation, module boundaries, archetype-appropriate structure |
| **Design** | Domain model richness, design patterns, invariant enforcement |
| **Readability** | Clarity, naming, intent communication, self-documenting structure |
| **Reliability** | Exception handling, failure modes, defensive construction |
| **Testability** | Whether the production design enables simple, isolated tests |
| **Complexity** | Cognitive load, method size, coupling, accidental versus inherent complexity |

Each dimension is rated **Strong**, **Adequate**, **Concerning**, or **Weak** and is backed by concrete code evidence.

## Recommended workflow

### 1. Start with representative repositories

If your real goal is standards creation, begin with 3 to 5 repositories that give you a fair sample:

- one relatively healthy repository
- one average repository
- one painful or high-friction repository
- more than one archetype if possible

### 2. Run the assessment from inside the target repository

The skill inspects the local file system directly, so run it from the checked-out repository you want assessed.

### 3. Let the skill inspect before redirecting it

The skill reads reference material and repository code before writing the report. That inspection phase is deliberate. Let it gather evidence before trying to steer the conclusions.

### 4. Challenge shallow findings

If the first pass feels weak, follow up with prompts like:

- Show stronger evidence for the architecture concerns.
- Which findings are structural versus local?
- What does this repo reveal about design-for-testability?
- Which examples are the strongest candidates for future standards?
- Where is the complexity inherent versus accidental?

### 5. Review the report for signal quality

Before using the report downstream, check that it:

- finds recurring patterns rather than isolated trivia
- uses real code evidence with exact class names
- captures both strengths and weaknesses
- distinguishes systemic issues from local issues
- identifies the archetype sensibly
- keeps the `Synthesis Input Summary` consistent with the final ratings
- uses risk tags that are supported by the evidence

If a reviewer finds the report difficult to understand, ask Copilot to explain the confusing sections, restate findings in plainer language, trace a claim back to its code evidence, or suggest focused follow-up questions.

Try prompts like:

- Explain the Design section in plainer language.
- Show me the strongest code evidence behind this finding.
- Which findings here look like standards candidates versus repository-specific cleanup?
- Summarize this report for an engineering manager who is new to this workflow.
- What follow-up questions should I ask to tell whether this problem is systemic or local?

### 6. Move from assessment to synthesis, then to standards carefully

Do not turn one repository's report directly into organization-wide policy. Review multiple assessments first, then run the companion **cross-repository-engineering-synthesis** skill to turn those detailed reports into a more readable synthesis. Use that synthesis to identify standards candidates, learning recommendations, and repository-specific remediation.

### 7. Prefer synthesis for broader audiences

Single-repository assessment reports are intentionally detailed and can feel overwhelming outside the immediate review group. For leaders, standards authors, or wider team communication, the companion **cross-repository-engineering-synthesis** skill usually produces the better artifact to share.

## Using the output responsibly

The report is intentionally detailed because it is diagnostic evidence. That does **not** mean every finding should become a rule, a public talking point, or a team-wide mandate.

Repository state is shaped by more than individual skill. Legacy constraints, delivery pressure, evolving ownership, missing examples, and inconsistent standards often leave visible marks in the code. Read the report as evidence about the system and the support a team may need, not as a verdict on the people involved.

If your organization also has audit or compliance expectations, keep those in a separate standards or controls baseline. Examples include approved platform versions such as Java 25 or Spring Boot 4, required pull request approval counts, and required repository files such as `README.md`. Repository Assessment can supply evidence that helps you shape those requirements, but it is not the source of truth for enforcing them.

Use the output to:

- identify recurring risks worth standardizing
- separate repository cleanup from broader standards work
- spot learning opportunities and coaching needs
- identify where teams need clearer examples, pairing, workshops, checklists, or refactoring time
- ground engineering conversations in evidence instead of anecdotes

In most cases, the best way to do that at scale is to move from single-repository assessments into the companion **cross-repository-engineering-synthesis** workflow before broad sharing or final standards drafting.

### Healthy response to uncomfortable findings

When a report surfaces painful patterns:

- start with pattern-level questions, not person-level judgments
- ask which issues are systemic, inherited, or repeated across repositories
- turn repeated findings into enablement actions such as standards, reference examples, and learning plans
- keep raw assessment reports out of grading and performance conversations

For broader sharing, pair the report with [references/how-to-read-repository-assessment-reports.md](references/how-to-read-repository-assessment-reports.md). That framing note helps skeptical engineers and managers interpret the detail correctly.

## What not to do

- Do not use the report to grade developers.
- Do not use the findings as evidence in performance reviews.
- Do not treat current repository patterns as accepted standards.
- Do not overgeneralize from one dramatic class or one painful repository.
- Do not let Copilot act as the sole authority.
- Do not convert raw findings directly into enforcement rules without cross-repository validation.
