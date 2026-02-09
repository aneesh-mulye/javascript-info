# Step 2 Answer Key: Sync and Types

## Snippet 1

**Output:**
```
property: initial
attribute: initial
After property change:
  property: changed-via-property
  attribute: initial
After attribute change:
  property: changed-via-property
  attribute: changed-via-attribute
---
Fresh input property: from-attr
Fresh input attribute: from-attr
After attr update - property: updated-attr
After property was set then attr updated:
  property: from-property
  attribute: attr-again
---
checked property: true
typeof checked property: boolean
getAttribute('checked'):
typeof getAttribute: string
After unchecking - property: false
After unchecking - attribute:
```

**Rationale:**

The `input.value` attribute/property sync is one of the most important gotchas. The key rules are:
1. The attribute acts as the "default value." As long as the property has never been explicitly set, changing the attribute syncs to the property.
2. Once the property is explicitly set (programmatically or by user input), the link from attribute to property is **broken permanently**. The attribute and property become independent.
3. The property **never** syncs back to the attribute, regardless.

**First input (`username`):**
- Initially, both are `"initial"` -- they start in sync.
- Setting the **property** (`username.value = 'changed-via-property'`) does NOT update the attribute. The attribute stays `"initial"`.
- After the property has been explicitly set, setting the **attribute** (`setAttribute('value', 'changed-via-attribute')`) only updates the attribute. The property remains `"changed-via-property"` because the sync link was broken when the property was explicitly set.

**Fresh input:**
- `setAttribute('value', 'from-attr')` sets both attribute and property (property hasn't been explicitly set yet, so attribute syncs to property).
- `setAttribute('value', 'updated-attr')` still syncs to the property because the property was never explicitly set -- the property becomes `"updated-attr"`.
- After `freshInput.value = 'from-property'`, the property is now "dirty" (explicitly set).
- `setAttribute('value', 'attr-again')` only changes the attribute; the property stays `'from-property'`.

**Checkbox:**
- The `checked` property is a **boolean** (`true`), while `getAttribute('checked')` returns `""` (empty string) -- boolean HTML attributes have empty string as their value when present.
- Setting `toggle.checked = false` unchecks it programmatically, but `getAttribute('checked')` still returns `""`. The `checked` attribute reflects the *default* checked state from the HTML source, not the current live state. Like `input.value`, the `checked` attribute does not sync with property changes.

## Snippet 2

**Output:**
```
relative getAttribute: /about
relative .href: http://<origin>/about
same? false
full getAttribute: https://example.com/page
full .href: https://example.com/page
same? true
---
getAttribute('style'): color: red; font-size: 14px;
typeof getAttribute('style'): string
.style: [object CSSStyleDeclaration]
typeof .style: object
.style.color: red
```

**Rationale:**
- For `href`: `getAttribute` returns the raw HTML attribute value. The `.href` DOM property returns the **full resolved URL**. For a relative URL like `/about`, these differ (the property includes the protocol and origin). For an already-absolute URL like `https://example.com/page`, they are the same string.
- For `style`: `getAttribute('style')` returns the raw string from the HTML attribute. The `.style` property returns a `CSSStyleDeclaration` object (typeof `"object"`), not a string. Individual CSS properties are accessed through this object (e.g., `.style.color` returns `"red"`).

Note: The exact string representation of the style object in `console.log` varies by browser. Most will show `[object CSSStyleDeclaration]` or expand the object's properties. The `typeof` is always `"object"`.

**Key concepts tested:**
- `input.value`: one-way sync from attribute to property, broken permanently once the property is explicitly set
- Property changes to `value` never sync back to the attribute
- `checked` attribute reflects the default/initial state, not the live state; it does not sync with property changes
- Boolean attributes: property is boolean, `getAttribute` returns a string (empty string)
- `href` property resolves to full URL; `getAttribute('href')` returns the raw value
- `style` property is a `CSSStyleDeclaration` object; `getAttribute('style')` is a string
- Fundamental type difference: attributes are always strings, properties are typed values
