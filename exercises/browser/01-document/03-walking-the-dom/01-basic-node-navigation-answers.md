# Step 1 Answer Key: Basic Node Navigation

## Snippet 1

**Output:**
```
2
SPAN
Beta
Beta
```

**Rationale:**

The `<div id="snippet1">` is written as `<div id="snippet1"><span>Alpha</span><span>Beta</span></div>` -- all on one line with no whitespace between the opening `<div>` tag and the first `<span>`, nor between the two `<span>` elements, nor between the last `<span>` and the closing `</div>`. Therefore there are no whitespace text nodes at all.

1. `s1.childNodes.length` is `2` -- the two `<span>` elements and nothing else.
2. `s1.firstChild.tagName` is `SPAN` -- `firstChild` is the first `<span>`. `tagName` on element nodes is always uppercase.
3. `s1.lastChild.textContent` is `Beta` -- `lastChild` is the second `<span>`, whose text content is "Beta".
4. `s1.firstChild.nextSibling.textContent` is `Beta` -- since there are no whitespace text nodes, `nextSibling` of the first `<span>` goes directly to the second `<span>`.

## Snippet 2

**Output:**
```
7
3
3
8
3
8
true
```

**Rationale:**

The `<div id="snippet2">` has its content on multiple lines with indentation. The DOM structure of its child nodes is:

- Index 0: Text node (`"\n    "` -- newline + spaces after `<div id="snippet2">`)
- Index 1: `<p>First</p>` element
- Index 2: Text node (`"\n    "` -- whitespace between `</p>` and `<!-- a comment -->`)
- Index 3: Comment node (`<!-- a comment -->`)
- Index 4: Text node (`"\n    "` -- whitespace between comment and second `<p>`)
- Index 5: `<p>Second</p>` element
- Index 6: Text node (`"\n  "` -- whitespace before `</div>`)

1. `s2.childNodes.length` is `7` -- all 7 nodes listed above.
2. `s2.firstChild.nodeType` is `3` -- index 0 is a text node (nodeType 3).
3. `s2.childNodes[2].nodeType` is `3` -- index 2 is a text node between the first `<p>` and the comment.
4. `s2.childNodes[3].nodeType` is `8` -- index 3 is the comment node (nodeType 8).
5. `s2.lastChild.nodeType` is `3` -- index 6 is the trailing whitespace text node.
6. `s2.childNodes[1].nextSibling.nextSibling.nodeType` is `8` -- `childNodes[1]` is the first `<p>`, `.nextSibling` is the text node at index 2, `.nextSibling` again is the comment node at index 3 (nodeType 8).
7. `s2.childNodes[3].parentNode === s2` is `true` -- the comment's parent is indeed the `<div>`.

**Key concepts tested:**
- Whitespace between tags creates text nodes in the DOM
- When tags are adjacent with no whitespace (Snippet 1), no text nodes are created
- `childNodes` includes ALL node types: elements, text nodes, and comments
- `nodeType` values: 1 = Element, 3 = Text, 8 = Comment
- `firstChild`, `lastChild`, `nextSibling` navigate ALL nodes, not just elements
- `parentNode` returns the parent of any node type
- `tagName` returns uppercase tag names for element nodes
