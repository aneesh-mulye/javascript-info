# Step 3 Answer Key: Dataset and Complex Attribute Manipulation

## Snippet 1

**Output:**
```
dataset.userId: 42
dataset.role: editor
dataset.lastLoginDate: 2025-01-15
dataset.isActive: true
typeof dataset.isActive: string
---
getAttribute('data-user-id'): 42
getAttribute('data-last-login-date'): 2025-01-15
dataset keys: ["userId", "role", "lastLoginDate", "isActive"]
---
After dataset.theme = 'dark':
  dataset.theme: dark
  getAttribute('data-theme'): dark
  hasAttribute('data-theme'): true
dataset.signUpSource: organic
getAttribute('data-sign-up-source'): organic
```

**Rationale:**
The `dataset` property provides access to all `data-*` attributes with automatic camelCase conversion:
- `data-user-id` becomes `dataset.userId`
- `data-role` becomes `dataset.role` (single word, no conversion needed)
- `data-last-login-date` becomes `dataset.lastLoginDate`
- `data-is-active` becomes `dataset.isActive`

Crucially, `typeof dataset.isActive` is `"string"`, not `"boolean"`. All `data-*` attribute values are strings, even if they look like `"true"` or numbers. The `dataset` API does not perform type conversion.

`getAttribute` returns the same string values using the original hyphenated names.

`Object.keys(card.dataset)` returns the camelCased versions of all `data-*` attribute names (without the `data-` prefix).

Setting via `dataset` syncs to the actual HTML attribute:
- `dataset.theme = 'dark'` creates a `data-theme` attribute on the element.
- `dataset.signUpSource = 'organic'` creates a `data-sign-up-source` attribute. The camelCase-to-hyphenated conversion works in reverse: each uppercase letter becomes a hyphen plus the lowercase letter.

## Snippet 2

**Output:**
```
High priority: [{"text":"Fix login crash","category":"bug","blocked":false},{"text":"SSO integration","category":"feature","blocked":true}]
---
By category: {"bug":["Fix login crash","Fix typo in footer"],"feature":["Add dark mode","SSO integration"]}
Before remove - dataset.priority: high
After remove - dataset.priority: undefined
After remove - 'priority' in dataset: false
Before delete - dataset.category: bug
After delete - getAttribute('data-category'): null
```

**Rationale:**
The filtering and mapping uses `dataset.priority` and `dataset.category` to access data attributes. `hasAttribute('data-blocked-by')` checks for the presence of the blocking attribute (only the third `<li>` has it).

The `reduce` groups all items by their `data-category`, producing an object with `"bug"` and `"feature"` keys.

For the removal tests:
- `removeAttribute('data-priority')` removes the HTML attribute, which is immediately reflected in `dataset` -- `dataset.priority` becomes `undefined` and `'priority' in dataset` is `false`. This confirms that `dataset` and actual HTML attributes are fully synchronized.
- `delete firstItem.dataset.category` removes the entry from `dataset`, which also removes the corresponding `data-category` HTML attribute. `getAttribute('data-category')` returns `null` (the standard return value when an attribute does not exist).

**Key concepts tested:**
- `dataset` provides camelCase access to `data-*` attributes (hyphen-separated names become camelCase)
- All `dataset` values are strings -- no automatic type conversion
- The camelCase conversion is bidirectional: setting `dataset.signUpSource` creates `data-sign-up-source`
- `dataset` and HTML attributes are fully synchronized in both directions
- `removeAttribute` on a `data-*` attribute removes it from `dataset`
- `delete dataset.key` removes the corresponding `data-*` HTML attribute
- `getAttribute` returns `null` for non-existent attributes
- Combining `dataset` with array methods (`filter`, `map`, `reduce`) for DOM data processing
