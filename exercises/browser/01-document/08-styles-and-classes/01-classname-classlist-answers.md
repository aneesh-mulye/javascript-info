# Step 1 Answer Key: className and classList

## Snippet 1

**Output:**
```
highlight bold
true
false
highlight bold active
highlight active
hidden
false
true
1
```

**Rationale:**

1. `box1.className` -- returns the full class attribute string: `highlight bold`.

2. `box1.classList.contains('highlight')` -- `true`, it is present.
3. `box1.classList.contains('active')` -- `false`, not present.

4. `box1.classList.add('active')` -- adds "active" without removing existing classes. `box1.className` is now `highlight bold active`.

5. `box1.classList.remove('bold')` -- removes only "bold". `box1.className` is now `highlight active`.

6. `box1.className = 'hidden'` -- setting `className` directly **replaces the entire class attribute**. All previous classes are gone.
   - `box1.className` is `hidden`.
   - `classList.contains('highlight')` is `false` (wiped out).
   - `classList.contains('hidden')` is `true`.
   - `classList.length` is `1`.

## Snippet 2

**Output:**
```
active
false

true
true
active highlight
4
active bold
```

**Rationale:**

1. `box2.className` -- initially `active`.

2. `box2.classList.toggle('active')` -- "active" is present, so it is **removed**. Returns `false` (class was removed). `box2.className` is now `` (empty string).

3. `box2.classList.toggle('active')` -- "active" is absent, so it is **added**. Returns `true` (class was added).

4. `box2.classList.toggle('highlight')` -- "highlight" is absent, so it is **added**. Returns `true`. `box2.className` is now `active highlight`.

5. `box2.classList.add('bold', 'hidden')` -- adds both. classList now has: active, highlight, bold, hidden. `classList.length` is `4`.

6. `box2.classList.remove('highlight', 'hidden')` -- removes both. Remaining classes: active, bold.

7. `Array.from(box2.classList).sort().join(' ')` -- sorted alphabetically: `active bold`.

**Key concepts tested:**
- `className` is the full class string; setting it **replaces** all classes
- `classList.add`/`remove` are additive/subtractive and accept multiple arguments
- `classList.toggle` adds if absent (returns `true`), removes if present (returns `false`)
- `classList.contains` checks for a single class
- `classList.length` gives the count of classes
- `classList` and `className` reflect each other -- they are two views of the same attribute
