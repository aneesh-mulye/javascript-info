# Step 3 Answer Key: nodeValue, hidden, Combined Properties

## Snippet 1

**Output:**
```
[0] nodeType=8, data=" config: theme=dark "
    nodeValue === data: true
    nodeName: #comment
[1] nodeType=3, data="Welcome to the"
    nodeValue === data: true
    nodeName: #text
[2] nodeType=8, data=" end config "
    nodeValue === data: true
    nodeName: #comment
---
b.nodeValue: null
b.data: undefined
b.firstChild.data: dashboard
```

**Rationale:**
The `info-box` div's `childNodes` include whitespace text nodes, two comments, the text `"Welcome to the "`, and the `<b>` element. The filter keeps comment nodes (nodeType 8) and non-whitespace-only text nodes (nodeType 3).

After filtering, we get three "interesting" nodes:
1. The first comment (`<!-- config: theme=dark -->`): nodeType 8, data is `" config: theme=dark "` (comments store their content with the surrounding spaces).
2. The text node `"Welcome to the "` between the comment and the `<b>` tag. After `.trim()`, it displays as `"Welcome to the"`.
3. The second comment (`<!-- end config -->`): nodeType 8, data `" end config "`.

Note: The text node between `</b>` and `<!-- end config -->` is whitespace-only, so it is filtered out.

For all text and comment nodes, `nodeValue === data` is `true` -- they are the same thing.

For the `<b>` element:
- `nodeValue` is `null` -- element nodes do not have a nodeValue.
- `data` is `undefined` -- the `data` property is not defined on element nodes (it is not `null`, it simply does not exist on the Element interface, so accessing it gives `undefined`).
- `firstChild.data` is `"dashboard"` -- the text node inside `<b>` has `data` equal to its text content.

## Snippet 2

**Output:**
```
Visible: ["Visible task 1", "Visible task 2"]
Hidden: ["Secret task", "Another secret"]
---
Before toggle - hidden: true
Before toggle - offsetHeight: 0
After toggle - hidden: false
After toggle - has dimensions: true
Re-hidden via property: true
getAttribute('hidden'): ""
```

**Rationale:**
The `<ul>` has four `<li>` elements. Two have the `hidden` attribute, two do not. The `hidden` DOM property is a boolean: `true` for elements with the `hidden` attribute, `false` for those without. The `reduce` correctly categorizes them.

For the toggle demo:
- The `<p id="message">` starts with `hidden` attribute, so `message.hidden` is `true`.
- `offsetHeight` is `0` for hidden elements (they have no layout).
- Setting `message.hidden = false` removes the hidden state, making it visible with non-zero dimensions.
- Setting `message.hidden = true` re-hides it.
- `getAttribute('hidden')` returns `""` (empty string). This is because when the `hidden` property is set to `true`, the browser adds the `hidden` attribute to the element. Boolean HTML attributes like `hidden` have an empty string as their attribute value when present (the attribute's mere presence means "true").

**Key concepts tested:**
- `nodeValue` and `data` are equivalent for text and comment nodes
- `nodeValue` is `null` for element nodes; `data` is `undefined` for element nodes
- Comment nodes store their content (including internal whitespace) in `data`/`nodeValue`
- The `hidden` property is a boolean; the `hidden` attribute is a string (empty string when present)
- Hidden elements have zero `offsetHeight`
- Setting the boolean `hidden` property to `true`/`false` properly syncs with the HTML attribute
- `getAttribute` on a boolean attribute returns `""` (not `"true"` or `"hidden"`)
