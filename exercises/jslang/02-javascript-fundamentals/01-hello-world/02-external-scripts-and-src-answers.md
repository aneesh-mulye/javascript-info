# Step 2 Answer Key: External Scripts and the src Gotcha

## Snippet 1

**Output:**
```
external-hello.js loaded
function
Hello, World!
__externalHelloLoaded: true
__inlineRan: undefined
```

**Rationale:**
- `external-greet.js` loads first (via `<script src="external-greet.js">`), defining `greet()` and setting `window.__externalGreetLoaded = true`.
- The next inline script accesses `greet`: `typeof greet` is `"function"`, and `greet("World")` returns `"Hello, World!"`.
- Then `<script src="external-hello.js">` loads. The external file logs `"external-hello.js loaded"` and sets `window.__externalHelloLoaded = true`. The inline content (`console.log("This line...")` and `window.__inlineRan = true`) is **completely ignored** because the tag has a `src` attribute.
- The final inline script checks: `__externalHelloLoaded` is `true` (set by the external file), but `__inlineRan` is `undefined` (the inline content was never executed).

**Key concepts tested:**
- External scripts make their definitions available to subsequent scripts
- The `src` attribute causes inline content to be ignored (the core gotcha)
- The ignored inline code doesn't even set variables — it's as if it doesn't exist

## Snippet 2

**Output:**
```
type=text/javascript ran
language=JavaScript ran
text/plain scripts found: 1
content accessible: true
```

**Rationale:**
- `type="text/javascript"` is the default and executes normally.
- `language="JavaScript"` is deprecated but still recognized — the script executes.
- `type="text/plain"` is **not** a JavaScript MIME type, so the browser does **not** execute that script. `"type=text/plain ran"` never prints.
- However, the non-executing script's content is still in the DOM as a `<script>` element. `querySelectorAll` finds it, and its `textContent` is accessible — it just wasn't executed as code. This is actually a pattern sometimes used for client-side templates.

**Key concepts tested:**
- `type="text/javascript"` is the default (explicit or implicit) — executes normally
- `language` is deprecated but harmless — script still runs
- A non-JavaScript `type` value prevents execution entirely
- Non-executing scripts are still DOM elements with accessible textContent
