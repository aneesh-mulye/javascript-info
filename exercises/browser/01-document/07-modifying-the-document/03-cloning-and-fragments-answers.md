# Step 3 Answer Key: cloneNode and DocumentFragment

## Snippet 1

**Output:**
```
1
true
Hello world
0

Hello world
```

**Rationale:**

The original `<div id="original">` contains `<p id="inner-p">Hello <strong>world</strong></p>`.

1. `deepClone = original.cloneNode(true)` -- deep clone copies the element **and all descendants**. So `deepClone` is a `<div>` containing the `<p>` which contains text "Hello " and `<strong>world</strong>`.

2. `shallowClone = original.cloneNode(false)` -- shallow clone copies **only the element itself**, with no children at all. So `shallowClone` is an empty `<div>`.

After appending both to target1:

- `deepClone.children.length` is **1** (the cloned `<p>`).
- `deepClone.querySelector('strong') !== null` is **true** (the `<strong>` was deep-cloned).
- `deepClone.textContent.trim()` is **`Hello world`** (the text content of the `<p>` and `<strong>` combined).

- `shallowClone.children.length` is **0** (no children).
- `shallowClone.textContent` is **``** (empty string, since no children means no text content).

- Modifying the deep clone's `<p>` textContent to "Modified!" does NOT affect the original, because clones are independent copies. `original.querySelector('p').textContent.trim()` is still **`Hello world`**.

## Snippet 2

**Output:**
```
3
0
Item X, Item Y, Alpha, Beta, Gamma
2
```

**Rationale:**

1. A `DocumentFragment` is created and three `<li>` elements (Alpha, Beta, Gamma) are appended to it. `fragment.childNodes.length` is **3**.

2. `baseList` is deep-cloned (preserving its two `<li>` children: Item X, Item Y). The fragment is then appended to the clone.

3. When a DocumentFragment is appended, the fragment **dissolves** -- only its children are inserted, not the fragment itself. After this, `fragment.childNodes.length` is **0** because its children have been moved into the cloned list.

4. The cloned list now has 5 `<li>` children: Item X, Item Y, Alpha, Beta, Gamma. `allItems.join(', ')` outputs **`Item X, Item Y, Alpha, Beta, Gamma`**.

5. `baseList.children.length` is **2** -- the original list is unchanged because we cloned it (deep clone creates independent copies), and the fragment's `<li>` elements were newly created, not taken from `baseList`.

**Key concepts tested:**
- `cloneNode(true)` (deep) copies element and all descendants; `cloneNode(false)` (shallow) copies only the element itself
- Clones are fully independent -- mutations to one do not affect the other
- `DocumentFragment` acts as a temporary container that "dissolves" on insertion -- only its children are moved into the target
- After insertion, the fragment becomes empty (its children have been moved)
- Deep cloning does not link the clone to the original in any way
