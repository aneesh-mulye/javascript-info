# Step 2 Answer Key: innerHTML, textContent, outerHTML

## Snippet 1

**Output:**
```
Before: <p id="target">Original paragraph</p>
target.outerHTML: <p id="target">Original paragraph</p>
target.tagName: P
target.textContent: Original paragraph
wrapper.innerHTML: <h3 id="replacement">I replaced the paragraph</h3>
getElementById('target'): null
replacement.tagName: H3
```

**Rationale:** This demonstrates the crucial `outerHTML` assignment gotcha. When you assign to `target.outerHTML`:
1. The DOM is updated: the `<p>` element is removed from the document and replaced with the new `<h3>` element.
2. But the JavaScript variable `target` still references the old, now-detached `<p>` element. It is not updated to point to the replacement.

So after the assignment:
- `target.outerHTML`, `target.tagName`, and `target.textContent` all reflect the **old** `<p>` element (which still exists in memory, just not in the DOM).
- `wrapper.innerHTML` shows the **new** `<h3>` that is actually in the DOM.
- `getElementById('target')` returns `null` because the `<p id="target">` is no longer in the document.
- `getElementById('replacement')` finds the new `<h3>` element.

## Snippet 2

**Output:**
```
htmlSet.childNodes.length: 1
htmlSet.firstChild.tagName: IMG
textSet.childNodes.length: 1
textSet.firstChild.nodeType: 3
textSet.innerHTML: &lt;img src=x onerror="alert('XSS')"&gt;
---
originalTextNode.data: Start
appended.textContent: Start - Middle - End
originalTextNode.data: Start
originalTextNode === appended.firstChild: false
originalTextNode.parentNode: null
```

**Rationale:**

Part A: `innerHTML` vs `textContent` for setting content.
- Setting `innerHTML` parses the string as HTML. The `<img>` tag becomes an actual `IMG` element node, so `childNodes.length` is 1 and `firstChild.tagName` is `"IMG"`. (This is the XSS risk with innerHTML.)
- Setting `textContent` inserts the string as literal text. The `<img ...>` string becomes a text node (nodeType 3), and when you read back `innerHTML`, the angle brackets are escaped to `&lt;` and `&gt;`.

Part B: `innerHTML +=` destroys and recreates all content.
- `innerHTML +=` is equivalent to `element.innerHTML = element.innerHTML + newStuff`. This means the entire content is serialized to a string, the string is concatenated, and then the whole thing is re-parsed. All existing DOM nodes inside the element are destroyed and new ones are created.
- The `originalTextNode` stored before the `+=` operations still holds its data (`"Start"`) but is now detached from the DOM.
- `originalTextNode === appended.firstChild` is `false` because `firstChild` is a brand new text node.
- `originalTextNode.parentNode` is `null` because the original node was removed from the document.

**Key concepts tested:**
- The `outerHTML` assignment gotcha: the variable keeps the old reference, the DOM gets the new element
- `innerHTML` parses HTML markup; `textContent` escapes it as literal text
- Security implication: `textContent` is safe for user input, `innerHTML` is not
- `innerHTML +=` completely destroys and rebuilds inner content, breaking existing node references
- Detached nodes retain their data but have `null` parentNode
