# Step 2 Answer Key: Element-Only Navigation

## Snippet 1

**Output:**
```
7
2
false
a
Two
3
Two
```

**Rationale:**

The `<div id="snippet1">` has its content on multiple lines with indentation:

```html
<div id="snippet1">
  <!-- greeting -->
  <span class="a">One</span>
  <span class="b">Two</span>
</div>
```

Child nodes of `<div id="snippet1">`:
- Index 0: Text node (`"\n  "` -- after opening `<div>`)
- Index 1: Comment node (`<!-- greeting -->`)
- Index 2: Text node (`"\n  "` -- between comment and first `<span>`)
- Index 3: `<span class="a">One</span>` element
- Index 4: Text node (`"\n  "` -- between the two `<span>`s)
- Index 5: `<span class="b">Two</span>` element
- Index 6: Text node (`"\n"` -- before closing `</div>`)

Element children (filtered): `<span class="a">` and `<span class="b">`.

1. `s1.childNodes.length` is `7` -- 4 text nodes (whitespace) + 1 comment node + 2 `<span>` elements = 7.
2. `s1.children.length` is `2` -- `children` only includes element nodes: the two `<span>`s.
3. `s1.firstChild === s1.firstElementChild` is `false` -- `firstChild` is the whitespace text node at index 0, while `firstElementChild` is `<span class="a">` at index 3. They are different objects.
4. `s1.firstElementChild.className` is `a` -- the first element child is `<span class="a">`.
5. `s1.lastElementChild.textContent` is `Two` -- the last element child is `<span class="b">Two</span>`.
6. `s1.firstElementChild.nextSibling.nodeType` is `3` -- `firstElementChild` is `<span class="a">` (index 3). Its `nextSibling` is the text node at index 4 (whitespace), which has nodeType 3 (Text).
7. `s1.firstElementChild.nextElementSibling.textContent` is `Two` -- `nextElementSibling` skips text nodes and goes directly to `<span class="b">`.

## Snippet 2

**Output:**
```
3
7
Banana
true
true
false
Banana
true
```

**Rationale:**

The `<ul id="snippet2">` contains:
```html
<ul id="snippet2">
  <li>Apple</li>
  <li>Banana</li>
  <li>Cherry</li>
</ul>
```

Child nodes:
- Index 0: Text node (whitespace)
- Index 1: `<li>Apple</li>`
- Index 2: Text node (whitespace)
- Index 3: `<li>Banana</li>`
- Index 4: Text node (whitespace)
- Index 5: `<li>Cherry</li>`
- Index 6: Text node (whitespace)

Element children: 3 `<li>` elements.

1. `items.length` is `3` -- `children` returns only the 3 `<li>` elements.
2. `allNodes.length` is `7` -- 4 text nodes (whitespace) + 3 `<li>` elements.
3. `items[1].textContent` is `Banana` -- the second element child.
4. `allNodes[1] === items[0]` is `true` -- `childNodes[1]` is the first `<li>`, which is the same as `children[0]`.
5. `items[0].nextElementSibling === items[1]` is `true` -- `nextElementSibling` of the first `<li>` is the second `<li>`, which is `children[1]`.
6. `items[0].nextSibling === items[1]` is `false` -- `nextSibling` of the first `<li>` (childNodes[1]) is the whitespace text node at childNodes[2], NOT the second `<li>`.
7. `items[2].previousElementSibling.textContent` is `Banana` -- the previous element sibling of Cherry is Banana.
8. `s2.children instanceof HTMLCollection` is `true` -- `children` returns an `HTMLCollection`.

**Key concepts tested:**
- `children` vs `childNodes`: `children` skips text and comment nodes, `childNodes` includes all
- `firstChild` vs `firstElementChild`: the former can be a text node, the latter is always an element
- `nextSibling` vs `nextElementSibling`: the former moves to any node (often whitespace text), the latter skips to the next element
- `children` returns an `HTMLCollection` (not a `NodeList`)
- Element-only navigation properties ignore whitespace text nodes entirely
