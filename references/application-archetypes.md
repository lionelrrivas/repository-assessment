# Application Archetypes

Use this reference when deciding what good separation of concerns looks like for the repository.

## REST API / Spring MVC
Assess boundaries between:
- controller/request handling
- application/service orchestration
- domain behavior
- persistence
- integration clients
- exception translation
- DTO mapping

Look for risks such as:
- controllers containing business logic
- services mixing orchestration, validation, mapping, persistence, and domain decisions
- repositories making business decisions
- transport concerns leaking into core logic

## Camunda workflow application
Assess boundaries between:
- workflow/process orchestration
- delegates/workers/task handlers
- domain services
- process variable mapping
- external integrations
- retry/error/compensation behavior
- engine concerns versus business logic

Look for risks such as:
- delegates mixing workflow variable handling, business logic, and integration code
- workflow engine concerns dominating the design
- compensation or retry logic hidden in business classes

## Kafka / MQ / Rabbit consumer
Assess boundaries between:
- listener/consumer adapter logic
- deserialization/parsing
- validation
- orchestration
- domain behavior
- downstream integration
- retry/dead-letter/error handling
- idempotency or duplicate handling where relevant

Look for risks such as:
- listener methods doing transport work, mapping, business rules, persistence, and recovery logic all at once
- duplicate handling missing or unclear where it matters
- technical failure handling mixed with business failure handling

**Framework selection guidance:** Spring Cloud Stream is the canonical Spring solution for this archetype.

Flag a framework selection risk when **all** of the following are true:
- The archetype matches a Spring Cloud Stream use case
- The codebase implements custom commodity infrastructure such as consumer lifecycle management, custom deserialization routing, or a custom payload expression evaluator
- No evident domain or compatibility constraint justifies bypassing the standard framework

If the classpath includes Spring Cloud Stream or Avro/schema-registry libraries, treat that as corroborating evidence — not sufficient evidence by itself.

Do not dismiss the framework based solely on the limitations of its annotation-based listener API before checking whether Spring Cloud Stream's functional or programmatic model already satisfies the requirement.

## Kafka / MQ / Rabbit producer
Assess boundaries between:
- use case initiation
- message/event construction
- domain event creation
- mapping/serialization
- infrastructure publishing concerns
- delivery guarantees/error handling

Look for risks such as:
- producers tightly coupled to domain behavior
- message construction logic duplicated across services
- publishing concerns bleeding into application logic

**Framework selection guidance:** Spring Cloud Stream is the canonical Spring solution for this archetype.

Flag a framework selection risk when **all** of the following are true:
- The archetype matches a Spring Cloud Stream use case
- The codebase implements custom commodity infrastructure such as publishing orchestration, custom serialization or routing, or delivery/retry plumbing that standard framework components already provide
- No evident domain or compatibility constraint justifies bypassing the standard framework

If the classpath includes Spring Cloud Stream or Avro/schema-registry libraries, treat that as corroborating evidence — not sufficient evidence by itself.

Do not dismiss the framework based solely on the limitations of a single publishing API before checking whether Spring Cloud Stream's supported models already satisfy the requirement.

## Scheduled or batch application
Assess boundaries between:
- scheduling/triggers
- job orchestration
- domain behavior
- persistence
- integration
- retry/recovery behavior

Look for risks such as:
- scheduled jobs acting as god entrypoints
- job orchestration and business rules collapsed into one class
- weak separation between trigger concerns and actual use-case behavior

**Framework selection guidance:** Spring Batch is the canonical Spring solution for this archetype.

Flag a framework selection risk when **all** of the following are true:
- The archetype matches a Spring Batch use case
- The codebase implements custom commodity infrastructure such as batch orchestration, custom chunking, or custom retry/restart logic that Spring Batch provides declaratively
- No evident domain or compatibility constraint justifies bypassing the standard framework

If the classpath contains `spring-batch-core`, treat that as corroborating evidence — not sufficient evidence by itself.

Do not dismiss the framework based solely on the complexity of its configuration model before checking whether its declarative job, step, and retry abstractions already satisfy the requirement.

## Mixed archetypes
If the repo contains more than one archetype:
- state the dominant one
- note the secondary archetype(s)
- keep the assessment anchored in the most central execution model
