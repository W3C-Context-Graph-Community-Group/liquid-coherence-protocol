# Liquid Coherence Protocol

**W3C Context Graphs Community Group — Coherence Protocol Committee**  
Chair: Ron Itelman (Community Group Chair)

---

## What This Repository Is For

This repository owns the **Coherence Protocol specification**: the core technical deliverable of the W3C Context Graphs Community Group.

The Coherence Protocol specifies how independently designed systems — each operating under its own codebook, its own assumptions, its own definitions — can cross a shared boundary, measure the gap between what one system declares and what another requires, and produce a structured record of what was known, what was missing, what was asked, and what was decided. It is the instrument that makes codebook misalignment detectable, measurable, and resolvable at the point where it actually occurs: the boundary between systems.

This is not a data quality framework. It is not an ontology. It is not a schema validator. It is a measurement protocol for the layer that all of those tools assume has already been handled — and that, in the default condition of most cross-system communication, has not.

---

## The Problem This Solves

Every framework that minimizes uncertainty — Shannon's channel coding, Bayesian decision theory, active inference — presupposes that sender and receiver share a codebook. Shannon is correct. His model is complete and proven. We are not challenging it. We are identifying where its assumptions stop holding.

Shannon certifies delivery. He tells you whether the bits arrived. He cannot tell you whether the value those bits encode means the same thing on both sides of the boundary. That information is not on the wire. It is in the sender's codebook, on the other side. No quantity computable from Shannon's model distinguishes aligned codebooks from misaligned ones. This gap is not an engineering opinion. It is a formal result, and it extends to every downstream framework built on Shannon's foundation.

The consequence: a receiver proceeds with zero uncertainty about an interpretation that may be wrong. The date `03/01/2026` passes schema validation, matches the expected format, carries no error flag, and may mean March 1st or January 3rd depending on which side of the boundary produced it. The field labeled `revenue` in a 10-K filing maps to 27 distinct tagged definitions in XBRL — one of which an agent will select, silently, without disclosing that alternatives exist or that the selection has interpretive consequences. Every system reports success. The answer may be wrong.

We call this condition **ignorance of incoherence**: the state in which a system acts on ambiguous information with full confidence precisely because no instrument it possesses can distinguish the ambiguity from agreement.

The Coherence Protocol is that instrument.

---

## What the Protocol Does

The protocol decomposes the codebook into three **comparison facets** — Meaning, Structure, and Data — and a **resolution layer**, Context, that functions asymmetrically as the accumulating record of what was missing, surfaced, and resolved across the other three.

| Facet | Question | Form |
|---|---|---|
| **Data** | What values exist? | Observable, delivered by Shannon |
| **Meaning** | What do those values refer to? | Semantic definition, URI-identified |
| **Structure** | How are those values encoded? | Schema and constraints |
| **Context** | What resolutions were required to make the comparisons above well-defined? | Resolution layer — accumulates through the protocol's operation |

Context is not a fourth kind of information alongside the others. It is the protocol's working memory: the structured record of every incompleteness discovered and every question answered. A match on Meaning or Structure without surfaced Context is unverifiable — not because Context is a separate dimension that also needs matching, but because the comparisons on Meaning and Structure are not yet well-defined without it.

Every comparison produces a binary result: match or mismatch. The protocol produces three actions:

- **Halt** — a decidable condition required to proceed is not satisfied. Do not proceed.
- **Ask** — uncertainty is measurable and reducible. The divergence has been identified and can be narrowed through further exchange. Each Ask acquires information that no computation on the received data can produce. Each Ask produces Context.
- **Act** — all decidable conditions are met and measured uncertainty is below threshold. The boundary is coherent. Proceed.

The cost is O(1) per facet comparison per boundary crossing. The substrate reduces to binary and admits tensor decomposition, opening a path toward self-referential inference on the same surface that performs measurement.

---

## Scope of This Repository

This repository is scoped to the Coherence Protocol committee's responsibilities as defined in the [Community Group Charter](https://github.com/W3C-Context-Graph-Community-Group/Charter):

**In scope:**

- The formal specification for how independent Context Graphs compose across system boundaries
- The dependency ordering governing valid facet comparison sequences (Context → Meaning → Structure → Data)
- The canonical claim form: the irreducible five-column substrate onto which any system projects its codebook (`id | source | timestamp | key | value`)
- The Halt / Ask / Act decision interface and the conditions governing each action
- Cross-boundary uncertainty propagation: how misalignment at one boundary affects assessments at adjacent boundaries
- Composite resolution trace format: how boundary-crossing decision records link into an auditable cross-system chain
- The Boolean diff and tensor structure that connect the measurement substrate to downstream inference
- The learning loop specification: how gauge outputs accumulate into boundary classifiers, how trained models are stored as canonical claims, and how global pattern detection emerges from local boundary history

**Not in scope of this repository** (owned by other committees):

- The Context Graph data model at a single boundary → [Context Graph Spec repo]
- Intent Map format and serialization → [Syntax & Serialization committee]
- Interface with RDF, OWL, SHACL, SKOS → [Semantic Alignment committee]
- Contract between coherence measurements and decision models → [Decision Interface committee]
- Industry use cases and adoption → [Business & Industry committee]
- Agent-to-agent boundary crossings → [Agentic AI committee]
- Deployment patterns and measured benefit → [Applied Knowledge committee]

---

## Current State

| Artifact | Status |
|---|---|
| [Liquid Coherence — A Protocol for Codebook Alignment at System Boundaries](./Liquid_Coherence___A_Protocol_for_Codebook_Alignment_at_System_Boundaries__12_.pdf) | Working Draft — March 2026 |
| Canonical claim form specification | Working Draft — see Protocol Requirements |
| Coherence Protocol specification (normative) | Not yet started |
| Composite resolution trace format | Dependency on single-boundary trace — stub in Glossary |
| Cross-boundary uncertainty propagation formal model | In paper; not yet in spec form |
| Tensor substrate and learning loop specification | In paper; formal spec pending JSON-TL integration |

The working draft paper establishes the formal results, worked examples, and architectural claims this committee's specification will be grounded in. Normative specification work begins from that foundation.

---

## How the Protocol Fits the Coherence Stack

The Coherence Stack has four layers. This committee owns Layer 2.

| Layer | Name | What it does |
|---|---|---|
| 0 | Tensor Substrate | Unified mathematical representation for coherence state |
| 1 | Context Graph | Append-only hypergraph log of context events at boundaries |
| **2** | **Coherence Protocol** | **How measurements are made and compared across boundaries — this repo** |
| 3 | Decision Interface | Consumes coherence measurements to drive downstream decisions |

Layer 2 is the connective tissue of the stack. The Context Graph (Layer 1) measures a single boundary in isolation. The Coherence Protocol specifies how those single-boundary measurements compose: how uncertainty propagates, how resolution traces link, and how a chain of boundary crossings produces a coherent — or demonstrably incoherent — cross-system record.

---

## Why a Standard

The coherence protocol measures a property that no existing standard measures. The specific claims:

The problem is **formally proven, not asserted.** Codebook alignment is not identifiable from channel observables. Any standard built on transmission metrics alone inherits this blind spot.

Every existing standard **assumes the precondition this protocol measures.** Schema matching, ontology alignment, SHACL validation, data contracts — all require that codebooks have been surfaced before reconciliation can begin. The coherence protocol operates at the layer below: detecting whether that precondition holds. It does not compete with RDF, OWL, or SHACL. It provides the verification layer they currently lack.

**AI agents cross boundaries without human intervention.** A single agent query may touch ten tools, ten APIs, ten systems — each with its own codebook. The agent's Context layer is empty. It has no instrument to detect that the meaning of a field shifted at hop three. The more capable the agent, the more convincingly it proceeds with a wrong interpretation. A standard protocol for surfacing and comparing codebooks at boundaries gives agents a structured way to build the Context that coherence requires.

The measurement is **domain-agnostic.** The canonical claim form requires no prior agreement on domain terms. The five columns are fixed; the URN namespace is open. Any system in any domain can project its codebook onto the same surface. The standard specifies the envelope, not the message.

The cost is **bounded.** Facet comparison is O(1) per field per boundary. Any agent running the gauge on the same projections gets the same result. This reproducibility is what makes the measurement auditable and the standard enforceable.

---

## Contributing

This committee's work takes place in this repository and in the [Community Group's public mailing list](https://www.w3.org/community/context-graphs/). The primary working mode is iterative: working examples first, specification language derived from demonstrated behavior.

Contributions, issues, and proposed edits should be submitted as GitHub issues or pull requests against this repository.

Participants from the Shannon / information theory, semantic web, AI / ML systems, decision science, and enterprise data integration communities are especially encouraged. The gap this protocol addresses is visible from each of those vantage points, and the standard will be stronger for engagement across all of them.

---

## Related Repositories

| Repository | Committee | Scope |
|---|---|---|
| [Charter](https://github.com/W3C-Context-Graph-Community-Group/Charter) | Community Group | Mission, scope, deliverables, governance |
| [Semantic-Alignment](https://github.com/W3C-Context-Graph-Community-Group/Semantic-Alignment) | Semantic Alignment | RDF/OWL/SHACL integration, Glossary, SHACL schema |

---

## Links

- [W3C Context Graphs Community Group](https://www.w3.org/community/context-graphs/)
- [Community Group Charter](https://github.com/W3C-Context-Graph-Community-Group/Charter)
- [why_this_exists.md](https://github.com/W3C-Context-Graph-Community-Group/Charter/blob/main/why_this_exists.md) — The full rationale for this initiative

---

*Maintained by the Coherence Protocol committee of the W3C Context Graphs Community Group.*  
*Committee Chair: Ron Itelman*
