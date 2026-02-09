# javascript.info — Structural Summary by ToC Heading (scope + depth)

Generated: 2026-02-09 (Asia/Kolkata)

> This mirrors the ToC hierarchy and describes what each heading covers/teaches and roughly how deep it goes.
> It intentionally does **not** summarize the actual content in detail.

---

## Part 1 — The JavaScript language

**Overall:** A language-first path from basics through modern JavaScript: core syntax, data types, functions/closures, objects/prototypes/classes, async, modules, plus selected advanced corners.

### An introduction
- **An Introduction to JavaScript** — what JS is, where it runs, what “scripts” are; orientation and motivation. **Depth:** gentle overview.
- **Manuals and specifications** — how to use MDN vs spec references; how to read docs effectively. **Depth:** practical navigation guidance.
- **Code editors** — editor/tooling setup for learning and iteration. **Depth:** practical overview.
- **Developer console** — using browser DevTools console for experiments and debugging. **Depth:** hands-on basics.

### JavaScript Fundamentals
- **Hello, world!** — first run, embedding/external scripts. **Depth:** beginner.
- **Code structure** — statements, semicolons, basic organization. **Depth:** beginner conventions.
- **"use strict"** — strict mode purpose + key behavior changes. **Depth:** conceptual + common gotchas.
- **Variables** — let/const/var basics, naming, mutation. **Depth:** beginner.
- **Data types** — introductory survey of primitives/objects. **Depth:** beginner (full detail later).
- **Interaction: alert/prompt/confirm** — basic browser IO. **Depth:** basic.
- **Type Conversions** — explicit/implicit coercions and pitfalls. **Depth:** beginner→intermediate.
- **Basic operators, maths** — arithmetic, assignment, precedence. **Depth:** beginner.
- **Comparisons** — equality/strict equality, ordering, edge cases. **Depth:** beginner→intermediate.
- **Conditional branching** — if/else, ternary. **Depth:** beginner.
- **Logical operators** — &&/||/!, short-circuiting. **Depth:** beginner→intermediate.
- **Nullish coalescing ??** — null/undefined-aware defaulting. **Depth:** focused modern feature.
- **Loops: while and for** — iteration patterns, break/continue. **Depth:** beginner.
- **switch** — multi-branch selection. **Depth:** beginner.
- **Functions** — declarations, params, return. **Depth:** beginner.
- **Function expressions** — expressions vs declarations, callbacks intro. **Depth:** beginner→intermediate.
- **Arrow functions (basics)** — concise functions + initial `this` note. **Depth:** beginner.
- **JavaScript specials** — a tour of JS “quirks” and practical rules of thumb. **Depth:** survey.

### Code quality
- **Debugging in the browser** — breakpoints, stepping, console workflow. **Depth:** practical.
- **Coding Style** — readability conventions and consistency. **Depth:** practical norms.
- **Comments** — what/when/how to comment well. **Depth:** pragmatic.
- **Ninja code** — anti-patterns that reduce clarity. **Depth:** cautionary.
- **Automated testing with Mocha** — unit testing basics, test structure. **Depth:** introductory testing.
- **Polyfills and transpilers** — compatibility strategies; Babel/polyfills framing. **Depth:** conceptual + practical.

### Objects: the basics
- **Objects** — object literals, properties, basic operations. **Depth:** foundational.
- **Object references and copying** — reference semantics, shallow vs deep copy issues. **Depth:** foundational + pitfalls.
- **Garbage collection** — reachability model at a high level. **Depth:** conceptual overview.
- **Object methods, this** — method calls and `this` binding basics. **Depth:** core concept.
- **Constructor, new** — constructor functions and `new` behavior. **Depth:** core.
- **Optional chaining ?.** — safe property access. **Depth:** focused modern feature.
- **Symbol type** — unique keys + meta-programming entry point. **Depth:** intermediate.
- **Object to primitive conversion** — coercion hooks and edge cases. **Depth:** intermediate and subtle.

### Data types
- **Methods of primitives** — wrappers and why primitives have methods. **Depth:** intermediate.
- **Numbers** — numeric quirks, rounding, special values. **Depth:** intermediate.
- **Strings** — operations, indexing, Unicode basics. **Depth:** intermediate.
- **Arrays** — basics, mutability, typical usage. **Depth:** intermediate.
- **Array methods** — map/filter/reduce and other workhorse patterns. **Depth:** practical and detailed.
- **Iterables** — iteration protocol; for..of. **Depth:** intermediate.
- **Map and Set** — keyed collections; set semantics. **Depth:** practical intermediate.
- **WeakMap and WeakSet** — GC-friendly associations. **Depth:** advanced-leaning.
- **Object.keys/values/entries** — enumeration helpers. **Depth:** practical.
- **Destructuring assignment** — structure extraction + defaults/rest. **Depth:** practical intermediate.
- **Date and time** — Date API + caveats. **Depth:** practical.
- **JSON methods, toJSON** — parse/stringify + serialization behavior. **Depth:** practical and detailed.

### Advanced working with functions
- **Recursion and stack** — recursion, stack limits and patterns. **Depth:** intermediate.
- **Rest/spread** — variadics and data expansion. **Depth:** practical intermediate.
- **Variable scope, closure** — lexical scope and closures, deeply. **Depth:** core + detailed.
- **The old var** — legacy scoping/hoisting behaviors. **Depth:** compatibility-focused.
- **Global object** — globalThis and environment globals. **Depth:** intermediate.
- **Function object, NFE** — function properties; named function expressions. **Depth:** advanced-leaning.
- **new Function** — dynamic code compilation semantics. **Depth:** advanced/edge-case.
- **setTimeout/setInterval** — scheduling and pitfalls. **Depth:** practical.
- **Decorators/forwarding, call/apply** — wrappers and forwarding `this`/args. **Depth:** intermediate→advanced.
- **Function binding** — bind and partial application. **Depth:** practical intermediate.
- **Arrow functions revisited** — deeper arrow semantics (`this`, `arguments`, etc.). **Depth:** intermediate→advanced.

### Object properties configuration
- **Property flags/descriptors** — defineProperty, enumerability/writability/configurability. **Depth:** advanced fundamentals.
- **Getters and setters** — accessor properties and encapsulation patterns. **Depth:** intermediate→advanced.

### Prototypes, inheritance
- **Prototypal inheritance** — prototype chain delegation, detailed. **Depth:** core + detailed.
- **F.prototype** — constructor linkage and prototype mechanics. **Depth:** core for legacy/class understanding.
- **Native prototypes** — caveats of extending built-ins. **Depth:** advanced caution.
- **Prototype methods, objects without proto** — Object.create(null) and edge cases. **Depth:** advanced.

### Classes
- **Class basic syntax** — class declarations, methods, constructors. **Depth:** practical intermediate.
- **Class inheritance** — extends/super/overrides. **Depth:** intermediate.
- **Static properties/methods** — class-level members. **Depth:** practical.
- **Private/protected** — private fields (#) and “protected by convention”. **Depth:** intermediate.
- **Extending built-in classes** — subclassing built-ins and gotchas. **Depth:** advanced-leaning.
- **instanceof** — prototype-based type checking. **Depth:** practical.
- **Mixins** — composition patterns. **Depth:** advanced patterns.

### Error handling
- **try…catch** — exceptions and finally. **Depth:** practical.
- **Custom errors** — extending Error and error taxonomy. **Depth:** intermediate.

### Promises, async/await
- **Callbacks intro** — motivation + callback shape. **Depth:** primer.
- **Promise** — states, then/catch, detailed basics. **Depth:** detailed foundation.
- **Chaining** — composition and return semantics. **Depth:** detailed.
- **Promise error handling** — propagation and catch patterns. **Depth:** detailed.
- **Promise API** — all/race/any/allSettled etc. **Depth:** practical reference.
- **Promisification** — converting callback APIs. **Depth:** practical.
- **Microtasks** — scheduling model behind promises. **Depth:** advanced-but-important.
- **Async/await** — ergonomic async composition. **Depth:** practical and detailed.

### Generators, advanced iteration
- **Generators** — iterator creation with yield. **Depth:** intermediate→advanced.
- **Async iteration/generators** — for-await, async iterables. **Depth:** advanced.

### Modules
- **Modules intro** — ESM model and module scope. **Depth:** practical.
- **Export/Import** — named/default exports + patterns. **Depth:** practical.
- **Dynamic imports** — runtime loading and splitting. **Depth:** intermediate.

### Miscellaneous
- **Proxy/Reflect** — meta-programming interception. **Depth:** advanced.
- **Eval** — executing strings + security/scope issues. **Depth:** advanced caution.
- **Currying** — functional transformation patterns. **Depth:** intermediate→advanced.
- **Reference Type** — spec-level nuance behind method calls/this. **Depth:** advanced internals.
- **BigInt** — integer arithmetic beyond Number. **Depth:** focused feature.
- **Unicode, String internals** — code points/surrogates/practical Unicode traps. **Depth:** advanced practical.
- **WeakRef/FinalizationRegistry** — GC-adjacent APIs and hazards. **Depth:** advanced.

---

## Part 2 — Browser: Document, Events, Interfaces

**Overall:** DOM, events, UI input, lifecycle/loading, and event loop concepts. **Depth:** practical, example-heavy.

### Document
- **Browser environment, specs** — what browser JS includes; standards landscape. **Depth:** orientation.
- **DOM tree** — node types and document structure. **Depth:** practical.
- **Walking the DOM** — traversal APIs and patterns. **Depth:** practical.
- **Searching** — selectors and lookup patterns. **Depth:** practical and detailed.
- **Node properties** — nodeName/tagName/textContent/innerHTML basics. **Depth:** practical.
- **Attributes vs properties** — differences and pitfalls. **Depth:** common gotchas.
- **Modifying the document** — create/insert/remove nodes. **Depth:** practical and detailed.
- **Styles and classes** — classList/style and computed styles intro. **Depth:** practical.
- **Element size and scrolling** — box metrics and scrolling props. **Depth:** intermediate.
- **Window sizes and scrolling** — viewport/scroll APIs. **Depth:** practical.
- **Coordinates** — client/page coords and bounding boxes. **Depth:** intermediate.

### Introduction to Events
- **Intro to browser events** — event model overview. **Depth:** foundational.
- **Bubbling/capturing** — propagation phases. **Depth:** detailed foundation.
- **Event delegation** — scalable patterns for handlers. **Depth:** practical.
- **Default actions** — preventDefault and behavior control. **Depth:** practical.
- **Custom events** — CustomEvent and dispatchEvent. **Depth:** intermediate.

### UI Events
- **Mouse events** — click/move/button semantics. **Depth:** practical.
- **mouseover/out vs mouseenter/leave** — boundary semantics. **Depth:** intermediate.
- **Drag’n’Drop with mouse** — building drag behavior manually. **Depth:** detailed practical.
- **Pointer events** — unified mouse/touch/pen model. **Depth:** practical.
- **Keyboard events** — keydown/keyup and key identification. **Depth:** practical.
- **Scrolling** — scroll event patterns. **Depth:** practical.

### Forms, controls
- **Form properties/methods** — forms and elements API. **Depth:** practical.
- **focus/blur** — focus management. **Depth:** practical.
- **change/input/cut/copy/paste** — input lifecycle events. **Depth:** practical.
- **submit** — submit flow and interception. **Depth:** practical.

### Document and resource loading
- **DOMContentLoaded/load/beforeunload/unload** — lifecycle timing. **Depth:** practical and detailed.
- **Scripts async/defer** — load/execute ordering. **Depth:** practical and detailed.
- **Resource load onload/onerror** — tracking asset load outcomes. **Depth:** practical.

### Miscellaneous
- **MutationObserver** — reacting to DOM changes. **Depth:** intermediate.
- **Selection and Range** — text selection APIs. **Depth:** intermediate→advanced.
- **Event loop** — microtasks vs macrotasks. **Depth:** foundational advanced topic.

---

## Part 3 — Additional articles

**Overall:** focused mini-tracks on specific web topics beyond the DOM+events core.

### Frames and windows
- **Popups and window methods** — window control. **Depth:** practical.
- **Cross-window communication** — postMessage patterns. **Depth:** intermediate.
- **Clickjacking** — UI redress attack + mitigations. **Depth:** security overview.

### Binary data, files
- **ArrayBuffer/typed arrays** — binary manipulation. **Depth:** intermediate.
- **TextDecoder/TextEncoder** — bytes↔text encoding. **Depth:** practical.
- **Blob** — binary payload objects. **Depth:** practical.
- **File/FileReader** — file inputs and reading APIs. **Depth:** practical.

### Network requests
- **Fetch** — primary HTTP API usage. **Depth:** practical.
- **FormData** — multipart form construction. **Depth:** practical.
- **Fetch progress** — tracking download progress. **Depth:** intermediate.
- **Fetch abort** — cancellation with AbortController. **Depth:** practical.
- **Fetch CORS** — cross-origin policy and preflights. **Depth:** detailed.
- **Fetch API (deeper)** — options/headers/modes/referrer/etc. **Depth:** reference-like.
- **URL objects** — URL parsing and composition. **Depth:** practical.
- **XMLHttpRequest** — legacy API basics. **Depth:** practical + compatibility.
- **Resumable file upload** — chunking/resume strategies. **Depth:** advanced practical.
- **Long polling** — near-realtime over HTTP. **Depth:** intermediate.
- **WebSocket** — full-duplex realtime. **Depth:** practical.
- **Server Sent Events** — one-way event stream. **Depth:** practical.

### Storing data in the browser
- **Cookies** — cookie model and document.cookie pitfalls. **Depth:** practical.
- **LocalStorage/sessionStorage** — key-value persistence. **Depth:** practical.
- **IndexedDB** — structured client-side DB. **Depth:** intermediate→advanced.

### Animation
- **Bezier curve** — easing curve math. **Depth:** conceptual + practical.
- **CSS animations** — keyframes/transitions. **Depth:** practical.
- **JS animations** — requestAnimationFrame patterns. **Depth:** intermediate.

### Web components
- **Orbital height** — conceptual overview of web components. **Depth:** orientation.
- **Custom elements** — definitions and lifecycle. **Depth:** practical.
- **Shadow DOM** — encapsulation. **Depth:** practical.
- **Template element** — template primitives. **Depth:** practical.
- **Slots/composition** — content projection. **Depth:** intermediate.
- **Styling** — scoping/theming. **Depth:** intermediate.
- **Events** — retargeting/composed events. **Depth:** intermediate→advanced.

### Regular expressions
- **Patterns and flags** — overview. **Depth:** foundational.
- **Character classes** — built-in and custom. **Depth:** foundational.
- **Unicode (u, \p{...})** — Unicode-aware matching. **Depth:** intermediate.
- **Anchors (^, $)** — boundary matching. **Depth:** foundational.
- **Multiline (m)** — anchor semantics over lines. **Depth:** foundational.
- **Word boundary (\b)** — boundary token semantics. **Depth:** foundational.
- **Escaping** — literal special chars. **Depth:** practical.
- **Sets/ranges ([...])** — bracket expressions. **Depth:** foundational.
- **Quantifiers** — repetition. **Depth:** foundational.
- **Greedy vs lazy** — matching control. **Depth:** intermediate.
- **Capturing groups** — grouping and extraction. **Depth:** foundational→intermediate.
- **Backreferences** — \N / \k<name>. **Depth:** intermediate.
- **Alternation (|)** — branching. **Depth:** foundational.
- **Lookahead/lookbehind** — assertions. **Depth:** advanced-leaning.
- **Catastrophic backtracking** — performance pitfalls. **Depth:** advanced practical.
- **Sticky (y)** — positional searching. **Depth:** intermediate.
- **RegExp/String methods** — match/search/replace APIs. **Depth:** practical reference.

---

## Sources referenced
- https://javascript.info/
- https://github.com/javascript-tutorial/en.javascript.info/issues/3654
