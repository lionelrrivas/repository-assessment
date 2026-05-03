# Readability Dimension

Assess how easily a competent developer can understand the code's intent, behavior,
and structure. Focus on naming, clarity, discoverability of side effects, and
cognitive load.

## Positive signals
- names reveal intent and business meaning
- methods are focused and understandable
- side effects are discoverable
- control flow is readable at a normal working pace
- code structure reduces mental simulation

## Concerning signals
- vague or misleading names
- long methods with mixed concerns
- hidden side effects
- output argument anti-pattern — methods that mutate input parameters instead of returning a value; call sites reveal nothing about the mutation (`populateReport(report)` gives no visual indication that the caller's object will be modified), forcing the reader to consult the method signature to understand data flow direction
- dense code requiring heavy context switching
- runtime interpreters or type-erased evaluators where the reader must infer meaning from string keys, path expressions, or `Object` values instead of named typed methods
- comments compensating for confusing code
- comments that restate what the code does rather than explaining constraints,
  decisions, or non-obvious intent — comment density is not evidence of readability;
  it can be evidence of the opposite

## Reviewer questions
- Do names reflect business meaning and behavior?
- Can a reader understand the method without mentally executing it line by line?
- Are side effects obvious? Are any parameters being mutated to carry results out rather than returned?
- Is the code easy to follow for normal maintenance work?
- In the classes where most maintenance work will happen, can a new developer
  understand the business intent without reading callers, third-party libraries, or
  the implementation details of collaborators?
- Do dominant maintenance classes communicate intent through named typed operations, or do readers have to decode string keys, path expressions, or `Object`-typed intermediate values to understand what is happening?

## Calibration: assess readability where it matters most

A common trap: utility classes and thin wrappers read cleanly, creating an Adequate
impression. Meanwhile, the orchestration layer, the most complex domain logic, and
the highest-traffic classes are genuinely hard to follow.

Readability must be weighted toward the classes where consequential maintenance work
happens. If those classes require significant mental simulation, force the reader to
understand the mechanism before the intent, or rely on comments to explain what the
code should communicate on its own — the rating should be Concerning, regardless of
how clean the simpler classes are.

Ask specifically:
- Which classes will developers spend the most time reading and changing?
- Can those classes be understood at a normal working pace?
- If the answer is no for those classes, do not let well-named helpers or clean data
  objects offset the rating.

## "Understandable with effort" is not Adequate

Reviewers often rationalize a hard-to-read core class with phrases like "readable once
you spend time with it" or "requires effort but understandable." For the dominant
maintenance classes, that is not an Adequate readability signal — it is the finding.

Adequate readability means a competent maintainer can understand intent and control
flow at a normal working pace. If a class requires line-by-line mental simulation, or
if the reader must first understand the mechanics of a runtime interpreter, generic
dispatcher, or framework workaround before they can understand the business intent, the
rating should reflect that friction directly.

**Peripheral vs. core:** Entry-point adapters (listeners, controllers), individual mapper classes, and well-designed model types near the system boundary often read cleanly — they have focused responsibilities and little branching. These are *peripheral* to where maintenance work concentrates. Core orchestration classes, event or request processors, and handler implementations are where developers spend most of their reading and editing time. If the peripheral classes read well but the core classes are dense and mixed-concern, the rating reflects the core. The peripheral classes are evidence of what is *possible* with good decomposition — not evidence that the overall readability is adequate.

## The comment-restatement signal

When code is accompanied by comments that say what the code does — not why — treat
this as a readability risk, not a readability strength. It means the code is not
communicating its intent on its own, and the comments are filling that gap.

A well-named method call needs no comment above it. If a comment is needed to explain
a line of code, that is a signal to improve the code, not to keep the comment.
Comments earn their place by explaining non-obvious constraints, business rules, or
decisions — not by narrating the execution sequence.
