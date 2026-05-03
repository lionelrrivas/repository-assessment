# Testability Dimension

Assess how well the production design supports clear, focused, maintainable tests.

**Do not assess test presence or test count. Assess whether the production design structure enables behavior to be verified simply, clearly, and in isolation.** A codebase where developers have written many tests is not necessarily testable — it may mean developers are working harder than good design would require.

## Positive signals
- important behavior can be tested with focused setup
- tests are readable and aligned to behavior, not to implementation mechanics
- dependency boundaries make isolation reasonable without excessive mocking
- both unit and integration tests have clear, distinct roles
- tests reveal intent rather than ceremony — setup is minimal relative to the behavior under test
- the most consequential classes are the easiest to test, not the hardest

## Concerning signals
- excessive mocking required for simple behavior (mocking more than 2-3 collaborators for a single behavior)
- large, verbose setup for small behavior — the test scaffolding exceeds the behavior under test
- tests are brittle because they depend on internal implementation details rather than observable behavior
- production seams are weak, unclear, or missing — tests work around a design that doesn't support them
- test complexity appears caused by tangled production design, not by genuine domain complexity
- output argument anti-pattern: tests of methods that mutate parameters must construct input objects, invoke the method, and inspect state after the call rather than asserting on a return value; this adds ceremony and makes tests harder to read; raise as a testability concern when it recurs across consequential service classes — a single occurrence is not a signal worth noting
- the most consequential and complex classes have tests that are interaction-only (`verify(mock).method(...)`) with no behavioral assertions
- `ReflectionTestUtils.setField()` needed to inject test values — a signal of field injection and poor constructor testability
- mock data or test fixtures in production code (e.g., a `@Component` that builds fake payloads) — the design lacked a clean test seam and a workaround was shipped instead
- tests of complex logic require constructing large, verbose domain object graphs because a meaningful abstraction is missing

## Reviewer questions
- Can important behavior be tested with small, focused setup?
- Are tests complex because the business problem is genuinely hard, or because the design is tangled?
- Is excessive mocking required for simple behavior?
- Do test patterns reveal production design problems?
- Can the most consequential domain logic be verified behaviorally, or only by checking that mocks were called?
- Are there signs that tests are working around the design rather than exercising it cleanly?

## Calibration: testability must reflect design quality

**A critical calibration rule**: if Design is Concerning or Weak, testability should almost never be rated Adequate or Strong without explicit justification. The two dimensions are structurally linked — anemic domain models, blurred boundaries, and service classes that mix responsibilities all create testability friction in exactly the areas where testing matters most.

A common failure mode: clean tests exist for simple, isolated utility classes and thin wrappers, while the most consequential business logic lives in complex service classes that resist behavioral testing. This creates a false impression of adequate testability.

Ask specifically: **Is the test suite performing better than the design deserves?**

Signs the answer is yes:
- Clean tests exist only for the simplest, most isolated classes
- The most consequential and complex classes have tests that are interaction-only — verifying mock calls, not behavior
- `ReflectionTestUtils.setField()` is needed to inject test values
- Mock data or test fixtures live in production code
- Tests of complex logic require constructing large domain object graphs because the right abstraction was never built

When this pattern is present, rate Testability as **Concerning** even if individual tests look clean. In the report, be direct: name which classes have good tests, name which classes resist good tests, and explain that the constraint is the production design — not developer skill or effort.

