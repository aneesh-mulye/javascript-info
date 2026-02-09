# Step 3 Answer Key: matches, closest, and Combined Searching

## Snippet 1

**Output:**
```
true
true
true
false
P
DIV
warning
null
true
```

**Rationale:**

`target` is the `<em id="target1">warning</em>` element, nested inside: `<p>` inside `<div class="panel-body">` inside `<div class="panel" data-type="warning">`.

1. `target.matches("em")` is `true` -- the element is an `<em>`, so it matches the tag selector.

2. `target.matches(".panel-body em")` is `true` -- `matches()` checks if the element would be selected by the CSS selector **within the document context**. The `<em>` is indeed an `<em>` inside a `.panel-body` in the document, so it matches.

3. `target.matches("#target1")` is `true` -- it has `id="target1"`.

4. `target.matches("div")` is `false` -- it is an `<em>`, not a `<div>`.

5. `target.closest("p").tagName` is `P` -- `closest("p")` walks up from the `<em>` (inclusive) and finds the parent `<p>`. `tagName` returns uppercase.

6. `target.closest(".panel-body").tagName` is `DIV` -- `closest(".panel-body")` walks up and finds `<div class="panel-body">`. Its tag is `DIV`.

7. `target.closest(".panel").dataset.type` is `warning` -- `closest(".panel")` finds `<div class="panel" data-type="warning">`. The `dataset.type` property reads the `data-type` attribute.

8. `target.closest(".panel-title")` is `null` -- `.panel-title` is the `<strong>` in the `panel-header`, which is a sibling branch, NOT an ancestor of `target`. `closest()` only walks **up** the ancestor chain (including self), so it returns `null`.

9. `target.closest("em") === target` is `true` -- `closest()` checks the element itself first. Since `target` is an `<em>`, `closest("em")` returns `target` itself.

## Snippet 2

**Output:**
```
2
Save, Submit
section-a, section-b
btn+primary, btn+danger, btn
null
```

**Rationale:**

The DOM has two sections with buttons:
- `section-a`: "Save" (btn primary), "Cancel" (btn)
- `section-b`: "Submit" (btn primary), "Delete" (btn danger), "Reset" (btn)

1. `primaryBtns.length` is `2` -- `querySelectorAll(".btn")` gets all 5 buttons, then `.filter(btn => btn.matches(".primary"))` keeps only those with class `primary`: "Save" and "Submit".

2. `primaryBtns.map(b => b.textContent).join(", ")` is `Save, Submit` -- the text content of the two primary buttons.

3. `sections.join(", ")` is `section-a, section-b` -- for each primary button, `closest("section").className` finds the parent section. "Save" is in `section-a`, "Submit" is in `section-b`.

4. `classLists.join(", ")` is `btn+primary, btn+danger, btn` -- for each button in section-b, `Array.from(btn.classList).sort().join("+")` converts the classList to a sorted array joined by `+`:
   - "Submit": classes `btn`, `primary` -> sorted: `btn`, `primary` -> `btn+primary`
   - "Delete": classes `btn`, `danger` -> sorted: `btn`, `danger` -> `btn+danger`
   - "Reset": class `btn` only -> sorted: `btn` -> `btn`

5. `dangerBtn.closest(".section-a")` is `null` -- the "Delete" button is inside `section-b`. `closest()` only walks up ancestors, and `.section-a` is a sibling section, not an ancestor. So it returns `null`.

**Key concepts tested:**
- `matches(selector)` checks if an element satisfies a CSS selector, evaluated in the context of the document
- `closest(selector)` walks up the ancestor chain (including the element itself) and returns the first match, or `null`
- `closest()` cannot find siblings or elements in different branches of the DOM tree
- Combining `querySelectorAll` with `Array.from` and `.filter` using `matches` for flexible element selection
- Using `closest` to classify or categorize elements by their ancestors
- `classList` returns a DOMTokenList; `Array.from` converts it for array methods
- `dataset` property for reading `data-*` attributes
- Part 1 integration: `Array.from`, `.map`, `.filter`, `.join`, spread operator, arrow functions
