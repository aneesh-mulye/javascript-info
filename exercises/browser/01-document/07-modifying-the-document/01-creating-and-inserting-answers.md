# Step 1 Answer Key: createElement, append/prepend/before/after

## Snippet 1

**Output:**
```
E:DIV:Appended div | E:DIV:Prepended div | T:Text before existing. | E:P:I was here first. | T:Text after existing.
```

**Rationale:** Let's trace the DOM mutations step by step:

1. `container.append(div1)` -- div1 ("Appended div") goes to the end of container, after `<p>`.
2. `container.prepend(div2)` -- div2 ("Prepended div") goes to the beginning of container, before `<p>`.
3. `existing.before('Text before existing. ')` -- a text node is inserted as a sibling before `<p>`.
4. `existing.after(' Text after existing.')` -- a text node is inserted as a sibling after `<p>`.
5. `container.prepend(div1)` -- div1 is **moved** (not copied) from its current position at the end to the beginning. This removes it from the end.

After all mutations, container's child nodes in order are:
- div1 (element, "Appended div") -- moved to front
- div2 (element, "Prepended div") -- was previously first, now second
- text node "Text before existing. "
- `<p>` element "I was here first."
- text node " Text after existing."

The loop filters: elements produce `E:TAG:trimmedText`, non-empty text nodes produce `T:trimmedText`. The whitespace-only text nodes between elements in the original HTML are trimmed to empty and skipped.

## Snippet 2

**Output:**
```
text:(start of menu) | <li>Search | <li>Home | <li>About | <li>Contact | text:(end of menu) | text:<li>Fake item</li>
4
Search, About, Contact, Home
```

**Rationale:**

Starting state of `<ul id="menu">`: `<li>Home</li>`, `<li>About</li>`.

1. `menu.append(liContact, ' (end of menu)')` -- appends two things at the end: the `<li>Contact</li>` element, and a **text node** " (end of menu)".
2. `menu.prepend('(start of menu) ', liSearch)` -- prepends two things at the beginning: a text node "(start of menu) ", then `<li>Search</li>`.
3. `menu.append('<li>Fake item</li>')` -- this passes a **string** to append, which creates a **text node**, NOT a parsed `<li>` element. The literal text `<li>Fake item</li>` appears as a text node.

So the child nodes are: text "(start of menu) ", `<li>Search`, `<li>Home`, `<li>About`, `<li>Contact`, text "(end of menu)", text `<li>Fake item</li>`.

The loop prints them joined. Then:

4. `menu.append(itemHome)` -- **moves** the Home `<li>` from its current position to the end. It does not duplicate it.

After the move, `menu.children` (element children only, no text nodes) are: Search, About, Contact, Home. That is 4 `<li>` elements.

`liTexts.join(', ')` outputs `Search, About, Contact, Home`.

**Key concepts tested:**
- `append`/`prepend` accept multiple arguments, mixing nodes and strings
- Strings passed to `append`/`prepend` become **text nodes**, not parsed HTML
- Inserting an already-in-DOM node **moves** it (removes from old position)
- `children` returns only element children, not text nodes
