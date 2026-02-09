# Step 3 Answer Key: Combined Multi-Level Navigation

## Snippet 1

**Output:**
```
3
Note
7
Item B
snippet1
true
true
```

**Rationale:**

The DOM structure:
```html
<div id="snippet1">
    <section>
        <h2>Heading</h2>
        <ul>
            <li>Item A</li>
            <li>Item B</li>
            <li>Item C</li>
        </ul>
    </section>
    <aside>
        <p>Note</p>
    </aside>
</div>
```

`<div id="snippet1">` element children: `<section>` and `<aside>`.

`<section>` element children: `<h2>` and `<ul>`.

`<ul>` element children: 3 `<li>` elements.

`<ul>` child nodes (with whitespace):
- Index 0: Text (whitespace)
- Index 1: `<li>Item A</li>`
- Index 2: Text (whitespace)
- Index 3: `<li>Item B</li>`
- Index 4: Text (whitespace)
- Index 5: `<li>Item C</li>`
- Index 6: Text (whitespace)

1. **Chain 1:** `s1.firstElementChild` is `<section>`. `.lastElementChild` is `<ul>`. `.children.length` is `3` (the three `<li>` elements).

2. **Chain 2:** `s1.firstElementChild` is `<section>`. `.nextElementSibling` is `<aside>`. `.firstElementChild` is `<p>`. `.textContent` is `Note`.

3. **Chain 3:** `ul.childNodes.length` is `7` -- 4 whitespace text nodes + 3 `<li>` elements.

4. **Chain 3 continued:** `ul.childNodes[3].textContent` is `Item B` -- index 3 is the second `<li>`.

5. **Chain 4:** `lastLi` is `<li>Item C</li>`. `.parentNode` is `<ul>`. `.parentNode` is `<section>`. `.parentNode` is `<div id="snippet1">`. `.id` is `snippet1`.

6. **Chain 5:** `document.documentElement.parentNode === document` is `true` -- the parent node of `<html>` is the document itself.

7. **Chain 5 continued:** `document.documentElement.parentElement === null` is `true` -- `parentElement` returns `null` because the document is not an element. `parentElement` only returns element parents, and the document node is not an element (it is nodeType 9).

## Snippet 2

**Output:**
```
2
TBODY
2
Alice, Bob
TD -> TR -> TBODY -> TABLE -> BODY -> HTML
```

**Rationale:**

The DOM structure for the table:
```html
<table id="snippet2">
    <thead>
        <tr><th>Name</th><th>Score</th></tr>
    </thead>
    <tbody>
        <tr><td>Alice</td><td>90</td></tr>
        <tr><td>Bob</td><td>85</td></tr>
    </tbody>
</table>
```

`<table>` element children: `<thead>` and `<tbody>`.

1. `table.children.length` is `2` -- `<thead>` and `<tbody>`.

2. `table.lastElementChild` is `<tbody>`. `tbody.tagName` is `TBODY` (tagName is always uppercase).

3. `tbody.children.length` is `2` -- the two `<tr>` rows in `<tbody>`.

4. `Array.from(tbody.children).map(tr => tr.firstElementChild.textContent)` maps each `<tr>` to its first `<td>`'s text content: `"Alice"` and `"Bob"`. `.join(", ")` produces `Alice, Bob`.

5. The ancestor walk: starting from `aliceTd` (the `<td>` containing "Alice"), walk up via `parentElement` and collect `nodeName`:
   - `TD` (the `<td>` itself)
   - `TR` (parentElement of `<td>`)
   - `TBODY` (parentElement of `<tr>`)
   - `TABLE` (parentElement of `<tbody>`)
   - `BODY` (parentElement of `<table>`)
   - `HTML` (parentElement of `<body>`)
   - Then `parentElement` of `<html>` is `null`, so the loop stops.

   Result: `TD -> TR -> TBODY -> TABLE -> BODY -> HTML`.

   Note: `nodeName` (like `tagName`) returns uppercase for element nodes. The walk uses `parentElement`, not `parentNode`, so it stops at `<html>` (since `<html>`'s `parentElement` is `null`; the document is not an element).

**Key concepts tested:**
- Chaining element-only navigation across multiple nested levels
- `firstElementChild`, `lastElementChild`, `nextElementSibling` skip all non-element nodes
- `childNodes` still includes whitespace text nodes even when navigating deeply
- `parentNode` vs `parentElement` at the top of the DOM tree: `parentNode` of `<html>` is the document, but `parentElement` is `null`
- `tagName`/`nodeName` always returns uppercase for elements
- `Array.from()` and `.map()` for converting collections and extracting data (Part 1 integration)
- The ancestor walk pattern using a `while` loop with `parentElement`
