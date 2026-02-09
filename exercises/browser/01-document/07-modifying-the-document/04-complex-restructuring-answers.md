# Step 4 Answer Key: Complex DOM restructuring

## Snippet 1

**Output:**
```
box-a children: Four
box-b children: One (clone), One, Two, Three
true
```

**Rationale:** Let's trace each operation on box-a and box-b:

Initial state:
- box-a: item-1("One"), item-2("Two"), item-3("Three")
- box-b: (empty)

1. `boxB.append(item2)` -- **moves** item-2 from box-a to box-b.
   - box-a: item-1, item-3
   - box-b: item-2

2. `boxB.prepend(item1Clone)` -- item1Clone is a clone with text "One (clone)", prepended to box-b.
   - box-a: item-1, item-3
   - box-b: item1Clone, item-2

3. `item3.replaceWith(item4)` -- replaces item-3 in box-a with item-4("Four"). item-3 is detached but still referenced.
   - box-a: item-1, item-4
   - box-b: item1Clone, item-2

4. `boxB.append(item3)` -- appends the detached item-3("Three") to box-b.
   - box-a: item-1, item-4
   - box-b: item1Clone, item-2, item-3

5. `item1Clone.after(item1)` -- **moves** the original item-1 from box-a to box-b, inserted right after item1Clone.
   - box-a: item-4
   - box-b: item1Clone, item-1, item-2, item-3

Final:
- box-a children: `Four`
- box-b children: `One (clone), One, Two, Three`
- `boxA.children.length === 1 && boxA.firstElementChild.id === 'item-4'` is **true**.

## Snippet 2

**Output:**
```
0
3
High: Fix crash | High: Patch security | Medium: Add tests | Low: Write docs | Low: Refactor utils
```

**Rationale:**

1. All 5 `<li>` elements are grabbed from `#unsorted` via `querySelectorAll` and stored in an array. They are sorted by `data-priority` ascending (1, 1, 2, 3, 3).

2. For each sorted `<li>`, the code creates group divs (one per priority level) and **moves** (via `append`) the original `<li>` nodes from `#unsorted` into the group's `<ul>`. Since these are the same DOM nodes being appended elsewhere, they are **removed** from `#unsorted`.

3. After all moves, `unsorted.querySelectorAll('li').length` is **0** -- all `<li>` nodes were moved out.

4. Three priority groups were created (priority 1, 2, and 3), so `sortedOutput.querySelectorAll('.priority-group').length` is **3**.

5. The `<li>` elements in sorted-output, in priority order:
   - Priority 1: "High: Fix crash", "High: Patch security"
   - Priority 2: "Medium: Add tests"
   - Priority 3: "Low: Write docs", "Low: Refactor utils"

   Joined: `High: Fix crash | High: Patch security | Medium: Add tests | Low: Write docs | Low: Refactor utils`

**Key concepts tested:**
- A DOM node can only exist in one place -- inserting it elsewhere **moves** it automatically
- `replaceWith` detaches the replaced node, but it remains referenceable and can be re-inserted
- `cloneNode` creates an independent copy; the original remains where it was
- Combining `before`/`after` with nodes in different containers causes cross-container moves
- `DocumentFragment` for batch insertion
- Using `Array.from` + `sort` on NodeLists for DOM restructuring
- Stable sort preserving insertion order within same-priority groups
