# OpenUIR – Open UI Representation

OpenUIR is an **open standard for UI instructions** between a producer (application logic) and a backend (rendering engine).  
It defines a **platform-agnostic, multi-language retained UI model** that can be implemented on web, desktop, and mobile platforms.

---

## Purpose

OpenUIR allows developers to:

- Separate application logic from rendering
- Build declarative, retained-mode UI trees
- Implement backends in different languages and frameworks (e.g., HTML/Lit, SwiftUI, GTK)
- Support consistent layout, styles, and events across platforms

---

## Core Profile

The current **1.0 Core Profile** includes:

- Core views: `Text`, `Image`, `TextField`
- Layout containers: `Row`, `Column`, `Stack`
- Modifiers: spacing, padding, alignment
- Event handling: input, focus, click

> The specification is **minimal by design**, suitable for a proof-of-concept or reference implementation.

---

## Reference Implementation

A minimal reference implementation is available:

- HTML backend using native elements and Lit components
- Producer running in a web worker
- Simple diffing for efficient UI updates

---

## Contribution

OpenUIR is **community-driven**. Contributions are welcome via GitHub pull requests.  
Please read `governance.md` and `CODE_OF_CONDUCT.md` before contributing.

---

## License

- **Specifications**: Creative Commons Attribution 4.0 (CC BY 4.0)  
- **Reference code**: Apache 2.0

---

## Non-Goals

- OpenUIR is **not a framework**. It does not provide widgets, animation, or advanced state management.
- OpenUIR does **not aim for SwiftUI compatibility**. Inspirations are conceptual only.

---

## Contact

- GitHub Issues: For questions, proposals, or bug reports
- Discussions: For general roadmap, PoC, and feature planning

---

**OpenUIR – Open UI Runtime**  
An open, platform-agnostic UI standard.
