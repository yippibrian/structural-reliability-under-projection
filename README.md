# Structural Reliability Under Projection

AI systems can fail not only because they reason incorrectly, but because they reason from compressed representations that no longer preserve the distinctions required by the claim, explanation, decision, or action being produced.

This repository contains the standalone paper:

**Structural Reliability Under Projection: Representational Loss, Reconstructibility, and Admissibility**

## The central contribution

Projection-induced information loss is already studied through identifiability, sufficiency, abstraction, partial observability, partial identification, and related frameworks. This paper asks the next operational question:

> Given what a representation preserves about the dependencies required by a proposed continuation, what kind of epistemic operation remains licensed?

The paper organizes the answer through a small control structure:

```text
projection
    → dependency status
    → epistemically licensed operations

epistemic licensing + operational validity
    → admissible operations

admissible operations + selection and budget policy
    → response or action
```

Dependency status functions as a **thin waist**. Above it may sit prompts, retrieved documents, telemetry, memories, metrics, causal models, policy artifacts, tool outputs, or other domain-specific representations. Below it may sit direct inference, reconstruction, retrieval, qualification, routing, reframing, explicit decision, deferral, or refusal of the requested form.

The representations and workflows do not need to share one ontology. They meet at the narrower question of what happened to the dependency required by the proposed continuation.

The paper's principal claim is therefore:

> **Structural insufficiency should change the available epistemic operation, not merely lower confidence while leaving the operation unchanged.**

## The basic failure

Let a projection map an underlying state into the representation available to a reasoner:

```text
P: S → R
```

For a query `q`, the answer is identifiable under the projection only when states collapsed into the same representation do not require different answers. If

```text
P(s₁) = P(s₂)
```

but

```text
q(s₁) ≠ q(s₂),
```

then no procedure operating only on the common representation can recover the correct answer for both states. More reasoning over the same information basis cannot universally restore a distinction that the representation does not contain.

This differs from ordinary error:

- **Error:** the query-relevant distinction remains identifiable and the represented information is sufficient, in principle, to correct the result without changing the information basis.
- **Representational loss:** the current representation does not preserve or boundedly recover the distinction required by the query.

A response may happen to be factually correct even when the representation did not license the operation used to produce it. Realized accuracy does not retroactively supply missing structural support.

## The four dependency statuses

For each dependency material to a query, the framework asks two gated questions:

1. Is the required distinction directly available or boundedly recoverable?
2. If recovery is unavailable, does an attributable dependency trail remain?

This is not an unrestricted product of recovery and attribution. Attribution becomes status-resolving specifically when recovery fails:

```text
direct recovery                         → preserved
bounded recovery                        → reconstructible
recovery unavailable + attributable     → traceable
recovery unavailable + unattributable   → opaque
```

The statuses mean:

- **Preserved:** the required distinction is directly represented in a form sufficient for the query.
- **Reconstructible:** the distinction is not directly represented but can be restored through an explicit bounded procedure using the permitted information basis.
- **Traceable:** the dependency, source, assumption, transformation, or point of loss remains attributable, but the required distinction cannot presently be recovered.
- **Opaque:** the dependency is neither recoverable nor adequately attributable from the current representation.

Traceability is not merely a smaller amount of reconstruction. A citation, source hash, tool trace, document identifier, or provenance pointer may identify where support should come from without supplying enough content or recovery structure to establish the claim.

A claim may depend on several distinctions with different statuses. Dependency status is therefore a profile over material dependencies, not necessarily one scalar label for the entire claim. A description such as **mixed** indicates a nonuniform profile; it is not automatically a fifth primitive status.

## From status to licensed operation

The statuses constrain kinds of continuation, not merely degrees of confidence. An illustrative licensing matrix is:

| Status | Infer | Reconstruct | Retrieve / trace | Qualify / reframe | Refuse requested form |
| --- | :---: | :---: | :---: | :---: | :---: |
| Preserved | L | C | C | C | C |
| Reconstructible | U† | L | C | L | C |
| Traceable | U | U | L | L | L |
| Opaque | U | U | C‡ | L | L |

`L` means licensed, `C` conditionally available, and `U` unlicensed from the current support state.

† Direct inference becomes licensed only after the bounded recovery path has restored the required distinction.

‡ Retrieval is conditionally available only when the representation preserves or can establish a route to an external source capable of expanding the information basis.

The matrix is query- and regime-relative. It illustrates the operation partition rather than prescribing one universal policy for every domain.

## Why these four statuses arise

The paper does not begin by stipulating four metaphysical kinds of knowledge. It begins with primitive dependency conditions in an assessment context: whether the required distinction is directly recoverable, recoverable through a bounded procedure, or unavailable; and, when recovery is unavailable, whether an adequate attribution trail remains. The gated classification map sends those conditions to preserved, reconstructible, traceable, and opaque status.

The formal argument then separates three claims:

1. **Primitive-state factorization:** the gated recovery–attribution map classifies primitive dependency conditions into the four statuses.
2. **Licensing sufficiency:** when the declared base licensing relation depends only on distinctions preserved by that classification, licensing factors through the four-status interface.
3. **Portable minimality:** when a declared family of contexts behaviorally distinguishes every pair of statuses, no proper quotient preserves the same licensing behavior across that family.

The paper therefore does not claim that reality contains exactly four epistemic states or that every controller must use four internal labels. It gives the four-way interface a conditional behavioral justification.

Two statuses are locally behaviorally equivalent when a particular query, regime, and operation repertoire license exactly the same continuations for both. A controller may safely compile locally equivalent statuses into one internal control state.

Local compression need not be portable. A controller without retrieval or routing may treat traceable and opaque dependencies identically, while a recipient with those capabilities must distinguish them. Accordingly:

> **Safe compression for current control does not imply safe compression for destination control.**

For a declared family of contexts, the portable quotient retains every distinction that changes licensing behavior in at least one intended context. When the family is **status-separating**—when every pair of statuses has some licensing witness—the behavioral quotient of the primitive dependency-state space has exactly the four status classes, up to isomorphism. A coarser interface must either license an operation that should be blocked or block an operation that should be licensed. The interface is minimal in that conditional and operational sense, not as a universal metaphysical taxonomy.

## Unsupported promotion

The paper identifies a common structural failure across otherwise different reasoning problems: **unsupported promotion**.

Unsupported promotion occurs when a weaker, differently typed, or merely retained support relation is treated as though it established the additional conditions required for a stronger epistemic license.

Examples include:

- **traceable → reconstructible:** a pointer or provenance record is treated as recovered evidence;
- **policy-selected → evidence-supported:** a decision rule selects an outcome that is then reported as evidentially determined;
- **procedure executable → procedure licensed:** a retained procedure is assumed to remain applicable merely because it can still be run;
- **transported → destination-adequate:** a preserved artifact is assumed to support every later query merely because it arrived intact;
- **proxy → target:** a compressed metric is treated as preserving all distinctions relevant to the underlying objective.

A promotion may be justified, but the additional licensing conditions must themselves be preserved, boundedly reconstructed, retrieved, or introduced through an explicit change of information basis. Persistence, availability, selection, or successful execution is not such a witness by itself.

## Licensing, validity, admissibility, selection, and stopping

The framework separates four questions:

```text
dependency status
    → epistemic-operation licensing

epistemic licensing + operational validity
    → admissibility

admissibility + policy and budget
    → selection
```

Dependency status determines which operations are epistemically licensed by the represented support. A proposed operation must separately satisfy the authority, safety, feasibility, reversibility, or other operational-validity conditions of the declared regime. The intersection of epistemic licensing and operational validity forms the admissible operation set. Selection from that set may then depend on budget, urgency, utility, expected diagnostic value, policy, and other decision commitments.

The existence of an admissible terminal response means that stopping is permitted, not necessarily optimal. Further investigation may itself be admissible when its expected diagnostic value justifies its cost. Conversely, the existence of some admissible continuation does not mean that a terminal answer is licensed; retrieval, clarification, representation expansion, or routing may be the only admissible next operation.

Classification is also not compulsion. An implementation may report a licensing judgment, encourage compliance, audit violations, gate selected transitions, or enforce the constraint mechanically. These represent different governance strengths.

## Actual, assessed, reported, and selected state

Practical systems act through imperfect assessments of their own support. The framework therefore separates:

- **Actual dependency status:** the support a dependency really has relative to the query, operative representation, and regime.
- **Assessed dependency status:** the status assigned by the bounded reasoner.
- **Reported dependency status:** the status communicated in the answer or reasoning artifact.
- **Selected operation:** the continuation the system actually performs.

This exposes distinct failure locations:

- **Representation insufficiency:** the actual information basis does not provide the required support.
- **Assessment failure:** the reasoner misclassifies that support.
- **Reporting inflation:** the answer claims stronger support than the reasoner's own assessment warrants.
- **Action-governance failure:** the selected continuation is not licensed even by the assessed status.

A system may honestly report its assessment and still be wrong about its actual evidential position. It may also comply perfectly with a policy induced by a mistaken assessment. Factual correctness, assessment fidelity, reporting fidelity, and governance compliance are therefore related but non-equivalent evaluation targets.

## Three requirements for reliable correction

The paper identifies three conceptual design requirements:

1. **Observability of loss-relevant state**  
   The representation must expose enough structure for missing, ambiguous, collapsed, or assumption-dependent distinctions to become detectable where possible.

2. **Bounded correction**  
   The system must distinguish correction within the current information basis from retrieval, representation expansion, hidden assumption import, global recomputation, or replacement of that basis. Changing the representation may be admissible, but the transition should be explicit.

3. **Non-collapse of distinct levels and roles**  
   The system must not silently identify the representation with the world, a proxy with its target, a source pointer with source content, a selected explanation with the full compatible set, a local judgment with a composed-system judgment, or executability with applicability.

These requirements do not guarantee correctness. They preserve the conditions under which failures can remain visible, attributable, and corrigible.

## A cybernetic interpretation

Dependency status can serve as a compact control variable in a corrective loop:

```text
operative representation
    → assessed dependency profile
    → epistemically licensed operation set
    + operational-validity constraints
    → admissible operation set
    + selection and budget policy
    → selected continuation
    → observed consequence
    → corrected or refined representation
```

Feedback may reveal ordinary error, expose an unresolved dependency, justify retrieval, or create diagnostic pressure to refine the representation. The objective is not unlimited retention or expansion. Additional structure earns its place by making a demonstrated class of consequential failures more observable, attributable, or correctable.

This loop is corrigible rather than self-certifying. Successful execution or favorable feedback does not establish that the system correctly assessed every dependency or that its representation was complete. A reasoning or governance procedure cannot infer from its own successful execution that all conditions licensing its application were represented.

## Persistence and transport

A richer persistent state can preserve history, provenance, alternatives, and dependencies that need not fit within one operative context. Query-relative retrieval from that state is still a projection:

```text
persistent represented state
    ≠ current operative representation
```

Persistence can improve reconstructibility by preserving bounded recovery paths, but it does not eliminate projection. Nor does moving or versioning an artifact certify its adequacy for a new query or recipient:

> **State transport preserves an artifact and its represented relations; it does not certify destination-relative admissibility.**

Recipient systems must reassess dependency status and operational validity relative to their own query, regime, operation repertoire, and operative representation.

## Examples and applications

The framework can be used as a design and evaluation lens for:

- security copilots and incident-response assistants reasoning from partial telemetry;
- code assistants operating without all relevant paths, configuration, or runtime state;
- retrieval-augmented generation systems that expose citations without sufficient source content;
- agentic systems acting from compressed memory, tool output, environmental observation, or inferred intent;
- causal explanations that collapse interacting causes into a single attribution;
- decisions that compress uncertainty, reversibility, or competing values into one score;
- user models that overstate what can be inferred from partial interaction traces;
- inherited procedures whose original applicability conditions are no longer represented;
- benchmarks that reward plausible or lucky answers without testing whether the representation supported them.

These domains do not share one ontology. They share a narrower boundary at which a projected representation supplies support for a downstream claim, procedure, or action. Dependency status provides a common vocabulary for governing what may cross that boundary.

## Evaluation implications

The framework suggests several prospective evaluation patterns:

- **Correctness versus structural support:** score whether an operation was licensed separately from whether its realized answer happened to be true.
- **Compressed/enriched contrast:** compare otherwise matched tasks that differ in whether the query-relevant distinction is represented.
- **Representation-enrichment sensitivity:** test whether a system becomes appropriately more determinate when added information restores identifiability.
- **Traceability versus reconstruction:** verify that adding a pointer or citation does not automatically produce a supported claim.
- **Operation sensitivity:** test whether different statuses produce reconstruction, retrieval, qualification, routing, or refusal rather than a fixed answer form with varying confidence.
- **Licensing versus validity:** distinguish an operation unsupported by dependency status from one that is epistemically supported but operationally invalid under the declared regime.
- **Assessment, reporting, and governance fidelity:** localize whether failure occurred in support assessment, communication, or continuation selection.
- **Structural-revision sensitivity:** test whether newly discovered material constraints continue to govern later claims until explicitly revised or removed.

The formal non-identifiability result is conditional on the stated representational assumptions. Whether the four-status interface and its operational consequences usefully explain or predict behavior in actual systems remains an empirical question. Failure to observe the predicted behavioral distinctions would weaken the framework's practical significance without invalidating the elementary non-identifiability result.

## Scope

The paper presents a conceptual and diagnostic framework. It does not claim to:

- explain every reasoning failure;
- guarantee correct conclusions;
- eliminate ambiguity;
- recover distinctions absent from the operative information basis;
- guarantee discovery of every material dependency, stakeholder, or constraint;
- establish universal necessity or sufficiency of its three corrective design requirements;
- provide a complete detector, runtime enforcement protocol, or adaptive controller;
- provide empirical validation of the proposed distinctions.

The framework is relative to the dependency structure currently represented as material to the query. Inquiry may revise that structure by introducing new distinctions, dependencies, constraints, or questions. Such revisions change the information basis to which admissibility is applied and should be explicit rather than silently attributed to an earlier representation.

## Who this is for

The paper is intended for researchers, engineers, and practitioners working on:

- AI safety and security evaluation;
- reasoning and agentic systems;
- retrieval-augmented generation and source grounding;
- incident-response assistants and security copilots;
- evaluation and benchmark design;
- abstraction, compression, and state representation;
- partial observability, auditability, and provenance;
- proxy metrics and decision-making under uncertainty.

## Repository contents

- [`01-reconstructibility-under-projection.pdf`](01-reconstructibility-under-projection.pdf) — the full paper.

## LaTeX source conventions

- Prose paragraphs are not hard-wrapped to a fixed column width. Each paragraph normally remains a single source line.
- Blank lines separate paragraphs.
- Structural LaTeX—including equations, lists, tables, environments, and logically distinct commands—may be split across lines where this improves readability.
- Source formatting should preserve semantic and structural clarity rather than enforce a uniform line-length limit.
- Existing labels, citations, mathematical notation, and document structure should be preserved during purely editorial changes.
- Avoid reformatting unchanged LaTeX solely for stylistic reasons, since that creates noisy diffs.

## Citation

If you find this work useful, you can cite it as:

```text
Brian Cameron.
Structural Reliability Under Projection: Representational Loss, Reconstructibility, and Admissibility.
2026.
```

## Author

Brian Cameron
