# Repository Assessment Summary

## Repository Context
- Repository name:
- Purpose:
- Primary application archetype:
- Secondary archetype patterns, if any:
- Relevant architectural context:
- Reviewer confidence in overall assessment: High / Medium / Low

## Executive Summary
Write a short summary suitable for leadership or socialization. Focus on the most important recurring engineering patterns, the most significant risks, and the most important strengths. Do not praise a class, mechanism, or extension point that the final ratings identify as a core weakness.

## Overall Engineering Profile
Write a concise narrative summary of the repository's engineering profile. Focus on recurring patterns rather than isolated issues. Keep this section aligned with the final dimension ratings.

## Dimension Assessments

### 1. Architecture
- Level:
- What good separation of concerns looks like for this archetype:
- Strengths:
- Risks:
- Evidence:
- Representative code snippets:
- Why it matters:
- Better direction:
- Example improvement:
- Confidence:
- Likely cause category:

### 2. Design
- Level:
- Strengths:
- Risks:
- Evidence:
- Representative code snippets:
- Why it matters:
- Better direction:
- Example improvement:
- Confidence:
- Likely cause category:

### 3. Readability
- Level:
- Strengths:
- Risks:
- Evidence:
- Representative code snippets:
- Why it matters:
- Better direction:
- Example improvement:
- Confidence:
- Likely cause category:

### 4. Reliability
- Level:
- Strengths:
- Risks:
- Evidence:
- Representative code snippets:
- Why it matters:
- Better direction:
- Example improvement:
- Confidence:
- Likely cause category:

### 5. Testability
- Level:
- Key question: does the *production design structure* enable behavior to be tested simply, clearly, and in isolation — or are tests working around the design?
- Strengths:
- Risks:
- Evidence:
- Representative code snippets:
- Why it matters:
- Better direction:
- Example improvement:
- Confidence:
- Likely cause category:
- Cross-dimension note: if Design or Architecture are Concerning, explain here whether those problems are creating testability friction in the most consequential areas.

### 6. Complexity
- Level:
- Strengths:
- Risks:
- Evidence:
- Representative code snippets:
- Why it matters:
- Better direction:
- Example improvement:
- Confidence:
- Likely cause category:

## Cross-Dimension Consistency Check
Before finalizing, verify that related dimension ratings are consistent with each other. If any of these relationships diverge, provide explicit justification.

| Relationship | Expected pattern | Actual consistency | Justification if divergent |
|---|---|---|---|
| Design ↔ Testability | Concerning Design → Testability should be Concerning unless production design provably enables simple isolated tests for complex behavior | | |
| Architecture ↔ Design | Concerning Architecture → Design likely shows anemic models or behavior displaced into service layer | | |
| Design ↔ Readability | Concerning Design in core processing classes often implies readability friction in the same hotspots | | |
| Design ↔ Complexity | Concerning Design → Complexity likely reflects procedural services absorbing displaced behavior | | |
| Reliability ↔ Design | Weak domain invariants or type-system bypass in core processing → Reliability at risk from scattered validation or silent runtime misses | | |

After any rating revision, update the Executive Summary, Overall Engineering Profile, Top Recurring Engineering Risk Patterns, Likely Underlying Skill or Standards Gaps, Recommended Candidate Examples for Engineering Standards, and Final Notes so they reflect the final ratings and contain no stale praise or contradictory language.

## Top Recurring Engineering Risk Patterns
List the 3 to 7 highest-signal recurring patterns found across the repository.
For each one, include:
- Pattern name
- Why it is high risk
- Evidence
- Scope: isolated / local but repeated / repository-wide / architectural-systemic
- Better direction

## Likely Underlying Skill or Standards Gaps
List the most likely engineering capability or standards gaps suggested by the repository.
For each one, include:
- Gap
- Evidence supporting the inference
- Confidence

## Recommended Candidate Examples for Engineering Standards
Identify which findings would make good examples for future engineering standards.
For each one, briefly describe:
- the problematic pattern
- why it is worth standardizing
- what better should look like
- exact code snippet(s) worth reusing later

## Synthesis Input Summary
Complete this section after the assessment has been finalized. Keep it concise, structured, and consistent because it will be used as input for cross-repository synthesis. Do not introduce new findings here; summarize the final assessment above.

### Repository Signal
- Repository name:
- Primary application archetype:
- Secondary archetype patterns, if any:
- Overall reviewer confidence: High / Medium / Low
- Architecture level: Strong / Adequate / Concerning / Weak
- Design level: Strong / Adequate / Concerning / Weak
- Readability level: Strong / Adequate / Concerning / Weak
- Reliability level: Strong / Adequate / Concerning / Weak
- Testability level: Strong / Adequate / Concerning / Weak
- Complexity level: Strong / Adequate / Concerning / Weak

### Normalized Risk Pattern Tags
List only tags supported by the evidence in this assessment. Use kebab-case. Prefer the common tags below when they fit; add a new tag only when none of the common tags accurately describes the finding.

Common tags:
- anemic-domain-model
- controller-business-logic
- listener-business-logic
- god-service
- oversized-core-handler
- mixed-layer-responsibilities
- framework-bypass
- custom-commodity-infrastructure
- type-system-bypass
- runtime-interpreter
- stringly-typed-dispatch
- weak-domain-invariants
- scattered-validation
- swallowed-exception
- weak-error-semantics
- silent-failure-mode
- static-analysis-suppression
- coverage-exclusion-risk
- reflection-based-tests
- excessive-mocking
- interaction-heavy-tests
- low-behavioral-test-coverage
- untested-core-behavior
- procedural-service-design
- helper-utility-overuse
- unclear-api-semantics
- persistence-leakage
- external-integration-coupling

Selected tags:
- 

### Standards Candidates
List the strongest findings that should be considered for future engineering standards. Each item should be evidence-backed and phrased as a standard area, not as a repository-specific complaint.

#### Candidate 1
- Standard area:
- Evidence repositories/classes:
- Severity: High / Medium / Low
- Why it should become a standard:
- What better should look like:
- Reusable example: yes / no

#### Candidate 2
- Standard area:
- Evidence repositories/classes:
- Severity: High / Medium / Low
- Why it should become a standard:
- What better should look like:
- Reusable example: yes / no

### Learning Recommendation Signals
List the most important learning needs suggested by the assessment. Prefer capability-based language over blame-based language.

#### Learning Signal 1
- Capability gap:
- Evidence:
- Suggested learning format: discussion / workshop / kata / pairing / reference standard / code review checklist
- Priority: High / Medium / Low

#### Learning Signal 2
- Capability gap:
- Evidence:
- Suggested learning format: discussion / workshop / kata / pairing / reference standard / code review checklist
- Priority: High / Medium / Low

### Cross-Repository Synthesis Notes
Use this space for short notes that will help a later synthesis agent interpret this repository fairly. Mention constraints, uncertainty, unusually strong examples, or cautionary examples.
- 

## Final Notes
Call out any important caveats, missing context, or constraints that may affect the assessment.
