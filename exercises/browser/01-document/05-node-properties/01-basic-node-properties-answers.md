# Step 1 Answer Key: Basic Node Properties

## Snippet 1

**Output:**
```
Node 0: type=3, nodeName="#text", tagName=undefined
Node 1: type=1, nodeName="P", tagName=P
Node 2: type=3, nodeName="#text", tagName=undefined
Node 3: type=8, nodeName="#comment", tagName=undefined
Node 4: type=3, nodeName="#text", tagName=undefined
---
P
P
#text
undefined
```

**Rationale:** The `<div id="container">` has five child nodes when you look at `childNodes`:
1. A text node (the whitespace/newline after `<div>` and before `<p>`) -- nodeType 3, nodeName `#text`, no tagName.
2. The `<p>` element -- nodeType 1, nodeName and tagName both `P` (uppercase in HTML documents).
3. A text node (whitespace between `</p>` and the comment).
4. The comment `<!-- a helpful comment -->` -- nodeType 8, nodeName `#comment`, no tagName.
5. A text node (whitespace after the comment and before `</div>`).

For the `<p>` element itself: `nodeName` and `tagName` both return `"P"`. Its `firstChild` is the text node `"Hello, "`, so `nodeName` is `"#text"` and `tagName` is `undefined` because text nodes do not have tag names.

## Snippet 2

**Output:**
```
innerHTML: Apple &amp; <em>Orange</em>
textContent: Apple & Orange
---
ul textContent: "\n    Apple & Orange\n    Banana\n  "
includes ampersand: true
includes &amp;: false
```

**Rationale:**
- `innerHTML` returns the raw HTML markup inside the element. The `&amp;` entity is preserved as `&amp;` in the HTML source, and the `<em>` tag is included as markup.
- `textContent` returns only the text content with all tags stripped and HTML entities decoded. So `&amp;` becomes a literal `&` character, and the `<em>` tags are removed, leaving just `"Apple & Orange"`.
- For the whole `<ul>`, `textContent` concatenates all descendant text nodes, including whitespace text nodes (the newlines and spaces from the HTML formatting).
- `firstLi.textContent.includes('&')` is `true` because the entity was decoded to a real ampersand.
- `firstLi.textContent.includes('&amp;')` is `false` because `textContent` contains the decoded `&`, not the raw entity string `&amp;`.

**Key concepts tested:**
- `nodeType` values: 1 = element, 3 = text, 8 = comment
- `tagName` is `undefined` for non-element nodes (only elements have tag names)
- `nodeName` works on all node types (`#text`, `#comment`, or the tag name for elements)
- Tag names are uppercase in HTML documents
- `childNodes` includes all nodes: text (including whitespace), elements, and comments
- `innerHTML` preserves HTML markup and entities in their raw form
- `textContent` strips tags and decodes HTML entities to their actual characters
- `textContent` on a parent concatenates all descendant text nodes including whitespace
