# Structural Reliability Under Projection

AI systems can fail not only because they reason incorrectly, but because they reason from compressed representations that no longer preserve the distinctions required by the claim, decision, explanation, or action being produced.

This repository contains the paper:

**Structural Reliability Under Projection: Representational Loss, Reconstructibility, and Admissibility**

---

## Overview

Modern AI systems often reason from compressed or partial representations: prompts, summaries, retrieved snippets, logs, metrics, traces, policy artifacts, tool outputs, memory, and interface-bounded context. These representations can be useful and necessary. They can also omit or collapse distinctions that remain operationally relevant.

The central claim of this paper is that some AI reasoning failures are not ordinary inference errors. They are failures of **invariant preservation under projection**. A system presents a conclusion as if it were supported by the representation available to it even though that representation does not preserve the distinction required by the conclusion.

This produces a recurring failure mode:

> A system treats non-identifiability under projection as though it were recoverable inference error.

The result may be fluent, coherent, and persuasive while still lacking structural support. Examples include unsupported root-cause attribution, hallucinated source support, unsafe action under missing state, and metric-driven proxy success.

The paper's main operational claim is:

> **Structural insufficiency should change the available epistemic operations, not merely confidence.**

The underlying identifiability question is only the starting point. Once the support available for a query has been characterized, the framework asks what the system is licensed to do next: infer directly, reconstruct, retrieve, request, qualify, route, defer, or refuse the requested form.

This makes the paper's distinctive object not projection alone, but a licensing relation of the form:

```text
representation
    → dependency support
    → support assessment
    → licensed epistemic operation
    → report or action
```

The framework therefore distinguishes factual correctness from structural reliability. A response can happen to be factually correct even when the representation did not license the epistemic operation used to produce it; conversely, a licensed operation can still contain an ordinary inference error.

At a higher level, the framework can be understood as three connected layers:

```text
information structure
    → dependency support
    → epistemic governance
```

The information layer asks what distinctions survive target formation and projection. The support layer asks what kind of support remains for the dependencies material to the query. The governance layer asks which epistemic operations and response forms that support licenses, while keeping operational permission for actions distinct from informational support.

---

## Core Idea

A reasoning system does not operate on the full underlying situation. It operates on a representation of that situation.

A representation may preserve some distinctions while losing others. For example:

* a log summary may preserve that an outage occurred while losing the event ordering needed for root-cause analysis;
* a retrieved citation may preserve a source pointer while omitting the passage needed to verify a claim;
* a single metric may preserve a ranking while losing the distinction between reversible and irreversible failures.

The question is not whether a representation is complete. The question is whether it preserves the distinctions required by the claim being made.

The operative representation also need not be the system's entire persistent reasoning state. A system may preserve a richer external state containing history, dependencies, provenance, alternatives, and lifecycle information while retrieving only the bounded portion relevant to the current query. That retrieved context is still a projection of the richer state:

```text
persistent represented state
    is not
current operative representation
```

Persistence therefore does not eliminate projection. It can make projection more explicit and revisitable by preserving a richer source from which later bounded views can be reconstructed.

When the required distinction survives projection, the system can reason over it. When it does not survive, structural insufficiency should change the epistemic operations available to the system, not merely lower confidence. Depending on what support remains, the system may reconstruct a boundedly recoverable distinction, retrieve or request missing support, qualify the claim, branch over assumptions, route to an appropriate source, weaken the answer, or refuse the requested inference. What it should not do is present the missing distinction as though it had been recovered from the current representation.

The dependency structure relevant to a query should not be treated as fixed or necessarily complete. Inquiry may reveal that the original question collapsed several questions, that two terms must remain distinct, that an action requires a separate authority or validity judgment, or that a previously known concern constrains a new claim. The framework therefore applies to the dependencies currently represented as material while allowing that later inquiry may revise that structure.

---

## Structural Reliability and Bounded Assessment

The paper gives **structural reliability** a distinct role from factual correctness. Relative to a query, operative representation, and reasoning regime, a continuation is structurally reliable when the epistemic operation selected does not exceed the support actually available for the query.

The paper separates three questions:

* **Assessment fidelity** — did the reasoner correctly assess the support available for the query?
* **Governance compliance** — did the reasoner select an epistemic operation licensed by its own support assessment?
* **Factual correctness** — is the resulting proposition actually true?

These are not interchangeable. A model may faithfully follow the operation policy induced by a mistaken support assessment. It may assess support correctly and nevertheless overclaim. And it may arrive at a correct answer through an operation that the representation did not support.

This distinction is important because ordinary answer accuracy can reward a lucky unsupported answer. Structural reliability evaluates a different question: whether the operation used to produce the answer was licensed by the information basis available to the reasoner.

---

## Target Formation and Projection

The paper distinguishes two stages that can introduce loss. A richer field of potentially relevant state may first be narrowed into the state treated as the target of reasoning, and that target is then projected into the operative representation:

`F → S_Γ → R`

This separates **target-selection loss**, where a material distinction is excluded when the reasoning target is formed, from **representational loss**, where the target contains the distinction but the operative representation fails to preserve or boundedly reconstruct it.

These failures require different repairs. Improving the representation may fix representational loss while leaving an incorrectly bounded target unchanged.

The richer source of a projection need not always be an inaccessible world state. It may itself be an explicit persistent reasoning state. In that case, a bounded query-relative retrieval can be written schematically as:

`B → R_q`

where `B` is the richer persistent state and `R_q` is the operative representation assembled for query `q`. This does not create projection-free reasoning; it changes where projection occurs and can make recovery easier because the richer source remains available.

---

## Error vs. Representational Loss

The paper distinguishes **error** from **representational loss**.

An **error** occurs when the information required to answer a query is present in the representation, but the system reasons incorrectly. In principle, the error can be corrected within the same representation.

A **loss** occurs when the representation does not preserve the distinction required by the query. In that case, no amount of additional reasoning over the same representation can recover the missing distinction without adding assumptions, expanding the representation, obtaining new information, or changing the answer form.

Formally, the paper frames this using identifiability under projection. Given a projection from an underlying state space into a representation, a query is identifiable when it is constant over the equivalence classes induced by that projection. If two underlying states map to the same representation but require different answers, the query is not identifiable under that projection.

Treating loss as error encourages overconfident answers, hallucinated support, arbitrary resolution of ambiguity, and unsafe action under incomplete state.

---

## Dependency Status

The paper introduces a dependency-status classification for reasoning under projection and presents it operationally as a ladder. For a claim depending on some distinction, the system should determine what kind of support the current representation provides for that distinction.

The term **ladder** refers to the weakening of available response forms as recoverability and auditability diminish; it is not a claim that all epistemic support relations form a total order or a single scalar dimension.

The four statuses induce different operation spaces rather than merely different confidence levels. An illustrative licensing matrix is:

| Status | Infer | Reconstruct | Retrieve / trace | Qualify / reframe | Refuse requested form |
| --- | :---: | :---: | :---: | :---: | :---: |
| Preserved | L | C | C | C | C |
| Reconstructible | U* | L | C | L | C |
| Traceable | U | U | L | L | L |
| Opaque | U | U | C** | L | L |

`L` means licensed, `C` conditionally available, and `U` unlicensed from the current support state.

\* Direct inference becomes licensed only after the bounded recovery path has actually restored the required distinction.

\** Retrieval is conditionally available only when the representation preserves or can establish a route to an external source capable of expanding the information basis.

The matrix is query- and regime-relative. It illustrates the operation partition rather than prescribing one universal policy for every domain.

A distinction is **preserved** when it is directly represented in a form sufficient for the query.

A distinction is **reconstructible** when it is not directly represented but can be recovered through an explicit bounded procedure using information available in the current representation.

A distinction is **traceable** when the dependency, source, assumption, transformation, or point of loss is recorded, but the missing distinction itself cannot be recovered.

A distinction is **opaque** when the dependency is neither recoverable nor auditable from the current representation.

The boundary between reconstructible and traceable is especially important. A citation, source hash, tool trace, or provenance pointer may make a dependency traceable, but it does not make the claim reconstructible unless the representation also includes enough content or recovery structure to determine the relevant distinction.

A claim may depend on several distinctions, and those dependencies may have different statuses. Dependency status is therefore better understood as a profile over the claim’s relevant dependencies rather than as one global scalar label. A claim-level description such as **mixed** indicates that this profile is nonuniform; it is not necessarily a fifth primitive status.

Operation and response-form selection must preserve the weaker or unresolved dependencies relevant to the claim rather than compressing the entire profile into an unjustifiably strong status. The four statuses are therefore not merely confidence levels: they correspond to different sets of epistemic operations that the representation licenses.

The paper also distinguishes the **structural role** of a dependency from its status. A dependency may function as an **invariant**, a **selector**, or an **operator**. Structural type and dependency status are orthogonal: for example, an invariant may be preserved while an operator condition is merely traceable. This matters because a system may preserve enough structure to execute a procedure while losing the conditions that establish whether applying that procedure is appropriate.

The dependency profile is stage-relative. Later inquiry may add, split, relate, narrow, or reject dependencies. Such revisions should be explicit, and newly represented constraints should be allowed to alter subsequent claim and action licensing.

---

## Structural Requirements

The paper identifies three structural requirements for reasoning under projection:

1. **Partial observability of loss-relevant state**
   The system must preserve or expose detectable signs that a required distinction may be missing, ambiguous, collapsed, or dependent on assumptions not encoded in the representation.

2. **Bounded correction**
   The system must distinguish bounded repair from global recomputation, unbounded replay, hidden assumption import, or an unmarked replacement of the information basis. A bounded and explicit transition to a richer or differently structured representation may itself be part of correction when it remains within the declared regime.

3. **Non-collapse of distinct levels**
   The system must not treat different representational roles as interchangeable, such as confusing a representation with the underlying system, an intermediate reasoning state with a final conclusion, or a selected explanation with the full set of explanations consistent with the evidence.

These requirements do not guarantee correctness. They preserve the conditions under which reasoning failures remain visible, corrigible, and accountable.

---

## Unsupported Promotion

The paper identifies a common structural failure across several apparently different reasoning mistakes: **unsupported promotion**.

Unsupported promotion occurs when a weaker, differently typed, or merely retained support relation is treated as though it established the additional conditions required for a stronger epistemic license.

Examples include:

* **traceable → reconstructible** — a pointer, citation, provenance record, or dependency trace is treated as though the missing distinction had been recovered;
* **policy-selected → evidence-supported** — a policy, prior, utility, or decision rule selects an outcome and the result is then reported as though the evidence itself determined it;
* **procedure preserved → procedure licensed** — a rule, heuristic, scaffold, or procedure remains executable after projection and its continued executability is treated as evidence that the conditions governing its use were also preserved.

A promotion may be justified, but the additional licensing conditions must themselves be preserved, boundedly reconstructed, retrieved, or introduced through an explicit change of information basis. Mere persistence of a pointer, outcome, procedure, or successful execution is not such a witness.

This principle unifies bounded correction, non-collapse, support-role separation, and the paper's broader warning against silently strengthening claims as representational constraints disappear.

---

## Expected Behavior

A system reasoning under projection should:

* avoid presenting unsupported determinate answers as if they followed from the representation alone;
* preserve ambiguity when multiple underlying states remain consistent with the representation;
* distinguish recoverable error from representational loss;
* separate inference from decision when action is required under non-identifiability;
* mark traceable dependencies without treating them as recovered;
* avoid collapsing distinct causal, evidential, temporal, institutional, or operational levels;
* revise the represented dependency structure explicitly when new material constraints are discovered;
* use bounded retrieval or representation change explicitly when the current operative view is insufficient rather than pretending the missing distinction was already present;
* select an epistemic operation and associated response form licensed by dependency status;
* separately check whether any proposed action or continuation is operationally permitted under the declared regime.

The goal is not blanket abstention. The goal is operation discipline. A system should infer directly when support is preserved, reconstruct when bounded recovery is available, retrieve, request, qualify, or route when a dependency is traceable, and expose insufficiency, defer, or reformulate when the dependency is opaque. Structural insufficiency should alter what the system does epistemically, not merely how confident it sounds.

---

## Dependency-Status Assessment

The framework distinguishes three related but non-identical status judgments and then treats operation or action selection separately:

* **Actual dependency status** — the support a dependency really has relative to the query, operative representation, and reasoning regime.
* **Assessed dependency status** — the status inferred by the reasoning system.
* **Reported dependency status** — the status communicated in the resulting answer or reasoning artifact.
* **Selected operation or action** — what the system actually does based on its assessment and any additional policy, authority, utility, safety, or operational constraints.

Practical systems do not have direct access to actual status in every case. They act through imperfect assessments. The paper therefore distinguishes **assessment fidelity** from **governance compliance**. Assessment fidelity asks whether the assessed support matches the support that actually obtains; governance compliance asks whether the selected operation is licensed by the assessment. Reporting remains a further observable layer. A system may faithfully act on a mistaken assessment, or it may correctly recognize limited support yet still select or report an operation stronger than its own assessment licenses.

When status assessment is uncertain, the system should preserve that uncertainty rather than silently promoting the claim to a stronger status.

The framework is also subject to its own projection limits. Successful execution of an admissibility procedure does not certify that every condition governing its applicability was represented. This **Self-Application Non-Certification** principle limits what the framework claims without undermining its practical value.

---

## Testable Consequences

The framework suggests several evaluation patterns.

### Correctness vs. Structural Support

Evaluation should not collapse factual correctness and structural support into one score. A model can be factually correct by chance even when the operative representation does not distinguish the states that require different answers. Conversely, a structurally licensed inference can still contain an ordinary reasoning mistake. The framework therefore predicts that answer accuracy and operation licensing should be evaluated separately.

### Representation-Enrichment Sensitivity

If a richer representation restores a distinction that was collapsed in a compressed one, a projection-aware system should become more willing to make determinate claims. Under the compressed representation, it should qualify, branch, request expansion, or mark the dependency.

### Traceability Is Not Reconstruction

Adding a citation, source pointer, provenance marker, or tool trace should not be treated as sufficient support unless the representation also contains enough content or recovery structure to determine the relevant claim.

### Persistent-State Retrieval Sensitivity

When a bounded operative representation is insufficient but a richer persistent state contains the missing distinction, a projection-aware system should be able to retrieve or reconstruct the needed query-relative state explicitly. Evaluation should distinguish successful bounded recovery from answers that merely behave as though the richer state had already been present in the original context.

### Operation Sensitivity

Evaluation should consider not only whether an answer is plausible, but whether the epistemic operation used to produce or replace it is licensed by the dependency status of the claim. A reconstructible case should permit bounded reconstruction; a traceable case may call for retrieval, request, qualification, or routing; an opaque case should not be silently treated as determinate.

### Assessment, Reporting, and Governance Fidelity

Evaluation should distinguish errors in dependency-status assessment from errors in reporting and operation selection. A system may underestimate or overestimate the support available to it, may correctly recognize limited support but report a stronger status, or may report the limitation accurately while nevertheless taking an action that presupposes stronger support.

### Compressed/Enriched Diagnostic Contrast

One possible evaluation design is to compare paired tasks that differ only in whether the query-relevant distinction is represented. A system that gives the same determinate answer form in both cases would be failing to regulate claims by dependency status.

### Structural-Revision Sensitivity

A longer-form evaluation could test whether a system updates its dependency structure when a new material distinction is introduced and whether later responses continue to respect the consequences of that revision.

### Empirical Vulnerability

The formal non-identifiability result is conditional on the stated representational assumptions. A separate empirical question is whether the framework's distinctions provide useful explanations or predictions for actual reasoning systems.

Evidence against the practical importance of the framework would include:

* failure to observe meaningful behavioral differences between preserved, reconstructible, traceable, and opaque dependency conditions under independently designed evaluation;
* failure of controlled representation enrichment to produce the predicted change in licensed answer form;
* failure of relational or dependency structure to add diagnostic value beyond component-level information; or
* repeated external cases in which the framework's distinctions provide no useful explanatory or corrective advantage over simpler existing accounts.

Such findings would not invalidate the elementary non-identifiability result itself, but they would weaken the claim that reconstructibility under projection identifies a practically important structure of AI reasoning failure.

---

## AI Safety and Security Relevance

The framework is intended to help analyze failures such as:

* unsupported root-cause attribution in incident response;
* hallucinated or weakly grounded source support in retrieval-augmented generation;
* security recommendations made without the relevant code path, configuration, or threat model;
* agentic actions taken from compressed or incomplete state;
* policy or deployment decisions that collapse reversibility, uncertainty, and residual risk into a single score;
* user-modeling or Theory-of-Mind-like claims that overstate what can be inferred from partial interaction traces;
* metric-driven proxy success that hides loss of the target structure.

The central safety question is whether a system can distinguish what its representation determines, what it can reconstruct, what it can merely trace, and what it has lost---and then bind that structural assessment to the inference, retrieval, reporting, or action operations it is permitted to perform.

---

## Who This Is For

This paper is intended for researchers, engineers, and practitioners working on:

* AI safety and security evaluation;
* reasoning systems;
* agentic reliability;
* retrieval-augmented generation and source grounding;
* incident-response assistants and security copilots;
* evaluation and benchmark design;
* abstraction, compression, and state representation;
* partial observability;
* auditability and provenance;
* proxy metrics and Goodhart-style failures;
* systems that must distinguish inference from decision under uncertainty.

---

## Repository Contents

* [`01-reconstructibility-under-projection.pdf`](01-reconstructibility-under-projection.pdf) — the full paper.

---

## LaTeX Source Conventions

The LaTeX source is intentionally kept close to the logical structure of the prose.

* Prose paragraphs are not hard-wrapped to a fixed column width. Each paragraph normally remains a single source line.
* Blank lines separate paragraphs.
* Structural LaTeX---such as equations, lists, tables, environments, and logically distinct commands---may be split across lines where doing so improves readability.
* Source formatting should preserve semantic and structural clarity rather than enforce a uniform line-length limit.
* Existing labels, citations, mathematical notation, and document structure should be preserved when making purely editorial changes.
* Avoid reformatting unchanged LaTeX solely for stylistic reasons, since this creates noisy diffs.

---

## Scope

This work presents a conceptual and diagnostic framework rather than a specific implemented or empirically evaluated system.

The paper explains why some reasoning failures are representational rather than merely inferential, why local coherence is not the same as structural support, and why output-level correctness can miss failures caused by projection. Its central operational claim is that structural insufficiency should constrain the epistemic operations available to a reasoning system rather than merely reduce confidence while leaving behavior unchanged. It formalizes structural reliability separately from factual correctness, distinguishes assessment fidelity from governance compliance, and treats unsupported promotion as a recurring way that weaker or differently typed support is silently converted into stronger epistemic license.

It does not claim to:

* explain every reasoning failure;
* guarantee correct conclusions;
* eliminate ambiguity;
* recover distinctions absent from the current information basis;
* guarantee that every relevant dependency or constraint has been discovered;
* provide a complete implementation of dependency-status tracking;
* report empirical validation of the framework.

The framework applies to the dependency structure represented at a given stage of reasoning. That structure may later be revised as additional distinctions, constraints, or relationships become material. Such revisions change the information basis to which admissibility is applied and should be made explicit.

The paper also permits architectures in which a richer persistent reasoning state exists outside the current model context and supplies bounded query-relative representations when needed. This is an architectural consequence of the framework, not a claim that the paper implements or empirically validates such a system.

Further formal refinement, projection-sensitive evaluation, persistent-state implementations, and independent empirical validation remain open directions.

---

## Citation

If you find this work useful, you can cite it as:

```text
Brian Cameron.
Structural Reliability Under Projection: Representational Loss, Reconstructibility, and Admissibility.
2026.
```

---

## Author

Brian Cameron
