# The Modern JavaScript Tutorial — javascript.info

## Complete Table of Contents & Summary

> Source: [https://javascript.info/](https://javascript.info/)
> By Ilya Kantor. ~1300 pages (PDF). Open-source, regularly updated.
> Last checked: February 2026.

The tutorial is divided into three parts: Part 1 covers the JavaScript language itself (environment-agnostic), Part 2 covers the browser DOM/Events/UI layer, and Part 3 collects standalone topical deep-dives that presuppose the first two parts.

---

## Part 1 — The JavaScript Language

Core language coverage from absolute basics through advanced patterns (closures, prototypes, classes, async, generators, modules, metaprogramming). Environment-agnostic: no browser or Node specifics except where unavoidable. Progresses roughly from beginner to intermediate/advanced.

### 1.1 An Introduction

Orientation chapter. Very short, no code yet.

- **An Introduction to JavaScript** — What JS is, its history (LiveScript → JavaScript, no relation to Java), what it can/can't do in the browser (same-origin policy, etc.), and what makes it unique (full integration with HTML/CSS, simple things done simply, supported everywhere). Mentions competing languages that transpile to JS (TypeScript, CoffeeScript, Dart, Brython, Kotlin).
- **Manuals and specifications** — Pointers to the ECMA-262 specification, MDN as the primary reference, and caniuse.com / kangax compat tables.
- **Code editors** — Brief distinction between IDEs (VS Code, WebStorm) and lightweight editors. Recommendations, not a tutorial on any specific editor.
- **Developer console** — How to open dev tools in Chrome, Firefox, Safari, Edge. Running snippets in the console. Enough to follow along with the tutorial.

### 1.2 JavaScript Fundamentals

The largest section. Covers all basic syntax and control flow. Detailed treatment with many small exercises. Suitable for complete beginners to programming.

- **Hello, world!** — The `<script>` tag, external scripts via `src`, the `type` and `language` attributes (deprecated), basic first program.
- **Code structure** — Statements, semicolons (and automatic semicolon insertion gotchas), comments (`//`, `/* */`).
- **The modern mode, "use strict"** — What `"use strict"` does, where to place it, that classes and modules enable it automatically.
- **Variables** — `let`, `const`, and (briefly) `var`. Naming conventions, case sensitivity, reserved words. Constants with UPPERCASE convention for hard-coded values.
- **Data types** — The 8 types: `number` (including `Infinity`, `NaN`), `bigint`, `string`, `boolean`, `null`, `undefined`, `object`, `symbol`. The `typeof` operator and its quirks (`typeof null === "object"`).
- **Interaction: alert, prompt, confirm** — The three browser modal functions. Enough to do interactive exercises, not meant as production UI.
- **Type Conversions** — String, numeric, and boolean conversions. Rules for each (e.g., `""` → `0`, `"0"` → `true`, `undefined` → `NaN`). Explicit vs implicit coercion.
- **Basic operators, maths** — Arithmetic operators, string concatenation with `+`, unary `+` for numeric conversion, assignment as an expression, increment/decrement, bitwise operators (mentioned, not detailed), comma operator.
- **Comparisons** — `==` vs `===`, comparison of different types, `null`/`undefined` comparison pitfalls. Practical advice: prefer strict equality.
- **Conditional branching: if, '?'** — `if`/`else if`/`else`, the ternary `?` operator, advice on when not to abuse ternaries.
- **Logical operators** — `||`, `&&`, `!`. Short-circuit evaluation. Truthy/falsy values. `||` for default values (pre-nullish-coalescing pattern).
- **Nullish coalescing operator '??'** — `??` vs `||`: only treats `null`/`undefined` as "empty". Precedence restrictions (can't mix with `||`/`&&` without parentheses).
- **Loops: while and for** — `while`, `do...while`, `for`. `break`, `continue`, labels for breaking out of nested loops.
- **The "switch" statement** — Syntax, fall-through behaviour, grouping cases, strict equality in switch.
- **Functions** — Function declarations, parameters, default values, `return`. Local vs outer variables. Naming conventions.
- **Function expressions** — Functions as values, function expressions vs declarations, the key difference: hoisting. Callback patterns.
- **Arrow functions, the basics** — `=>` syntax, single-line and multi-line variants. Brief intro only — revisited later in depth.
- **JavaScript specials** — Quick recap/cheatsheet of everything in this section.

### 1.3 Code quality

Practices and tooling. Relatively short articles, each focused on one concern.

- **Debugging in the browser** — Chrome DevTools: Sources panel, breakpoints, stepping through code, watch expressions, call stack, `debugger` statement.
- **Coding Style** — Brace styles, indentation, line length, semicolons, nesting levels. References to popular style guides (Airbnb, StandardJS, Google). Linters (ESLint).
- **Comments** — When/how to write good comments, self-documenting code, JSDoc annotations (briefly).
- **Ninja code** — Satirical article on how *not* to write code. Teaches good practices by showing humorous bad ones (one-letter variables, abbreviations, overlapping names, etc.).
- **Automated testing with Mocha** — BDD-style testing. `describe`/`it`/`assert`. Writing tests before code. Nested `describe`, `before`/`after` hooks. A practical intro to test-driven development at a basic level.
- **Polyfills and transpilers** — What transpilers (Babel) and polyfills (core-js) do. Why they're needed for using modern JS in older environments. High-level overview, not a Babel configuration tutorial.

### 1.4 Objects: the basics

Core object mechanics. Assumes familiarity with fundamentals above. Detailed coverage of how objects work under the hood.

- **Objects** — Object literals, properties (dot and bracket notation), computed properties, property shorthands, `in` operator, `for...in` loop, property ordering rules. Thorough treatment.
- **Object references and copying** — Objects stored/copied by reference vs primitives by value. Comparison of objects. Shallow copy with `Object.assign` and spread. Deep cloning with `structuredClone`. Practical implications.
- **Garbage collection** — Mark-and-sweep algorithm, reachability concept, internal optimisations (generational, incremental, idle-time collection). Conceptual, not engine-specific implementation details.
- **Object methods, "this"** — Method shorthand syntax. `this` in methods. `this` is not bound — evaluated at call time. Arrow functions have no own `this`. Implications and common pitfalls.
- **Constructor, operator "new"** — Constructor function convention (capital letter). What `new` does internally (create object, run function, return). `new.target`. Return from constructors. Methods in constructors.
- **Optional chaining '?.'** — `?.` for safe property access, `?.()` for optional method calls, `?.[]` for optional bracket access. Short-circuiting. Read-only (can't use for assignment).
- **Symbol type** — Creating symbols, symbols as unique property keys, global symbol registry (`Symbol.for`/`Symbol.keyFor`), system symbols (`Symbol.toPrimitive`, `Symbol.iterator`, etc.). Why they exist (avoid name clashes in library code).
- **Object to primitive conversion** — `Symbol.toPrimitive`, `toString`, `valueOf`. Conversion hints: `"string"`, `"number"`, `"default"`. How operators trigger conversions. Fairly detailed treatment of the conversion algorithm.

### 1.5 Data types

In-depth treatment of each built-in data type and associated patterns. Significant depth — one of the meatiest sections.

- **Methods of primitives** — How primitives can have methods via temporary wrapper objects (`String`, `Number`, `Boolean`). The "object wrapper" mechanism. Why `new Number()` etc. should be avoided.
- **Numbers** — `toString(base)`, rounding (`Math.floor/ceil/round/trunc`, `toFixed`), imprecise floating-point (`0.1+0.2`), `isNaN`, `isFinite`, `parseInt`/`parseFloat`, `Math` object methods.
- **Strings** — Backtick template literals, special characters, string length, accessing characters, immutability, case conversion, `indexOf`/`includes`/`startsWith`/`endsWith`, `slice`/`substring`/`substr`, string comparison and locale, Unicode surrogates (briefly).
- **Arrays** — Declaration, `at()`, push/pop/shift/unshift, internal representation (contiguous-memory optimisation), `for...of` vs `for...in`, length property (truncation trick), `new Array(n)`, `toString`. When arrays are and aren't appropriate.
- **Array methods** — `splice`, `slice`, `concat`, `forEach`, `indexOf`/`includes`/`find`/`findIndex`/`findLast`/`findLastIndex`, `filter`, `map`, `sort` (and its string-coercion gotcha), `reverse`, `split`/`join`, `reduce`/`reduceRight`, `Array.isArray`, `some`/`every`, `fill`, `copyWithin`, `flat`/`flatMap`. Very thorough — this is essentially a reference article.
- **Iterables** — The iterable protocol (`Symbol.iterator`), writing custom iterables, iterables vs array-likes, `Array.from`. How `for...of` works under the hood.
- **Map and Set** — `Map` (any-type keys, iteration order, `Object.entries`/`Object.fromEntries` conversion), `Set` (unique values), iteration methods, `WeakMap`/`WeakSet` previewed.
- **WeakMap and WeakSet** — Weak references, garbage-collection-friendly caching/bookkeeping, no iteration, use cases (additional data for objects, caching).
- **Object.keys, values, entries** — `Object.keys/values/entries` (return arrays, not iterables). Transforming objects via these + `Object.fromEntries`.
- **Destructuring assignment** — Array and object destructuring, default values, rest pattern `...`, nested destructuring, smart function parameters via destructuring.
- **Date and time** — `new Date(...)` variants, `getFullYear`/`getMonth`/etc., `Date.now()`, `Date.parse`, auto-correction, benchmarking.
- **JSON methods, toJSON** — `JSON.stringify` (replacer, space), `JSON.parse` (reviver), `toJSON` method, handling circular references, practical serialisation patterns.

### 1.6 Advanced working with functions

Deeper function mechanics: scope, closures, scheduling, decorators, binding. Intermediate-to-advanced level.

- **Recursion and stack** — Recursive thinking, execution context and the call stack, recursive data structures (linked lists, trees). Base case / recursive case pattern. Rewrites between loops and recursion.
- **Rest parameters and spread syntax** — `...args` in function signatures, spread in function calls and array/object literals, `arguments` object (legacy). Practical patterns.
- **Variable scope, closure** — Lexical Environment, scope chain, closures explained in detail with diagrams. The classic loop-variable closure pitfall. IIFE pattern (historical). This is the most conceptually dense article in the section.
- **The old "var"** — `var` hoisting, no block scope, function scope, IIFE as workaround. Why `let`/`const` replaced it.
- **Global object** — `window` (browser) / `globalThis`, global variables, polyfill pattern.
- **Function object, NFE** — Functions are objects: `.name`, `.length` (parameter count), custom properties. Named Function Expressions for reliable self-reference in recursion.
- **The "new Function" syntax** — `new Function('a', 'b', 'return a+b')`. Created from strings at runtime. Closure scope: accesses global scope, not the enclosing lexical environment. Use cases and caveats.
- **Scheduling: setTimeout and setInterval** — Delayed and repeated execution. Nested `setTimeout` vs `setInterval` (precision differences). Zero-delay `setTimeout`. `clearTimeout`/`clearInterval`. Garbage collection of scheduled callbacks.
- **Decorators and forwarding, call/apply** — Transparent caching decorator, `func.call`, `func.apply`, method borrowing, forwarding with spread. Practical decorator patterns.
- **Function binding** — `bind` for fixing `this`. Partial application with `bind`. The "losing this" problem in callbacks. Why arrow functions partially solve it.
- **Arrow functions revisited** — No `this`, no `arguments`, no `new`, no `super`. How these properties make arrows ideal for short callbacks and method-internal functions.

### 1.7 Object properties configuration

Short section on property descriptors. Intermediate level.

- **Property flags and descriptors** — `writable`, `enumerable`, `configurable` flags. `Object.getOwnPropertyDescriptor`, `Object.defineProperty`, `Object.defineProperties`. Sealing/freezing objects.
- **Property getters and setters** — `get`/`set` in literals and via `defineProperty`. Accessor descriptors vs data descriptors. Practical patterns (computed properties, validation, compatibility shims).

### 1.8 Prototypes, inheritance

JavaScript's prototype-based inheritance model. Core OOP foundation. Intermediate level, conceptually important.

- **Prototypal inheritance** — `[[Prototype]]` internal slot, `__proto__`, prototype chains, property lookup, `for...in` and inherited properties, `hasOwnProperty`. Writing doesn't use prototype (writes always go to the object itself).
- **F.prototype** — The `.prototype` property of constructor functions, how `new F()` sets `[[Prototype]]`, the default `constructor` property. Distinction between `F.prototype` (the property) and `[[Prototype]]` (the internal link).
- **Native prototypes** — `Object.prototype`, `Array.prototype`, `Function.prototype`, etc. How methods like `[].join` are found via the prototype chain. Prototype pollution (adding to native prototypes — why it's generally discouraged). Borrowing methods from prototypes.
- **Prototype methods, objects without \_\_proto\_\_** — `Object.create`, `Object.getPrototypeOf`/`Object.setPrototypeOf`. Creating "very plain" objects with `null` prototype (e.g., for dictionaries). Modern API vs `__proto__`.

### 1.9 Classes

ES6+ class syntax and patterns. Builds on prototype understanding. Intermediate level.

- **Class basic syntax** — `class` declaration, constructor, methods, what a class really is under the hood (syntactic sugar over prototype-based constructors), differences from plain functions (not hoisted, always strict, enumerable: false for methods).
- **Class inheritance** — `extends`, `super` in methods and constructors, overriding methods, the requirement to call `super()` before `this` in derived constructors, overriding class fields.
- **Static properties and methods** — `static` keyword, inheritance of statics, use cases (factory methods, class-level data).
- **Private and protected properties and methods** — `#privateField` syntax, the convention of `_protectedField` (not enforced). Encapsulation patterns. Read-only via getter without setter.
- **Extending built-in classes** — Subclassing `Array`, `Map`, etc. `Symbol.species` for controlling which constructor built-in methods use internally.
- **Class checking: "instanceof"** — `instanceof` operator, `Symbol.hasInstance`, how it walks the prototype chain. `Object.prototype.toString` as a more reliable type tag.
- **Mixins** — JavaScript's single-inheritance model and how mixins provide a workaround. `Object.assign` to copy methods. EventMixin example. Not a deep treatment of mixin libraries or multiple inheritance theory.

### 1.10 Error handling

Concise coverage of try/catch and custom error types.

- **Error handling, "try...catch"** — Syntax, only catches runtime errors (not parse-time), works synchronously. `catch` binding, the error object (`name`, `message`, `stack`). `throw`, rethrowing, `finally`. `try...catch` around `setTimeout`. Global handler `window.onerror`.
- **Custom errors, extending Error** — Subclassing `Error`, the `name` property, `instanceof` checks in catch, wrapping exceptions. Practical pattern for a `ValidationError` / `ReadError` hierarchy.

### 1.11 Promises, async/await

Comprehensive async programming coverage. Progresses from callbacks through promises to async/await. Intermediate-to-advanced.

- **Introduction: callbacks** — Callback-based async pattern, callback-in-callback (pyramid of doom), error-first callback convention. Motivates the need for promises.
- **Promise** — `new Promise(executor)`, `resolve`/`reject`, `.then`/`.catch`/`.finally`, state machine (pending → fulfilled/rejected), handlers are always async (microtask queue).
- **Promises chaining** — Returning values and promises from `.then`, the chain as a pipeline, `fetch` example. The common mistake of not returning from `.then`.
- **Error handling with promises** — `.catch` placement, implicit `try...catch` in executors and handlers, rethrowing, unhandled rejections (`unhandledrejection` event).
- **Promise API** — `Promise.all`, `Promise.allSettled`, `Promise.race`, `Promise.any`, `Promise.resolve`/`Promise.reject`. Practical scenarios for each.
- **Promisification** — Converting callback-based APIs to promise-based. Helper function pattern.
- **Microtasks** — The microtask queue, promise handlers execute as microtasks, ordering guarantees, `queueMicrotask`.
- **Async/await** — `async` functions always return a promise, `await` pauses execution, error handling with `try...catch`, `await` in loops, top-level `await` in modules. Parallel execution with `Promise.all` + `await`.

### 1.12 Generators, advanced iteration

Two focused articles. Advanced level.

- **Generators** — `function*`, `yield`, the generator object (iterator protocol), `generator.next(value)` for two-way communication, `generator.throw`, `generator.return`, generator composition via `yield*`.
- **Async iteration and generators** — `Symbol.asyncIterator`, `for await...of`, async generators (`async function*`), practical example of paginated data fetching.

### 1.13 Modules

ES modules system. Intermediate level.

- **Modules, introduction** — What modules are, `<script type="module">`, strict mode by default, module-level scope, single evaluation, `import.meta`, `this` is `undefined` at top level, deferred execution.
- **Export and Import** — Named exports/imports, `default` export, re-exporting, `as` for renaming, `import *`, export lists. Best practices.
- **Dynamic imports** — `import()` expression, returns a promise, use cases (conditional loading, computed module paths).

### 1.14 Miscellaneous

Advanced standalone topics. Each article is relatively self-contained. Advanced level.

- **Proxy and Reflect** — `new Proxy(target, handler)`, all traps (`get`, `set`, `has`, `deleteProperty`, `apply`, `construct`, etc.), `Reflect` API, revocable proxies. Detailed treatment — one of the longer articles. Use cases: validation, default values, observable objects, negative array indices.
- **Eval: run a code string** — `eval()`, scope behaviour (strict vs sloppy), why it's almost always avoidable, `new Function` as a safer alternative.
- **Currying** — Currying vs partial application, implementing a curry helper, practical uses in functional patterns.
- **Reference Type** — The internal `Reference Type` specification concept, how it explains why `obj.method()` works but `(obj.method)()` can lose `this` in certain cases. A spec-level explanation.
- **BigInt** — Arbitrary-precision integers, creation (literal `123n` or `BigInt()`), operators, can't mix with `Number`, comparison, polyfills.
- **Unicode, String internals** — Surrogate pairs, combining marks, `String.fromCodePoint`/`codePointAt`, Unicode-aware iteration, normalisation (`normalize`). Deeper than the Strings article in §1.5.
- **WeakRef and FinalizationRegistry** — Weak references for optional caching, `FinalizationRegistry` for cleanup callbacks. Caveats about GC non-determinism. Advanced and niche.

---

## Part 2 — Browser: Document, Events, Interfaces

Covers the browser as a host environment: DOM manipulation, event handling, forms, resource loading. Assumes Part 1 knowledge. Intermediate level throughout.

### 2.1 Document

DOM tree structure and manipulation. The core of browser-side JS.

- **Browser environment, specs** — The `window` object hierarchy: DOM (`document`), BOM (`navigator`, `location`, `alert`, etc.), JavaScript core. Spec references (DOM Living Standard, CSSOM, HTML spec).
- **DOM tree** — Everything is a node: element nodes, text nodes (including whitespace), comment nodes. Browser auto-correction of malformed HTML. The DOM as a tree structure visualised.
- **Walking the DOM** — `document.documentElement`, `.body`, `.head`. Child nodes (`childNodes`, `firstChild`, `lastChild`), siblings (`nextSibling`, `previousSibling`), parent (`parentNode`). Element-only navigation (`children`, `firstElementChild`, etc.). NodeList vs HTMLCollection.
- **Searching: getElement\*, querySelector\*** — `getElementById`, `getElementsByTagName`/`ClassName` (live collections), `querySelectorAll`/`querySelector` (static), `matches`, `closest`. When to use which.
- **Node properties: type, tag and contents** — `nodeType`, `nodeName`/`tagName`, `innerHTML`, `outerHTML`, `textContent`, `nodeValue`/`data` for text nodes, `hidden` property. Differences between `innerHTML` and `textContent` (security: XSS via innerHTML).
- **Attributes and properties** — DOM properties vs HTML attributes, synchronisation, `getAttribute`/`setAttribute`/`removeAttribute`, `dataset` for custom `data-*` attributes, non-standard attributes.
- **Modifying the document** — Creating elements (`createElement`, `createTextNode`), insertion methods (`append`, `prepend`, `before`, `after`, `replaceWith`), `insertAdjacentHTML/Text/Element`, `remove`, `cloneNode`, `DocumentFragment`. Old-school methods (`appendChild`, `insertBefore`) mentioned.
- **Styles and classes** — `className`, `classList` (`.add`/`.remove`/`.toggle`/`.contains`), `style` property (camelCase), `style.cssText`, computed styles via `getComputedStyle`. When to use classes vs inline styles.
- **Element size and scrolling** — `offsetParent`/`offsetLeft`/`offsetTop`, `offsetWidth`/`offsetHeight`, `clientTop`/`clientLeft`/`clientWidth`/`clientHeight`, `scrollWidth`/`scrollHeight`/`scrollTop`/`scrollLeft`. Geometry diagram. CSS `box-sizing` implications.
- **Window sizes and scrolling** — `document.documentElement.clientWidth/Height` (viewport), `scrollWidth/Height` of the document, `window.scrollX/Y` (`pageXOffset`/`pageYOffset`), `scrollTo`/`scrollBy`/`scrollIntoView`.
- **Coordinates** — `getBoundingClientRect` (client/viewport coordinates), `elementFromPoint`, document coordinates (client + scroll), converting between the two systems.

### 2.2 Introduction to Events

Event model fundamentals.

- **Introduction to browser events** — Common event types (mouse, keyboard, form, document, CSS), three ways to assign handlers (HTML attribute, DOM property, `addEventListener`/`removeEventListener`), the event object, `handleEvent` interface for object-based handlers.
- **Bubbling and capturing** — Bubbling phase (target → root), `event.target` vs `this`/`currentTarget`, `stopPropagation`/`stopImmediatePropagation`, capturing phase (`{capture: true}`), the three-phase model.
- **Event delegation** — Handling events on a common ancestor, using `event.target` + `closest`, the `data-action` pattern, `focusin`/`focusout` for delegating focus. Benefits (less memory, dynamic elements) and limitations.
- **Browser default actions** — `event.preventDefault()`, `passive: true` for scroll-related events, the `defaultPrevented` property for inter-handler communication, `return false` in `on<event>` attributes.
- **Dispatching custom events** — `new Event()` / `new CustomEvent()`, `dispatchEvent`, `detail` property, `bubbles`/`cancelable` options, synchronous dispatch. Building custom component events.

### 2.3 UI Events

Specific event categories in detail.

- **Mouse events** — `click`, `dblclick`, `mousedown`/`mouseup`, `contextmenu`. Modifier keys (`shiftKey`, `ctrlKey`, `altKey`, `metaKey`), button property, coordinates (`clientX/Y`, `pageX/Y`). Event order.
- **Moving the mouse: mouseover/out, mouseenter/leave** — `mouseover`/`mouseout` with `relatedTarget`, event frequency, `mouseenter`/`mouseleave` (no bubbling, no triggers for child elements). Building tooltip and hover effects.
- **Drag'n'Drop with mouse events** — Implementing drag and drop from scratch with `mousedown`/`mousemove`/`mouseup`. Drop targets, droppable detection via `elementFromPoint`. `ondragstart` returning `false` to prevent native drag.
- **Pointer events** — `pointerdown`/`pointerup`/`pointermove`/etc. Unified model for mouse, touch, and pen. `pointerId`, `pointerType`, `isPrimary`. `setPointerCapture`. Why pointer events supersede both mouse and touch events.
- **Keyboard: keydown and keyup** — `event.key` (character) vs `event.code` (physical key), auto-repeat, default actions (e.g., preventing non-digit input). Legacy `keypress` mentioned as deprecated.
- **Scrolling** — The `scroll` event, detecting scroll position, show/hide elements on scroll, preventing scroll (and the difficulty thereof).

### 2.4 Forms, controls

Form element specifics.

- **Form properties and methods** — `document.forms`, named access, `form.elements`, backreference `element.form`, `input.value`/`checked`/`select.options`/`select.selectedIndex`, `option` creation.
- **Focusing: focus/blur** — `focus`/`blur` events and methods, `tabindex`, `focusin`/`focusout` (bubble), `activeElement`, `autofocus`. Delegating focus events.
- **Events: change, input, cut, copy, paste** — `change` (fires on loss of focus for text inputs), `input` (fires on every edit), clipboard events (`cut`/`copy`/`paste`, `clipboardData`). `event.preventDefault()` for clipboard control.
- **Forms: event and method submit** — `submit` event, `form.submit()` (doesn't trigger `submit` event), validation before submission, preventing double-submission.

### 2.5 Document and resource loading

Page lifecycle and script loading.

- **Page: DOMContentLoaded, load, beforeunload, unload** — `DOMContentLoaded` (DOM ready, images may still load), `load` (everything loaded), `beforeunload` (confirm leaving), `unload` (cleanup). `readyState` and `readystatechange`.
- **Scripts: async, defer** — `defer`: loads in parallel, executes after DOM parsed, in order. `async`: loads in parallel, executes immediately when loaded, no order guarantee. `DOMContentLoaded` and their interaction. Dynamic scripts.
- **Resource loading: onload and onerror** — `load`/`error` events on `<script>`, `<img>`, `<link>`. Cross-origin policy for error details. `window.onerror` for global script errors.

### 2.6 Miscellaneous (Browser)

Advanced browser topics.

- **Mutation observer** — `MutationObserver` API: observing DOM changes (childList, attributes, characterData, subtree). Use cases: auto-highlighting, integration with third-party scripts, tracking dynamic content.
- **Selection and Range** — `Range` object (start/end containers and offsets), `Selection` object, programmatic selection of DOM content and form inputs, `contentEditable`. Fairly detailed.
- **Event loop: microtasks and macrotasks** — The event loop in the browser: macrotask → all microtasks → render. Splitting CPU-heavy tasks with `setTimeout(0)`, progress indication, `queueMicrotask`. Relationship between the event loop and UI rendering.

---

## Part 3 — Additional Articles

Standalone topic clusters. Assume knowledge of Parts 1 and 2. No prescribed reading order. Range from intermediate to advanced.

### 3.1 Frames and windows

Cross-window and security topics.

- **Popups and window methods** — `window.open`, popup blockers, window features string, `window.close`, `window.closed`, scrolling/resizing popups, focusing windows.
- **Cross-window communication** — Same-origin policy, accessing content of iframes/popups, `postMessage` / `message` event for cross-origin communication, the `origin` check.
- **The clickjacking attack** — What clickjacking is (transparent iframe overlay), `X-Frame-Options` header, `sandbox` attribute, defensive JavaScript techniques.

### 3.2 Binary data, files

Binary data handling in the browser.

- **ArrayBuffer, binary arrays** — `ArrayBuffer` as raw memory, typed arrays (`Uint8Array`, `Float64Array`, etc.), `DataView` for mixed-format binary data, conversions between them.
- **TextDecoder and TextEncoder** — Decoding `ArrayBuffer`/typed arrays to strings (`TextDecoder`), encoding strings to bytes (`TextEncoder`). UTF-8 focus.
- **Blob** — `Blob` as high-level binary data, creating blobs, `blob:` URLs via `URL.createObjectURL`, downloading blobs, blob-to-base64, `Blob` to/from `ArrayBuffer`.
- **File and FileReader** — `File` extends `Blob`, `<input type="file">`, `FileReader` (readAsText, readAsDataURL, readAsArrayBuffer), reading progress, `FileReaderSync` for Web Workers.

### 3.3 Network requests

Comprehensive networking coverage. The longest section in Part 3.

- **Fetch** — Basic `fetch(url, options)`, response handling (`.json()`, `.text()`, `.blob()`), response headers, request headers, POST requests with JSON and FormData.
- **FormData** — `new FormData(form)`, `append`/`set`/`delete`/`get`, sending with `fetch`, appending files, sending form-like data without an actual form.
- **Fetch: Download progress** — Reading the response body chunk-by-chunk via `response.body` (ReadableStream), tracking download progress with `reader.read()`.
- **Fetch: Abort** — `AbortController`, `signal` option in `fetch`, aborting multiple requests, custom abortable operations.
- **Fetch: Cross-Origin Requests** — CORS explained: simple vs preflighted requests, `Origin`/`Access-Control-Allow-Origin` headers, credentialed requests, response header access restrictions. Fairly detailed CORS treatment.
- **Fetch API** — Comprehensive reference of all `fetch` options: `method`, `headers`, `body`, `mode`, `credentials`, `cache`, `redirect`, `referrer`, `referrerPolicy`, `integrity`, `keepalive`, `signal`.
- **URL objects** — `new URL()`, `searchParams`, encoding, comparison with string URLs.
- **XMLHttpRequest** — The legacy API. Open/send/events pattern, response types, progress tracking, upload progress, cross-origin, `abort`, synchronous requests (deprecated). Included primarily for encountering legacy code.
- **Resumable file upload** — Implementing resumable uploads using custom protocol (check offset → send from that byte). Server interaction pattern.
- **Long polling** — The long polling pattern (request → server holds → event → response → reconnect). Comparison with WebSocket. Server-side timeout handling.
- **WebSocket** — `new WebSocket(url)`, open/message/error/close events, sending data (text and binary), connection states, closing handshake, bufferedAmount, rate limiting.
- **Server Sent Events** — `EventSource` API, auto-reconnect, `Last-Event-ID`, named events, connection lifecycle, comparison with WebSocket (unidirectional, auto-reconnect, simpler protocol).

### 3.4 Storing data in the browser

Client-side storage mechanisms.

- **Cookies, document.cookie** — Reading/writing cookies, `path`, `domain`, `expires`/`max-age`, `secure`, `samesite`, `httpOnly` (server-only), size limits, `encodeURIComponent`. Third-party cookies.
- **LocalStorage, sessionStorage** — Key-value string storage. Differences (session vs persistent, tab scope). `setItem`/`getItem`/`removeItem`/`clear`/`key`/`length`. The `storage` event for cross-tab communication.
- **IndexedDB** — Transactional object store database. Opening/versioning, object stores, transactions, CRUD operations, key ranges, cursors, indexes. Promise wrapper libraries mentioned. The most complex article in this section.

### 3.5 Animation

CSS and JS animation techniques.

- **Bezier curve** — Mathematical definition, control points, common curves (ease, ease-in, ease-out), CSS `cubic-bezier()`. Visual/interactive approach.
- **CSS-animations** — `transition` (property, duration, timing-function, delay), `@keyframes` + `animation`, `transitionend`/`animationend` events. Practical examples.
- **JavaScript animations** — `requestAnimationFrame`-based animation loop, timing functions (linear, power, elastic, bounce), applying timing functions for various effects. When to use JS vs CSS animations.

### 3.6 Web components

The Web Components standard suite.

- **From the orbital height** — Overview of the four standards: Custom Elements, Shadow DOM, Templates, HTML Imports (deprecated). Motivation and browser support.
- **Custom elements** — `customElements.define`, autonomous vs customised built-in elements, lifecycle callbacks (`connectedCallback`, `disconnectedCallback`, `attributeChangedCallback`, `adoptedCallback`), `observedAttributes`. Upgrade timing.
- **Shadow DOM** — `element.attachShadow({mode})`, encapsulation of styles and DOM, built-in shadow DOM in browser elements (e.g., `<input type="range">`). `mode: 'open'` vs `'closed'`.
- **Template element** — `<template>` tag, inert content, `template.content` (DocumentFragment), cloning for instantiation.
- **Shadow DOM slots, composition** — `<slot>` elements, named and default slots, `slotchange` event, flattened DOM. How light DOM composes into shadow DOM.
- **Shadow DOM styling** — `:host`, `:host()`, `:host-context()`, `::slotted()`, CSS custom properties for theming through the shadow boundary.
- **Shadow DOM and events** — Event retargeting in shadow DOM, bubbling through shadow boundaries, `composed` flag, `composedPath()`.

### 3.7 Regular expressions

Thorough regex tutorial from basics to advanced. One of the most extensive sections, standalone and self-contained.

- **Patterns and flags** — `/.../` syntax and `new RegExp()`, flags `g`, `i`, `m`, `s`, `u`, `y`. `str.match`, `str.replace` basics.
- **Character classes** — `\d`, `\s`, `\w` and their negations `\D`, `\S`, `\W`. The dot `.` and its behaviour with/without `s` flag.
- **Unicode: flag "u" and class \\p{...}** — Correct handling of surrogate pairs with `u` flag, Unicode property escapes (`\p{Letter}`, `\p{Script=Cyrillic}`, etc.).
- **Anchors: string start ^ and end $** — Matching at boundaries, testing full-string match, multiline interaction.
- **Multiline mode of anchors ^ $, flag "m"** — Per-line matching with `m` flag.
- **Word boundary: \\b** — What `\b` matches (transition between `\w` and `\W`), common use cases (whole word search).
- **Escaping, special characters** — Which characters need escaping in regex, escaping in `new RegExp()` with strings (double backslash).
- **Sets and ranges [...]** — Character sets, ranges (`[a-z]`), negation (`[^...]`), no escaping needed for most special chars inside sets.
- **Quantifiers +, \*, ? and {n}** — `{n}`, `{n,m}`, `+`, `*`, `?` shorthands, applying to characters vs groups.
- **Greedy and lazy quantifiers** — Default greedy behaviour, lazy variants (`+?`, `*?`, `??`), the alternative approach using negated sets. Detailed explanation of the matching engine's backtracking.
- **Capturing groups** — `(...)` for capture, numbered groups in results and `$1` in replacement, non-capturing `(?:...)`, named groups `(?<name>...)`.
- **Backreferences in pattern: \\N and \\k\<n\>** — `\1`, `\2` etc. for matching same text again, named backreferences `\k<name>`.
- **Alternation (OR) |** — `|` operator, alternation scope within groups.
- **Lookahead and lookbehind** — `(?=...)`, `(?!...)`, `(?<=...)`, `(?<!...)`. Zero-width assertions. Practical examples (password validation, number formatting).
- **Catastrophic backtracking** — Why certain patterns are exponentially slow, how to diagnose and fix (atomic groups, possessive quantifiers where supported, rewriting patterns). Important practical topic.
- **Sticky flag "y", searching at position** — `y` flag behaviour: match only at `lastIndex`, use cases for tokenizers/parsers.
- **Methods of RegExp and String** — Comprehensive reference: `str.match`, `str.matchAll`, `str.search`, `str.replace`, `str.replaceAll`, `str.split`, `regexp.exec`, `regexp.test`. Flag interactions. When to use which method.

---

## Notes on scope and depth

- **Exercises**: Most articles include tasks/exercises with solutions (expandable). The tutorial is hands-on.
- **Level**: Progresses from zero-knowledge beginner (Part 1 early chapters) to intermediate/advanced (Part 1 later chapters, Part 3). Part 2 is mostly intermediate.
- **Coverage**: Comprehensive for the language and browser API fundamentals. Does **not** cover: Node.js, TypeScript, any framework (React/Vue/Angular), build tools (Webpack/Vite), testing frameworks beyond Mocha basics, or server-side concerns.
- **Currency**: Kept up to date with modern JS (ES2020+ features like optional chaining, nullish coalescing, WeakRef, etc. are included). Some legacy coverage (`var`, `XMLHttpRequest`, `arguments`) is explicitly marked as historical.
- **Style**: Explanatory with runnable examples in an inline sandbox. Each article is self-contained but linked in sequence. Suitable both for linear study and for reference.
