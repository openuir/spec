# OpenUIR

**OpenUIR (Open User Interface Representation)** is an open, backend-agnostic specification for representing user interfaces as a retained UI tree with explicit mutations.

OpenUIR defines *what* a user interface is and *how* it changes — not *how* it is rendered.

It is designed as a **foundational layer** for building UI frameworks, runtimes, and tools across languages, threads, processes, and platforms.

---

## What OpenUIR Is

OpenUIR is:

* A **UI representation standard**, not a framework
* A **retained-mode** UI model with stable node identities
* A **producer / backend** architecture
* Designed for **multi-language** and **multi-backend** environments
* Suitable for **worker-thread**, **WASM**, and **cross-process** UI architectures

OpenUIR treats the UI tree as **data**, communicated through explicit instructions.

---

## What OpenUIR Is Not

OpenUIR is **not**:

* A UI framework or widget library
* A replacement for HTML, SwiftUI, Compose, GTK, or LVGL
* A styling language like CSS
* An application runtime or lifecycle manager
* A solution for navigation, animation, or state management

Those concerns belong in higher-level frameworks built *on top of* OpenUIR.

---

## Core Architecture

OpenUIR separates UI systems into two roles:

### Producer

* Builds and owns the UI tree
* Resolves layout intent and styles
* Handles application state and events
* Runs in any language (Swift, Rust, JavaScript, WASM, etc.)
* May run on a background thread or in a separate process

### Backend

* Renders UI using a native toolkit (DOM, SwiftUI, Compose, GTK, LVGL, etc.)
* Maintains a retained representation of nodes
* Applies layout and styles using platform-native mechanisms
* Dispatches user events back to the producer

Communication happens via **explicit UI instructions**, not shared framework APIs.

---

## UI Model

* Retained-mode UI tree
* Nodes have **stable identifiers**
* Changes are expressed as **explicit create / update / remove instructions**
* No implicit reconciliation or diffing by the backend

This model enables deterministic updates and safe cross-thread or cross-process execution.

---

## Layout

OpenUIR defines a **flexbox-like, one-dimensional layout model**:

* HStack (horizontal)
* VStack (vertical)
* ZStack (overlay)

Layout semantics are **semantic**, not pixel-perfect.

Backends are expected to preserve layout intent while mapping to native mechanisms.

---

## Styles

Styles in OpenUIR are:

* Explicit
* Fully resolved by the producer
* Applied directly by the backend

OpenUIR does **not** include implicit style inheritance.

This keeps backend implementations small and predictable.

---

## Events

OpenUIR supports bidirectional communication:

* Backends emit user events tied to node identifiers
* Producers handle events and emit new UI instructions

Event semantics are minimal and explicit. There is no implicit bubbling or capture model.

---

## Accessibility

OpenUIR includes semantic accessibility primitives such as roles and labels.

Platform-specific accessibility behavior remains the responsibility of the backend.

---

## Encoding

OpenUIR defines its protocol independently of any concrete encoding.

* Binary encoding is recommended for performance-sensitive scenarios
* JSON is valid for tooling, debugging, and early implementations

Encoding choice does not affect the semantics of the specification.

---

## Intended Audience

OpenUIR is primarily aimed at:

* UI framework authors
* Systems and engine developers
* Embedded and industrial UI teams
* Cross-platform and multi-language toolchains

It is **not** intended to replace mainstream UI frameworks for typical application development.

---

## Status

OpenUIR is an **early-stage open standard**.

Current focus:

* Defining a stable core profile
* Providing reference producers and backends
* Validating real-world feasibility

---

## Governance

OpenUIR is developed as an open, vendor-neutral standard.

Design decisions are documented in [`RATIONALE.md`](./RATIONALE.md).

---

## License

TBD

---

**OpenUIR exists to enable new UI architectures — not to replace existing ones.**
