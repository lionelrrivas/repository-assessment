# Reliability Dimension

Assess how well the code handles failure, preserves correctness, and behaves predictably under non-happy-path conditions.
Focus on exception handling, null handling, validation placement, failure boundaries, retry/recovery semantics, and whether business failures and technical failures are handled intentionally.

## Positive signals
- exception boundaries are intentional and understandable
- failures preserve useful context
- business failures and technical failures are treated appropriately
- validation is performed close to where it belongs — ideally enforced by the type itself at construction
- retry/recovery semantics are explicit when relevant
- domain types can only be constructed in a valid state — invalid input fails fast at the boundary, not deep in business logic

## Concerning signals
- swallowed exceptions
- generic catch blocks with weak intent
- technical failures leaking across boundaries without translation or context
- unclear retry, dead-letter, fallback, or compensation behavior
- brittle null-heavy designs
- validation strategy that is scattered or inconsistent
- validation that is caller-dependent — every caller must remember to validate before use because the domain type itself does not enforce its invariants
- domain types that can be constructed in an invalid state without any error signal
- output argument anti-pattern — methods that mutate input parameters to communicate a result instead of returning one create invisible side effects; callers passing shared or reused objects may receive unexpected state changes; implicit ordering dependencies (the passed object is only valid after the call) spread silently across call sites; particularly risky in async or message-driven flows where aliasing and ordering are harder to reason about

## Reviewer questions
- How are failures handled for this app type?
- Are exception boundaries intentional and understandable?
- Are business failures and technical failures treated distinctly?
- Are retries, dead-letter flows, compensations, or fallback behaviors explicit where relevant?
- Are validation and null handling placed sensibly?
- Can a domain type be constructed in an invalid state? If so, is validation guaranteed to run before use — or is that assumption spread across every call site?

## Calibration: reliability as a downstream effect of design

**A critical calibration rule**: scattered validation and caller-dependent correctness are design problems with reliability consequences. They are not primarily a reliability problem — they are a *design* problem that makes reliability fragile.

When domain types carry no constructor validation, any caller can bypass validation by constructing the type without it. Reliability then becomes dependent on external discipline across every call site, rather than being enforced structurally. This is a systemic risk.

When you find this pattern:
- Report it in **Design** as an anemic domain model finding (the type makes no promise about its own validity)
- Report it in **Reliability** as a systemic risk (correctness depends on scattered external discipline, not structural enforcement)
- Connect the two explicitly: "The reliability risk here is rooted in the design — see Design dimension."

Do not rate Reliability as Adequate when domain types can be constructed in invalid states and the codebase relies on callers to perform validation separately. That is a systemic risk, not an incidental one.

For message-driven and Kafka/MQ archetypes, additionally assess:
- Are retry and dead-letter behaviors intentional and explicit?
- Is there evidence of duplicate or idempotency handling where the archetype requires it?
- Are deserialization errors handled at the listener boundary rather than propagating into business logic?
