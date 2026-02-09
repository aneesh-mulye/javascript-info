# Step 2 Answer Key: Inline styles, style property, cssText

## Snippet 1

**Output:**
```
(empty string)
(empty string)
(empty string)
salmon
24px
(empty string)
(empty string)
```

Note: The three initial `console.log` calls and the last two each print an empty string `""`. In the actual console, these appear as blank lines.

**Rationale:**

1. `panel1.style.backgroundColor`, `.fontSize`, `.padding` -- all return **empty string** `""`. The `style` property only reads **inline** styles (from the `style` attribute on the HTML element). Panel1 has its styles set via a `<style>` block (CSS stylesheet), not inline, so `style.*` returns `""` for all of them.

2. After setting `panel1.style.backgroundColor = 'salmon'` and `panel1.style.fontSize = '24px'`:
   - `panel1.style.backgroundColor` returns `salmon`
   - `panel1.style.fontSize` returns `24px`

3. `panel1.style.padding` still returns `""` -- we never set padding as an inline style; it is only in the stylesheet.

4. `panel1.style.backgroundColor = ''` -- setting to empty string **removes** that inline style. It returns `""`, and the element falls back to the CSS stylesheet value of `lightgray` (though `style.backgroundColor` still reports `""`).

## Snippet 2

**Output:**
```
bold
center

red
(empty string)
(empty string)
(empty string)
5px
0.8
```

**Rationale:**

1. `panel2.style.fontWeight` returns `bold` and `panel2.style.textAlign` returns `center` -- these are set as **inline** styles in the HTML: `style="font-weight: bold; text-align: center;"`.

2. `panel2.style.color` returns `""` -- color is set in the stylesheet (`color: navy`), not inline.

3. After `panel2.style.color = 'red'`, `panel2.style.color` returns `red`.

4. `panel2.style.cssText = 'margin-top: 5px; opacity: 0.8;'` -- this **completely overwrites** the entire inline `style` attribute. All previous inline styles (fontWeight, textAlign, color) are **gone**.

5. After cssText overwrite:
   - `panel2.style.fontWeight` returns `""` (gone)
   - `panel2.style.textAlign` returns `""` (gone)
   - `panel2.style.color` returns `""` (gone)
   - `panel2.style.marginTop` returns `5px`
   - `panel2.style.opacity` returns `0.8`

**Key concepts tested:**
- `element.style` reads/writes **only inline styles**, never stylesheet styles
- Multi-word CSS properties use camelCase in JS (`backgroundColor`, `fontSize`, `fontWeight`, `textAlign`, `marginTop`)
- Setting a style property to `""` removes that inline style
- `style.cssText` overwrites the **entire** inline style attribute -- all previous inline styles are lost
- Stylesheet styles remain applied but are invisible to `element.style`
