# Usage Guide

## How to trigger the skill

With the skill installed, Copilot will invoke it automatically when you ask to assess, review, evaluate, or audit a repository. Just ask naturally from inside the target checked-out repository:

```
Assess this repository for engineering quality.
```

```
Review this codebase and give me an assessment report.
```

```
Audit this microservice — I'm particularly interested in architecture and testability.
```

```
Analyze this repo and produce a structured report at docs/assessments/.
```

You do not need to name the skill or paste any prompts. The skill handles the full workflow automatically.

---

## What the skill does

Once triggered, the skill:

1. Reads all reference guides (architecture, design, readability, reliability, testability, complexity)
2. Detects the primary application archetype (REST API, Kafka consumer, Camunda workflow, batch job, etc.)
3. Reads the code in depth — all service and domain classes, controllers, error handling, and representative tests
4. Runs mandatory named checks: anemic domain model, architecture layer evidence, framework selection, type-system bypass/runtime interpreter, static analysis suppression, and high-maintenance readability
5. Drafts and cross-checks ratings across six dimensions for internal consistency
6. Writes the final report to `docs/assessments/<repo-name>-assessment.md`

---

## The six assessment dimensions

| Dimension | What it covers |
|---|---|
| **Architecture** | Layer separation, module boundaries, archetype-appropriate structure |
| **Design** | Domain model richness, design patterns, invariant enforcement |
| **Readability** | Clarity, naming, intent communication, self-documenting structure |
| **Reliability** | Exception handling, failure modes, defensive construction |
| **Testability** | Whether the *production design* enables simple, isolated tests |
| **Complexity** | Cognitive load, method size, coupling, accidental vs inherent complexity |

Each dimension is rated **Strong**, **Adequate**, **Concerning**, or **Weak** with real code evidence.

---

## Recommended workflow

### 1. Open the target repository

Run the skill from inside the checked-out repository. The skill inspects the local file system directly.

### 2. Trigger the assessment

Ask Copilot to assess the repository. See example prompts above.

### 3. Let the skill inspect the code first

The skill reads the reference guides and code before writing anything. This is by design — do not interrupt or redirect it during the inspection phase.

### 4. Challenge shallow findings

If the first pass is weak, follow up with prompts like:

- Show stronger evidence for the architecture concerns.
- Which findings are structural versus local?
- What does this repo reveal about design-for-testability?
- Which code examples are strongest candidates for future standards?
- Where is the complexity inherent versus accidental?

### 5. Review the output

Before using the report as input to a later orchestrator or standards process, validate:

- it found recurring patterns rather than isolated trivia
- it used real code evidence with exact class names
- it captured both strengths and weaknesses
- it distinguished systemic versus local issues
- the archetype detection makes sense for the codebase

---

## Recommended repo assessment sequence

The skill follows this sequence automatically:

1. Identify archetype and context
2. Review package and module structure
3. Inspect representative flow paths
4. Inspect key design hotspots
5. Inspect exception and failure handling
6. Inspect representative tests
7. Draft ratings and run cross-dimension consistency checks
8. Complete the assessment template
9. Record top recurring risks
10. Record strongest examples for future standards

---

## Good pilot usage

Start with 3 to 5 representative repositories:

- one relatively healthy repo
- one average repo
- one painful or complex repo
- more than one archetype if possible

---

## What not to do

- Do not use this to grade developers.
- Do not treat the current repo patterns as accepted standards.
- Do not overgeneralize from one dramatic class.
- Do not let Copilot act as the sole authority.
- Do not convert findings directly into enforcement rules without later validation.
