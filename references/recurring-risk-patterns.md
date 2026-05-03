# Recurring Risk Patterns

Look specifically for these issues when present:

- blurred responsibility boundaries appropriate to the repository archetype
- transport, controller, listener, workflow, delegate, handler, or adapter logic mixed with business logic
- orchestration mixed with business rules
- mapping, validation, persistence, integration, and domain decisions collapsed into the same classes
- framework-specific classes taking on too much business responsibility
- god classes
- utility-heavy design where domain behavior or focused collaborators should exist
- argument-driven behavior, including null, flag, or parameter combinations that significantly alter behavior
- output argument anti-pattern — methods that mutate input parameters to carry results out rather than returning a value (distinct from argument-driven behavior, which controls branching); most consequential when service methods mutate DTO or entity arguments, multiple parameters are mutated, or shared objects are threaded across layers; do not flag obvious mutator APIs (`add`, `append`, `put`), builder patterns, or framework-required mutation (Jackson deserialization, JPA entity population, Spring model/context objects, domain methods whose purpose is a legitimate state transition on `this`)
- excessive constructor dependencies suggesting weak cohesion or overloaded responsibilities
- large methods with multiple concerns
- duplicated decision logic across services, handlers, delegates, consumers, or producers
- weak exception boundaries
- swallowed exceptions
- technical failures and business failures treated indistinctly
- retry, compensation, dead-letter, fallback, or recovery behavior that is hidden, scattered, or unclear
- weak idempotency or duplicate-handling design where message or workflow processing makes this important
- vague class, method, and variable names that hide business intent
- improper use of Java language features where it materially affects correctness, maintainability, or clarity
- type-system bypass in core processing: converting typed payloads or closed schemas into JSON, raw maps, or `Object` values, then recovering meaning through strings, reflection, or DSLs; this can trigger Architecture, Design, Readability, Complexity, and Reliability findings
- missing or incorrect equals/hashCode implementations where value semantics matter
- misuse of inheritance, static state, Optional, exceptions, mutability, or collection semantics where it creates engineering risk
- tests with excessive mocking caused by poor design seams
- overly complex tests that reveal tangled production responsibilities
- tests that are difficult to understand because setup, orchestration, and assertions are obscured by production design issues
- architecture or design patterns that make focused unit tests unnecessarily difficult
- custom commodity infrastructure replacing standard framework components where they fit the archetype — for example, custom consumer lifecycle management, SQL builders, or message expression evaluators; flag only when all three are true: the archetype matches, custom commodity infrastructure exists, and no evident domain or compatibility constraint justifies the bypass
- static analysis suppressions in handwritten production code (`@SuppressWarnings("java:S####")`, `@SuppressWarnings("squid:S####")`, `// NOSONAR`) that silence quality gates rather than address the underlying issue, particularly cognitive complexity suppressions (`S3776`) which prevent future degradation from being surfaced
