# Architecture Dimension

Assess whether the repository exhibits clear structural boundaries and proper separation of concerns appropriate to its archetype.

**Important calibration**: The presence of controllers, services, and repositories does not constitute evidence of good architecture. These are naming conventions. Evidence of good architecture is *behavioral separation* — each layer does only what it should, and responsibilities are not collapsed across layers, regardless of what the classes are called.

## Positive signals
- responsibilities are clearly separated *in behavior*, not just in naming
- orchestration is separated from business rules
- transport, workflow, or listener concerns do not dominate business logic
- external integration details are not leaking into core behavior
- structure helps the reader reason immediately about where a change belongs
- each layer could be read and understood independently without needing to understand the full stack

## Concerning signals
- boundaries exist only in naming, not in actual behavior placement
- orchestration, validation, mapping, persistence, domain decisions, and integration calls collapse into the same methods or classes
- framework-facing classes (controllers, delegates, listeners) take on too much business responsibility
- the codebase has no clear home for core business behavior — domain logic is spread across service methods
- service classes that appear focused by name are unfocused in behavior
- the domain "layer" consists only of data-carrying classes with no behavior — the architecture has a domain namespace but no domain layer in practice
- custom commodity infrastructure replacing standard framework components without an evident domain or compatibility constraint: for example, custom consumer lifecycle management where Spring Cloud Stream fits the archetype, custom dynamic SQL builders where Spring Data applies, or custom expression evaluators against message payloads where typed message contracts would suffice

## Reviewer questions
- Are responsibilities clearly separated in behavior, not just class names?
- Is transport/workflow/listener logic mixed with business logic in the same methods?
- Are orchestration and domain decisions collapsed into the same classes?
- Are framework concerns dominating the design?
- If you removed all framework and infrastructure code, would a meaningful domain model remain?
- Where does business behavior live? If the answer is "the service layer, inside large methods", that is an architecture concern.
- Does the codebase build custom commodity infrastructure for problems that standard Spring framework components already solve? Check whether the detected archetype has a canonical Spring solution, whether any evident domain or compatibility constraint justifies the bypass, and whether classpath evidence merely corroborates rather than proves the finding.
- If one framework entry model appears insufficient, does the framework also offer a supported functional, declarative, or programmatic model that satisfies the same requirement? Do not let the limits of one annotation or API surface stand in for the capabilities of the framework as a whole.

## Adequate vs. Concerning: calibrating the core handler check

A clean listener, factory, configuration class, and well-named exception types are positive signals — but they are **peripheral evidence**. The listener delegates; it does not decide. The factory routes; it does not process. Architectural quality is determined by what happens in the core handlers where real business processing runs.

**Concerning threshold:** If the majority of primary use-case handlers combine three or more of these architectural concerns in a single class or primary execution method — orchestration, domain retrieval, transformation/mapping, external integration, business decision-making, persistence — Architecture is **Concerning**. This is true even when the boundary layer (listener, config, factory) is clean. The clean boundary shows what is possible; the core handlers show what the architecture actually delivers under load.

**Adequate threshold:** Adequate applies when the risks are present but the core handlers largely stay within a single layer's responsibility — they may be large or procedural, but they do not cross into persistence, direct integration orchestration, and business decisions all at once. A clear improvement path exists.

**The test:** If you removed the listener, factory, and configuration entirely, what would the architecture look like? If the remaining service classes each collapse multiple architectural concerns, the architecture is Concerning regardless of the quality of what surrounds them.
