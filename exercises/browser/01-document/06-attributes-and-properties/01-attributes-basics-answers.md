# Step 1 Answer Key: Attributes Basics

## Snippet 1

**Output:**
```
hero.id: hero
hero.className: main-panel
hero.tabIndex: 0
hero['data-role']: undefined
hero['custom-flag']: undefined
hero.customFlag: undefined
getAttribute('data-role'): admin
getAttribute('custom-flag'): yes
---
type property: email
value property: user@example.com
required property: true
typeof required: boolean
nonstandard-attr property: undefined
getAttribute nonstandard: test123
```

**Rationale:**
Standard HTML attributes are automatically mirrored as DOM properties. For the `<div>`:
- `id`, `className` (corresponding to the `class` attribute), and `tabIndex` (corresponding to `tabindex`) are all standard attributes for HTML elements, so they exist as properties.
- `data-role` and `custom-flag` are non-standard attributes for a `<div>`. They do NOT become DOM properties. Accessing them via bracket notation (`hero['data-role']`) or dot notation returns `undefined`.
- However, `getAttribute()` can access any attribute, standard or not.

For the `<input>`:
- `type`, `value`, and `required` are standard input attributes and become properties.
- The `required` property is a **boolean** (`true`), not a string -- the browser converts boolean HTML attributes to proper boolean property values.
- `nonstandard-attr` is not a standard attribute for `<input>`, so it is not available as a property but is accessible via `getAttribute`.

## Snippet 2

**Output:**
```
hasAttribute('href'): true
hasAttribute('rel'): false
getAttribute('href'): /about
link.href: http://<origin>/about
same? false
---
After setAttribute - hasAttribute('rel'): true
After setAttribute - getAttribute('rel'): noopener
data-tracking property: undefined
data-tracking getAttribute: nav-about
---
attributes.length: 6
attribute names: ["id", "href", "title", "target", "rel", "data-tracking"]
first attr value: nav-link
```

**Rationale:**
- `hasAttribute` checks whether an attribute exists in the HTML. The `<a>` has `href` but not `rel` initially.
- `getAttribute('href')` returns the raw attribute value as written in HTML: `"/about"`. The `link.href` DOM property returns the **full resolved URL** (e.g., `http://localhost/about` or whatever the page origin is). So they are not equal for relative URLs.
- `setAttribute` adds or modifies an attribute. After setting `rel`, `hasAttribute` returns `true` and `getAttribute` returns the value.
- Non-standard attributes set via `setAttribute` (like `data-tracking`) still do NOT become DOM properties -- `link['data-tracking']` is `undefined` -- but they are accessible via `getAttribute`.
- The `attributes` collection is a `NamedNodeMap` containing all attributes. After adding `rel` and `data-tracking`, the link has 6 attributes total: `id`, `href`, `title`, `target`, `rel`, `data-tracking` (in document order, with dynamically added ones at the end).
- `attrs[0].value` is `"nav-link"` (the value of the `id` attribute, which is first).

Note: The exact value of `link.href` depends on the page's origin. It will be the full URL with the origin prepended to `/about`. The key point is that it differs from the raw attribute value `"/about"`.

**Key concepts tested:**
- Standard HTML attributes become DOM properties; non-standard ones do not
- `className` maps to the `class` attribute (since `class` is a reserved word)
- Boolean attributes like `required` become boolean properties, not strings
- `getAttribute` returns the raw string value as written in HTML
- The `href` property returns the full resolved URL; `getAttribute('href')` returns the raw value
- `setAttribute` adds/modifies attributes but non-standard attributes still do not become properties
- The `attributes` collection (`NamedNodeMap`) is ordered and iterable
