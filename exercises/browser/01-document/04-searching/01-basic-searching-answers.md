# Step 1 Answer Key: getElementById and querySelector Basics

## Snippet 1

**Output:**
```
DIV
Hello
2
null
null
Important
```

**Rationale:**

1. `box.tagName` is `DIV` -- `getElementById("box")` returns the `<div id="box">` element. `tagName` always returns uppercase.

2. `firstIntro.textContent` is `Hello` -- `querySelector(".intro")` returns the **first** element matching the CSS selector `.intro`, which is the first `<p class="intro">Hello</p>`.

3. `allIntros.length` is `2` -- `querySelectorAll(".intro")` returns a NodeList of **all** matching elements: both `<p class="intro">` elements.

4. `missing` is `null` -- `getElementById` returns `null` when no element with that ID exists.

5. `missingQ` is `null` -- `querySelector` also returns `null` when no match is found.

6. `spanInBox.textContent` is `Important` -- `querySelector("#box span")` uses a descendant CSS selector to find the first `<span>` inside `#box`, which is `<span id="highlight">Important</span>`.

## Snippet 2

**Output:**
```
Dashboard
Logout
item active
Dashboard
Dashboard
```

**Rationale:**

1. `menuItem.textContent.trim()` is `Dashboard` -- `querySelector("#menu .item")` finds the first element with class `item` that is a descendant of `#menu`. That is the first `<li class="item active">Dashboard</li>`. After `.trim()`, the text is `Dashboard`.

2. `link.textContent` is `Logout` -- the attribute selector `a[href='/logout']` matches the anchor element inside the third `<li>`.

3. `firstLi.className` is `item active` -- `li:first-child` inside `#menu` selects the first `<li>`. Its `className` property returns the full class attribute string: `"item active"`.

4. `itemInMenu.textContent.trim()` is `Dashboard` -- `menu.querySelector(".item")` searches within `menu` (the `<ul id="menu">`). It finds the first `.item` descendant, which is the first `<li>`.

5. `scoped` output is `Dashboard` -- This is a subtle point. `menu.querySelector("#menu .item")` does **not** return `null`. Even though `querySelector` is called on `menu` (the `<ul id="menu">` element), the CSS selector `#menu .item` is evaluated against the **entire document** and then filtered to only descendants of `menu`. Since the first `<li class="item active">` both matches `#menu .item` (it is a `.item` descendant of `#menu` in the full document) AND is a descendant of `menu`, it is found. The selector is matched globally; the element scoping only restricts which results are returned, not how the selector is parsed. So `scoped.textContent.trim()` is `Dashboard`.

**Key concepts tested:**
- `getElementById` returns a single element or `null`
- `querySelector` returns the **first** match or `null`
- `querySelectorAll` returns a static NodeList of all matches
- CSS selector syntax works in `querySelector`/`querySelectorAll`: class selectors, ID selectors, descendant combinators, attribute selectors, pseudo-classes
- `tagName` is always uppercase
- `className` returns the full class attribute as a string
- `querySelector` called on an element scopes results to descendants, but the selector itself is evaluated in the context of the full document (the `:scope` behavior subtlety)
