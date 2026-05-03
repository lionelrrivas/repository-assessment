# Complexity Dimension

Assess the amount of cognitive and structural difficulty introduced by the code.
Focus on branching, dependency load, state management, duplication, incidental complexity, and whether the design amplifies complexity beyond what the problem domain requires.

## Positive signals
- methods are reasonably focused
- control flow is manageable
- classes have understandable dependency sets
- decomposition reduces cognitive load
- domain complexity is represented clearly rather than amplified

## Concerning signals
- large methods with many branches
- deeply nested logic
- boolean flags or parameter combinations controlling behavior
- output argument anti-pattern: readers must track which parameters serve as outputs and mentally simulate the mutation chain, increasing cognitive load; methods with multiple output parameters are particularly taxing; report in this dimension only when recurring — isolated instances are a readability or design concern, not a complexity concern in isolation
- excessive constructor dependencies
- duplicated decision logic
- accidental complexity created by design decisions rather than domain need
- runtime interpreters, generic evaluators, or string-driven dispatch layers built over a closed typed model
- service classes absorbing logic that belongs in a richer domain model — recognizable as large, procedural methods that manipulate data-only types
- long parameter lists as a substitute for a missing domain concept
- duplicated null checks, type checks, or conditional flows at multiple call sites because no shared abstraction exists
- `@SuppressWarnings` annotations suppressing Sonar cognitive complexity rules (`java:S3776`, `squid:S3776`) or other quality gates in handwritten production code — these are active, team-documented decisions to silence the tooling after complexity thresholds were breached; they do not fix the complexity and mask future degradation as the method grows

## Reviewer questions
- Is the complexity inherent to the domain, or created by weak design?
- Are there large methods, branching explosions, or excessive dependencies?
- Is complexity being reduced, or merely moved around?
- Are the most complex methods complex because the business problem is hard, or because the design has no place to put the logic?
- Are there `@SuppressWarnings` annotations or `// NOSONAR` comments suppressing static analysis rules, especially cognitive complexity? Each one is an explicit acknowledgement that the configured threshold was breached and a decision not to address it.

## Calibration: complexity as a downstream effect of design

**A critical calibration rule**: when Design is Concerning or Weak, expect Complexity to reflect the structural burden being pushed into service and utility code. Complexity and Design are often co-causes of the same root problem — an anemic domain model.

When the domain model is anemic, behavior gets displaced into service classes as long, procedural methods. This is not a complexity problem independent of design — it is a design problem expressing itself as complexity. When you find this pattern, name it in both dimensions and connect them explicitly.

Signs that complexity is design-rooted:
- Service methods are long because they are doing what a richer domain type would do for itself
- The same conditional logic appears in multiple service methods because no shared abstraction captured the rule
- Methods accept many parameters because no domain concept groups those values
- Cognitive load is high primarily because the reader must mentally simulate field manipulation across multiple classes rather than follow meaningful method calls on coherent objects

In these cases, rating Complexity without noting the design root cause leaves the finding incomplete. Note it explicitly: "The complexity in `<ClassName>` is a downstream effect of an anemic domain model — see Design dimension."

## Rating cap for suppressed core complexity

If a handwritten production method on the main change surface suppresses
`@SuppressWarnings("java:S3776")`, Complexity should not be rated Adequate
unless the assessor can show both of the following:
- the method is peripheral to day-to-day maintenance
- the suppression is not hiding structural complexity

Suppressions in core handlers, primary execution paths, runtime interpreters,
or other high-maintenance classes are direct evidence of complexity. The
threshold was already exceeded; the suppression only stops the tool from
reporting future growth.

If the method is complex because the design bypassed available typed models or
framework capabilities, treat that complexity as accidental rather than
inherent, and connect it to Design or Architecture.
