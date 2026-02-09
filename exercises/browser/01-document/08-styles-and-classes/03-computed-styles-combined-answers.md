# Step 3 Answer Key: getComputedStyle and combining styles with classes

## Snippet 1

**Output:**
```
(empty string)
(empty string)
(empty string)
rgb(0, 0, 139)
18px
300px
rgb(220, 20, 60)
rgb(0, 128, 0)
rgb(220, 20, 60)
```

Note: The first three lines are empty strings. The color values are returned in `rgb()` format because `getComputedStyle` returns **resolved** values.

**Rationale:**

1. `elem1.style.color`, `.fontSize`, `.width` -- all return `""` because elem1 has **no inline styles**. The `style` property only reads inline styles.

2. `getComputedStyle(elem1)` reads the **actually applied** styles:
   - `.color` returns `rgb(0, 0, 139)` -- this is `darkblue` resolved to RGB.
   - `.fontSize` returns `18px`.
   - `.width` returns `300px`.

3. After `elem1.classList.add('override-color')`: The `.override-color` class sets `color: crimson`. Since class selectors have lower specificity than ID selectors... however, `.override-color` is declared **after** the `#elem1` rule in the stylesheet, and both have the same property. Actually, `#elem1` has higher specificity than `.override-color`. But wait -- the element now matches both `#elem1 { color: darkblue }` and `.override-color { color: crimson }`. The ID selector has higher specificity, so `darkblue` should win.

   Actually, let me reconsider. The specificity of `#elem1` (0,1,0,0) is higher than `.override-color` (0,0,1,0). So `darkblue` should still apply. But the snippet comment says "overrides color" and later "The 'override-color' class is still applied, so color is crimson". Let me re-examine...

   The CSS specificity rules: ID selectors (specificity 0,1,0,0) beat class selectors (0,0,1,0). So `#elem1 { color: darkblue }` should beat `.override-color { color: crimson }`.

   However, reading the snippet more carefully and the comment on line 74: "The 'override-color' class is still applied, so color is crimson (not the original darkblue from #elem1 CSS)". The snippet author intended for the class to override. This would only work if `!important` were used or specificity were different. Given standard CSS specificity, the ID selector wins.

   **Corrected output for line 63 (`comp1b.color`):** `rgb(0, 0, 139)` (darkblue still wins due to higher ID specificity).

   But this creates a contradiction with the snippet's own comments. The snippet comment on line 74 explicitly states the color should be crimson after removing inline style. This suggests the author may have intended `.override-color` to have higher specificity, or there may be an error in the exercise. Given standard CSS rules, the ID selector `#elem1` has higher specificity than the class `.override-color`, so `darkblue` wins.

   **However**, if we take the code at face value and apply CSS rules correctly:
   - `comp1b.color` = `rgb(0, 0, 139)` (darkblue -- ID wins over class)
   - After `elem1.style.color = 'green'`: `comp1c.color` = `rgb(0, 128, 0)` (inline styles beat everything except `!important`)
   - After `elem1.style.color = ''`: `comp1d.color` = `rgb(0, 0, 139)` (falls back to CSS cascade, where ID still beats class)

**Corrected Output:**
```
(empty string)
(empty string)
(empty string)
rgb(0, 0, 139)
18px
300px
rgb(0, 0, 139)
rgb(0, 128, 0)
rgb(0, 0, 139)
```

**Note:** The snippet's comments on lines 61 and 73-74 are misleading. They suggest the class overrides the ID-selector style, but standard CSS specificity means the `#elem1` rule (ID, specificity 0,1,0,0) beats `.override-color` (class, specificity 0,0,1,0). The color remains `darkblue` / `rgb(0, 0, 139)` throughout (except when an inline style is set). If the exercise author intended crimson to win, the CSS would need `.override-color` to use `!important` or have a more specific selector like `#elem1.override-color`.

## Snippet 2

**Output:**
```
200px
32px
700
rgb(128, 128, 128)
32px
```

**Rationale:**

1. `comp2.width`: elem2 has `width: 50%` and `box-sizing: border-box`. The parent is `400px` wide. 50% of 400px = 200px. With `border-box`, the 200px includes padding (10px each side = 20px) and border (3px each side = 6px). `getComputedStyle().width` with `border-box` reports `200px` in modern browsers (the border-box width, since that is the specified box model).

2. `comp2.fontSize`: elem2 has `font-size: 2em`. The parent has `font-size: 16px` (inline). 2em * 16px = `32px`. `getComputedStyle` resolves relative units to absolute `px` values.

3. `pseudoStyle.fontWeight`: The `::before` pseudo-element has `font-weight: bold`. `getComputedStyle` resolves `bold` to its numeric equivalent: `700`.

4. `pseudoStyle.color`: The `::before` pseudo-element has `color: gray`. Resolved to RGB: `rgb(128, 128, 128)`.

5. Attempting to set `comp2.fontSize = '10px'` on the computed style object either throws a `DOMException` (caught by the try/catch) or is silently ignored. Either way, the actual style is unchanged. `getComputedStyle(elem2).fontSize` is still `32px`.

**Key concepts tested:**
- `element.style` reads ONLY inline styles; `getComputedStyle` reads the actual applied/resolved styles
- `getComputedStyle` returns **resolved values** -- relative units (%, em) are converted to px, named colors to `rgb()`
- `getComputedStyle` can read pseudo-element styles via the second argument (`'::before'`)
- `getComputedStyle` is read-only -- attempting to set values does nothing (or throws)
- Inline styles take precedence over stylesheet styles (unless `!important` is used)
- CSS specificity: ID selectors beat class selectors
- `font-weight: bold` resolves to `700` in computed styles
- `box-sizing: border-box` affects how `width` is interpreted
