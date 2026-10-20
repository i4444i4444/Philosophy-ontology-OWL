# Ontology of Philosophy

A formal OWL 2 DL ontology designed to model the domain of philosophy, focusing on the relationships between philosophers, philosophical movements, primary sources, and specific interpretative fragments.

## Design Rationale

### The Problem with Taxonomy
Representing philosophy as a strict hierarchy or taxonomy presents a fundamental methodological challenge. In a standard `subClassOf` model, a philosopher must be assigned to a specific philosophical movement. However, philosophical thought rarely fits into mutually exclusive categories. For instance, Immanuel Kant's philosophy is widely recognized as a synthesis of rationalism and empiricism. 

If we model Kant as an instance of only one movement, we lose the complexity of his thought. If we attempt to model him as an instance of both rationalism and empiricism — classes that are often contradictory in their core premises—the ontology becomes logically inconsistent. Furthermore, trying to define philosophy itself through a rigid, conjunctive definition inevitably excludes thinkers who deviate from that definition.

### The Network Solution
To resolve this, the ontology abandons strict taxonomic classification in favor of a **network model of intersecting concepts**. Instead of assigning a philosopher directly to a movement, the ontology introduces an intermediate layer of abstraction: the **interpretation fragment**.

The model works as follows:
1. A **Philosopher** produces a **Source** (a text).
2. A specific quote or passage from this source is extracted as an **Interpretation Fragment**.
3. This fragment is categorized by its **Dimension** (e.g., Subject, Method, Style, Goal).
4. The fragment represents a specific **Characteristic**.

This structure allows multiple philosophers to share the same characteristics without being forced into the same rigid class. The connection is grounded in actual textual evidence (quotes), making the ontology descriptive rather than prescriptive.

##  Ontology Architecture

*   **Base classes:** `Philosopher`, `Philosophical_movement`, `Source`, `Interpretation_fragment`, `Dimension`, `Characteristic`.
*   **Defined subclasses:** `Goal_Characteristic`, `Method_Characteristic`, `Style_Characteristic`, `Subject_Characteristic` (defined via `owl:equivalentClass` with `hasValue` restrictions on the `has_dimension` property).
*   **Properties:** 13 Object properties and 1 Data property (`has_quote`).
*   **Reasoning logic:** The `is_characterized_by` property is not asserted manually. It is inferred by the reasoner through a property chain axiom (`has_fragment ∘ represents_characteristic`). This eliminates the need to duplicate relationships and ensures logical consistency.

## Data

The ontology is populated with:
*   **16 philosophers** and **13 philosophical movements**.
*   **158 interpretation fragments** (imported from an XLSX dataset).
*   **110 out of 158** fragments are linked to at least one characteristic.

## Technologies & Tools

*   **OWL 2 DL / RDF/XML** — ontology format.
*   **Protege** — development environment.
*   **OWL Reasoner** — used for consistency checking and inferring implicit relationships.
*   **Gephi** — graph visualization (subgraphs of philosophers, fragments, and characteristics).

## Repository Structure

*   `ontology/` — the `.owl` ontology file.
*   `graphs/` — Gephi graphs showing relationships via fragments and direct characteristic links.

## Getting Started

Download the `.owl` file and open it in [Protege](https://protege.stanford.edu/). To view inferred relationships (such as `is_characterized_by`), start any OWL-compatible reasoner (e.g., HermiT or Pellet).
