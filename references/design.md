# Design Dimension

Assess how well responsibilities are assigned and modeled.
Focus on object-oriented design quality, cohesion, abstraction quality, dependency
direction, behavior placement, and whether the code reflects meaningful domain concepts.

## Positive signals
- classes have focused responsibilities
- behavior is placed near the concept it belongs to
- abstractions simplify understanding
- dependencies reflect meaningful collaboration
- the model expresses the business problem clearly
- core domain types enforce their own invariants at construction
- Java language features (records, sealed classes, constructor validation) are
  used where they fit the design intent

## Concerning signals
- god classes
- utility-heavy design where richer object behavior should exist
- argument-driven methods based on flags, nulls, or parameter combinations
- output argument anti-pattern — methods that mutate their parameters to carry results out instead of returning a value; this signals misplaced behavior, weak encapsulation, and procedural manipulation of data-carrying classes; it often accompanies an anemic domain model — an external method "fills in" a domain object that should derive or construct the result itself; when recurring in service classes, it is the design problem to name, not merely a readability inconvenience; do not flag obvious mutator APIs, builder patterns, or framework-required mutations (Jackson deserialization, JPA entity population, Spring context objects, or domain methods that legitimately transition state on `this`); distinguish from argument-driven behavior, where parameters control which branch executes — output arguments communicate results through mutation rather than return
- weak cohesion
- abstractions that add indirection without payoff
- duplicated decision logic across classes
- framework-shaped classes with little design intention
- core processing classes that erase available types into `Object`, raw maps, JSON strings, or generic expression contexts and then rebuild behavior through path expressions, operator strings, reflection, or runtime DSLs
- **anemic domain models** — data-carrying classes that have no behavior, exist
  only as getters and setters, and rely on external classes to perform operations
  that belong to the model itself
- dedicated validation classes or utilities that exist because the model being
  validated is too weak to enforce its own invariants
- mutable data classes where an immutable value type (such as a Java record)
  would be more appropriate and safer

## Reviewer questions
- Does each class have a focused purpose?
- Is behavior located where it naturally belongs?
- Are abstractions helping or merely adding layers?
- Are methods branching because the model is weak?
- Does the code reflect meaningful domain concepts?
- Do the core data-carrying classes have any behavior, or are they pure data
  bags? If a separate class exists to validate or operate on them, why doesn't that
  behavior live in the model itself?
- Could any data-carrying class be an immutable value type or Java record?
  If not, is mutability intentional and necessary, or incidental?
- When you see a utility or helper class, ask what it is operating on. If it
  exists to compensate for a weak model, the finding belongs to the model, not the
  utility.
- Are any methods mutating their input parameters to carry results out rather than
  returning a value? If so, is there a domain type or return value that belongs here?
- Is a core processing class discarding available types and re-expressing the problem through `Object`, raw maps, JSON paths, reflection, or operator strings? If so, is the input really open-ended at runtime, or is the design bypassing a type system that could model it directly?

## The anemic domain model

**This is one of the most common and consequential design weaknesses in Java applications. Always check for it explicitly — do not rely on it surfacing incidentally.**

An anemic domain model is a class that carries data but has no meaningful behavior.
It typically appears as a collection of fields with getters and setters, no
constructor-enforced invariants, and no domain logic. Operations that should belong
to the model — validation, derivation, transformation — are instead pushed into
external service, utility, or helper classes.

This weakness is often invisible to reviewers who assess classes in isolation,
because each class appears focused. The weakness only becomes visible when you ask:
*where does the behavior that belongs to this type actually live?*

**Signs of an anemic model:**
- a separate validation class or method exists whose sole input is one of the core
  domain types, or accepts that type's fields as parameters
- helper methods elsewhere perform logic that reads like it belongs to the type
  (e.g., "get the effective identifier from this object", "normalize this object",
  "check if this object is in a valid state")
- the domain type can be constructed in an invalid state because no constructor
  validation exists — an external caller can omit required fields without detection
- the domain type is mutable in ways that are never intentionally needed — fields can
  be changed after construction without any domain justification

**The consequence for other dimensions:**
An anemic domain model displaces behavior into service classes, making services large, procedural, and difficult to test in isolation. It also means validation is dependent on every call site performing it correctly, which is a reliability risk. When you find this pattern, reflect it in Design and note its cascading effects on Testability, Reliability, and Complexity.

## Java language features as design signals

In Java 17+, certain language features signal good design when used appropriately:
- **Records** — appropriate for immutable value types where identity is defined by
  data, not reference. Compact constructors allow validation at construction time,
  eliminating the need for external validators. If a class is effectively a value
  object but is not a Record, ask why — mutability is often incidental.
- **Sealed classes/interfaces** — appropriate for closed type hierarchies where the
  set of variants is known and should be exhaustive. A good alternative to reflection-
  based or instanceof-chain polymorphism. Enables the compiler to enforce completeness
  of handling.
- **Constructor-enforced invariants** — any domain type that can only be valid in
  certain states should enforce those states at construction, throwing on invalid
  input rather than relying on an external validation pass.

When these features are absent where they would clearly fit, note it as a design gap and recommend them explicitly.
When they are used appropriately, note it as a strength.

## Type-system bypass / runtime interpreters

Look for core processing code that takes a closed, known input model and turns it
into generic JSON, raw maps, document contexts, or `Object` values, then uses
strings, operator names, reflection, or a DSL to recover meaning.

When you see this, ask: is the input truly open-ended at runtime, or is the code
bypassing a type system that could model the problem directly?

This often means a core class is acting as a runtime interpreter for a closed
message hierarchy, known schema, or finite set of variants.

Treat it as a design weakness when:
- contracts disappear into `Object` and unchecked casts
- changes move from compile-time failures to runtime failures
- core logic becomes procedural and string-driven
- readability and complexity worsen because the reader must simulate interpreter logic

Do not flag truly open-ended rule engines or user-authored logic, where runtime
programmability is the point. But when the schema is closed and known, generic
mapping layers and interpreters are usually a design weakness, not a strength.

## Ease of unit-test construction is not a design strength

A class being easy to instantiate in tests, having few framework dependencies, or not
being a Spring bean can be good for test setup — but that does not make it a strong
design. A parser, interpreter, or generic evaluator can be trivial to construct and
still be a weak abstraction if everything is `Object`, unchecked casts, and string-
driven dispatch.

Treat "easy to construct in tests" as a **Testability** observation unless the class
also exposes a coherent, typed abstraction with responsibilities that clearly belong
together.


## Interface-backed god classes: a common inflation trap

A polymorphic service interface can create a false impression of good design. The interface defines a clean behavioral contract — a well-named method, sensibly parameterized, appropriate for polymorphic dispatch. This *looks* like a design strength.

Design quality, however, is determined by what implements the interface, not by the interface itself. When the concrete implementations each carry 10 or more injected collaborators, own mixed concerns, and contain large methods, the interface is a dispatching layer in front of a set of god classes. The interface does not fix the underlying problem — it adds a layer of indirection that makes the problem less visible.

**How to check:**
- Find every concrete implementation of the interface
- Count constructor parameters and `@Autowired` field declarations in each
- 10+ injected dependencies: investigate method size, concern mixing, and whether the dependency set has a unifying purpose
- 15+: presumptively a god class unless collaborators are homogeneous and methods stay cohesive

**How to rate:**
- Do not credit the interface as a design strength until implementations are inspected
- If core-path or majority implementations are god classes, the interface finding is neutral at best — it reveals the dispatch structure but does not offset the implementation quality
- Credit the interface pattern only when the implementations behind it are also well-designed: focused responsibilities, cohesive dependencies, and methods that stay within a single concern

## Concerning vs. Weak: calibrating god class findings

A single god class is a Concerning finding — it affects that class's maintainability and testability in isolation, and targeted refactoring can address it.

When the god class pattern is **pervasive across all or most core processing handlers** — every handler has 10+ dependencies, every primary processing method is 100+ lines, the pattern is consistent rather than exceptional — the design is **Weak**. At that scale, the problem is the structural approach that produced the pattern, not individual class decisions. Fixing it requires reworking how responsibilities are organized across the entire processing layer, which is significant refactoring — not a few targeted improvements.

The existence of improvement steps (extract a coordinator, group mappers into collaborators) does not mean the design is Concerning rather than Weak. Every design problem has improvement paths. The question is whether improvement requires targeted fixes to individual classes or changing the structural approach to the entire processing layer. When every handler is a god class, the latter is true — the design is Weak. Do not use "I can describe how to fix it" as evidence for Concerning over Weak — that test confuses a describable path with an easy path. Weak design always has describable improvement paths; what makes it Weak is that those paths require reworking the entire structural approach rather than making targeted class-level changes.

Ask: *if a team wanted to fix the worst god class, would that address the pattern — or would the same structural forces immediately recreate the same shape in every other handler?* If the answer is the latter, the design is Weak.
