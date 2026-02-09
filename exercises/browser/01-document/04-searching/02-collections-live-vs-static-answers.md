# Step 2 Answer Key: Live vs Static Collections

## Snippet 1

**Output:**
```
2
2
3
2
2
2
```

**Rationale:**

Initial state: `<div id="snippet1">` contains two `<p class="note">` elements.

1. `liveNotes.length` is `2` -- `getElementsByClassName("note")` returns a live HTMLCollection. Initially 2 elements.

2. `staticNotes.length` is `2` -- `querySelectorAll(".note")` returns a static NodeList snapshot. Initially 2 elements.

3. After appending a new `<p class="note">Gamma</p>`:
   - `liveNotes.length` is `3` -- the live collection automatically reflects the DOM change.

4. `staticNotes.length` is `2` -- the static NodeList is a snapshot from when `querySelectorAll` was called. It does not update.

5. After removing the first `.note` element (Alpha):
   - `liveNotes.length` is `2` -- the live collection updates again: Beta and Gamma remain.

6. `staticNotes.length` is `2` -- still the original snapshot (Alpha and Beta references, though Alpha is now detached from the DOM).

## Snippet 2

**Output:**
```
3
3
3
3
5
3
Four
undefined
```

**Rationale:**

Initial state: `<ul id="snippet2">` contains 3 `<li>` elements.

1. `liveArr.length` is `3` -- `Array.from(liveLis)` creates a regular array from the live collection at this moment. Arrays are plain data; they do not update when the DOM changes.

2. `staticArr.length` is `3` -- the spread operator `[...staticLis]` creates a regular array from the static NodeList. Also a snapshot.

3. After `insertAdjacentHTML("beforeend", "<li>Four</li><li>Five</li>")`, two more `<li>` elements are added. Now the DOM has 5 `<li>` elements.

4. `liveArr.length` is `3` -- the plain array was created before the insertion and does not update.

5. `staticArr.length` is `3` -- same: a plain array created before the insertion.

6. `liveLis.length` is `5` -- the **live HTMLCollection** automatically reflects the DOM change.

7. `staticLis.length` is `3` -- the **static NodeList** was a snapshot and does not update.

8. `liveLis[3].textContent` is `Four` -- the live collection now has 5 items; index 3 is the fourth `<li>` ("Four").

9. `staticLis[3]` is `undefined` -- the static NodeList only has 3 items (indices 0-2), so index 3 is out of bounds.

**Key concepts tested:**
- `getElementsByClassName` and `getElementsByTagName` return **live** HTMLCollections that auto-update with DOM changes
- `querySelectorAll` returns a **static** NodeList that is a snapshot at call time
- Converting a live collection to an array (via `Array.from` or spread) creates a plain array that does NOT update -- the "liveness" is lost
- Accessing an out-of-bounds index on a NodeList returns `undefined` (not an error)
- `insertAdjacentHTML` as a way to add elements to the DOM
- The practical importance of understanding live vs static: if you cache a collection reference and the DOM changes, live collections reflect changes but static ones do not
