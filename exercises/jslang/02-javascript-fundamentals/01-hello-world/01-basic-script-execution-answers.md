# Step 1 Answer Key: Basic Script Execution

## Snippet 1

**Output:**
```
A
B
Hello
C
D
```

**Rationale:** Script blocks execute top-to-bottom in document order. The first `<script>` logs "A". The `<p id="middle">` is then parsed. The second `<script>` logs "B", then accesses the `<p>` (which is above it in the document and already parsed), getting its textContent "Hello", then logs "C". The third `<script>` logs "D". Each script block runs to completion before the next begins.

## Snippet 2

**Output:**
```
E: before external
G: after external
Above
```

**Rationale:**
- "E: before external" prints normally from the inline script.
- "F: inside src script" **never executes**. The `<script>` tag has a `src` attribute, so the inline content between the tags is completely ignored — regardless of whether the external file loads successfully or not.
- The failed load of `nonexistent-file.js` does **not** prevent subsequent scripts from running. The browser logs a network error in the console but continues parsing. "G: after external" prints, followed by "Above" from the `<div>`'s textContent.

**Key concepts tested:**
- Script execution order (document order, top-to-bottom)
- Scripts can access DOM elements that appear above them
- The `src` attribute causes inline content to be ignored
- A failed external script load doesn't block subsequent scripts
