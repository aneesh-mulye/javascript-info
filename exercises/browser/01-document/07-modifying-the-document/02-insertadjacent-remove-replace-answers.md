# Step 2 Answer Key: insertAdjacentHTML, remove, replaceWith

## Snippet 1

**Output:**
```
SPAN:BB | P:AB-Anchor paragraph-BE | SPAN:AE
```
```
<b>AB-</b>Anchor paragraph<i>-BE</i>
```

**Rationale:**

The four `insertAdjacentHTML` positions on `anchor1` (`<p id="anchor1">`), which is a child of `wrapper1`:

1. `'beforebegin'` inserts `<span>BB</span>` as a **sibling before** anchor1 inside wrapper1.
2. `'afterbegin'` inserts `<b>AB-</b>` as the **first child** inside anchor1.
3. `'beforeend'` inserts `<i>-BE</i>` as the **last child** inside anchor1.
4. `'afterend'` inserts `<span>AE</span>` as a **sibling after** anchor1 inside wrapper1.

So wrapper1's element children are: `<span>BB</span>`, `<p>` (anchor1), `<span>AE</span>`.

- `SPAN:BB` -- the beforebegin span
- `P:AB-Anchor paragraph-BE` -- the paragraph's textContent includes the `<b>` text "AB-", the original text "Anchor paragraph", and the `<i>` text "-BE"
- `SPAN:AE` -- the afterend span

`anchor1.innerHTML` shows the raw HTML inside the `<p>`: `<b>AB-</b>Anchor paragraph<i>-BE</i>`.

## Snippet 2

**Output:**
```
4
text node
<li>Not a real item</li>
Alpha, Parsed item, Omega
```

**Rationale:**

1. `liBeta.insertAdjacentHTML('afterend', '<li id="li-parsed">Parsed <b>item</b></li>')` -- inserts a **real parsed `<li>`** element after Beta. This is `insertAdjacentHTML`, which **parses** the string as HTML. The list is now: Alpha, Beta, Parsed item, Gamma.

2. `list2.append('<li>Not a real item</li>')` -- appends a **text node** (not a real `<li>`), because `append` treats strings as text. So the list now has 4 `<li>` elements (Alpha, Beta, Parsed item, Gamma) plus a trailing text node.

3. `list2.querySelectorAll('li').length` is **4** (Alpha, Beta, Parsed item, Gamma).

4. The last child node of list2 is the text node from `append`. Its `nodeType` is 3 (text node), so it prints `text node`. Its trimmed textContent is `<li>Not a real item</li>` (the literal string).

5. `liBeta.remove()` removes Beta from the list.

6. `liGamma.replaceWith(liOmega)` replaces Gamma with a new `<li>Omega</li>`.

7. Final `<li>` elements: Alpha, Parsed item, Omega. Their textContent joined: `Alpha, Parsed item, Omega`.

**Key concepts tested:**
- `insertAdjacentHTML` **parses** its string argument as HTML -- creates real DOM elements
- `append` with a string creates a **text node** -- does NOT parse HTML
- The four positions of `insertAdjacentHTML`: `beforebegin`, `afterbegin`, `beforeend`, `afterend`
- `remove()` detaches an element from the DOM (but the JS reference still exists)
- `replaceWith()` replaces an element with another node; the replaced element is detached but still referenceable
