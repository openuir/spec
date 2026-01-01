# RATIONALE

This document explains the motivation, design decisions, and trade-offs behind **OpenUIR (Open User Interface Representation)**.

It exists to clarify *why* OpenUIR is designed the way it is, what problems it aims to solve, and which problems it intentionally does **not** attempt to solve.

OpenUIR is not a framework. It is a **foundational specification**.

---

## 1. Scope and Intent

OpenUIR defines a **retained-mode UI representation** and a **small, explicit instruction set** for mutating that representation.

It is designed to sit **below** UI frameworks and **above** rendering backends.

OpenUIR intentionally avoids defining:

* Navigation systems
* Animation engines
* State management models
* Styling languages (e.g. CSS)
* Application lifecycles

These concerns belong in higher-level frameworks built *on top of* OpenUIR.

The scope of OpenUIR is deliberately narrow to ensure:

* Predictable semantics
* Portable implementations
* Low backend complexity

---

## 2. Producer / Backend Separation

A core principle of OpenUIR is the strict separation between:

* **Producer**: owns UI structure, state, layout intent, and style resolution
* **Backend**: renders UI using a native toolkit and dispatches events

This separation enables:

* Multi-language producers
* Worker-thread or cross-process UI logic
* Backend reuse across platforms

OpenUIR treats the UI tree as **data**, not as framework objects.

---

## 3. Retained-Mode UI Model

OpenUIR uses a **retained-mode** UI model:

* UI nodes persist over time
* Nodes have stable identities
* Changes are expressed as explicit mutations

This model was chosen because it:

* Enables partial updates
* Avoids full tree rebuilds
* Works across threads and processes
* Aligns with native UI toolkits and scene graphs

Immediate-mode UIs and declarative rebuild models were explicitly rejected, as they are difficult to apply safely across language and process boundaries.

---

## 4. Explicit Instructions (No Implicit Diffing)

OpenUIR backends do **not** perform reconciliation or diffing.

Instead, producers emit explicit instructions such as:

* Create node
* Update properties
* Remove node

This design:

* Removes backend heuristics
* Makes performance characteristics predictable
* Avoids hidden costs and magic behavior

While this shifts responsibility to the producer, it greatly simplifies backend implementations and improves determinism.

---

## 5. Stable Node Identities

OpenUIR requires nodes to have **stable identifiers**.

This is a deliberate trade-off.

Stable IDs:

* Enable precise updates
* Avoid structural ambiguity
* Support cross-thread and cross-process communication

While managing IDs can be burdensome in dynamic UIs, OpenUIR treats identity as a **first-class concept**, similar to scene graphs, game engines, and embedded UI systems.

---

## 6. Layout Philosophy

OpenUIR adopts a **flexbox-like, one-dimensional layout model**.

The goals are:

* Broad platform support
* Simple mental model
* Native toolkit mapping

Layout semantics are defined **semantically**, not mathematically.

Pixel-perfect equivalence across backends is explicitly *not* required.

This mirrors real-world behavior of existing systems such as SwiftUI, CSS, and native UI toolkits.

---

## 7. Styles Without Inheritance

OpenUIR intentionally does **not** include implicit style inheritance.

Reasons:

* Style inheritance is backend-complex
* It requires environment propagation
* It introduces hidden coupling and ordering dependencies

Instead:

* Styles are resolved by the producer
* Backends apply styles directly

Higher-level frameworks are expected to provide:

* Style inheritance
* Theming
* Environment-based styling

OpenUIR remains a flat, explicit layer.

---

## 8. Events and Interaction

OpenUIR supports bidirectional communication:

* Backends emit user events associated with node IDs
* Producers handle events and emit new UI instructions

Event semantics are minimal and explicit.

There is no implicit bubbling, capture, or priority system unless explicitly specified.

This avoids backend-specific event models leaking into the core standard.

---

## 9. Accessibility

OpenUIR includes **semantic accessibility primitives**, such as:

* Roles
* Labels
* Actions

However, platform-specific accessibility behavior is owned by the backend.

A single, universal accessibility system is not feasible across platforms.

OpenUIR prioritizes **semantic intent** over platform parity.

---

## 10. Binary Wire Format

OpenUIR defines its protocol independently of any concrete encoding.

Binary encoding is recommended because it:

* Enables zero-copy transfers
* Scales well across threads and processes
* Reduces serialization overhead

However:

* JSON is a valid transport for tooling and debugging
* Binary is not required for correctness

The wire format is an optimization, not a philosophical requirement.

---

## 11. Comparison to Existing Systems

OpenUIR occupies a different layer than most UI systems:

| System                | Category                       |
| --------------------- | ------------------------------ |
| React / Angular       | UI frameworks                  |
| Flutter               | Framework + renderer           |
| SwiftUI               | Framework + language feature   |
| Tokamak / OpenSwiftUI | SwiftUI reimplementations      |
| **OpenUIR**           | **UI representation standard** |

OpenUIR enables architectures that existing systems do not target, such as multi-language producers and cross-process UI control.

---

## 12. Adoption Expectations

OpenUIR is not intended for mass-market application development.

Likely early adopters include:

* Embedded and industrial UI teams
* Systems and engine developers
* UI framework authors
* Cross-platform tooling teams

The project prioritizes correctness and composability over convenience.

---

## 13. Non-Goals

OpenUIR explicitly does **not** aim to:

* Replace existing UI frameworks
* Define a complete application platform
* Guarantee pixel-perfect rendering across backends
* Solve all styling or theming problems
* Hide complexity behind implicit behavior

---

## 14. Design Philosophy

OpenUIR favors:

* Explicitness over magic
* Determinism over convenience
* Portability over platform-specific optimization
* Small core over large surface area

This philosophy is intentional and central to the project.

---

## 15. Conclusion

OpenUIR is a low-level, opinionated foundation for building UI systems across languages and platforms.

Its success depends on remaining:

* Small
* Clear
* Implementable
* Honest about trade-offs

OpenUIR exists to enable new architectures, not to replace existing ones.

---

**End of RATIONALE**
