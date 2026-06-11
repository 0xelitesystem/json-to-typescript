# json-to-typescript

Paste any JSON value, get TypeScript interface declarations. Single HTML file. Browser-only.

**Live demo:** https://0xelitesystem.github.io/json-to-typescript/

## Why

You get a sample API response. You need types for it. You either spend 10 minutes writing them by hand and miss a nullable field, or you use a CLI tool, or you paste into one of three online tools that may be tracking your data. This is the smallest, fastest, no-network alternative.

## Use it

Open `index.html` in any browser, or visit the hosted demo at `https://0xelitesystem.github.io/json-to-typescript/` once Pages is enabled.

1. Paste JSON in the left panel.
2. Pick a root interface name and an export style.
3. Copy or download the generated TypeScript.

## What it handles

- **Nested objects**: each becomes its own interface, named after the property key (PascalCased)
- **Arrays of objects**: merged across all elements to detect optional fields and union types
- **Mixed arrays**: produce union types like `(string | number)[]`
- **Null values**: produce `| null` unions where present
- **Optional fields** (when input is an array of object samples and a key is missing from some): generate `field?: type`
- **Quoted property names** for keys that aren't valid TS identifiers
- **Nested array merging**: arrays of objects inside objects in arrays all merge correctly

## Export styles

| Style | Output |
|---|---|
| `export interface` | Default. `export interface Foo { ... }` |
| `declare interface` | Ambient declaration, useful for `.d.ts` files |
| `interface` (no export) | Plain interface, no export |
| `export type` | Type aliases instead of interfaces; necessary for some union-type roots |

## Tech

- Single HTML file, ~600 lines including the schema generator
- Vanilla JS, no frameworks, no dependencies, no build
- Light and dark themes with OS preference detection
- WCAG AA contrast on both themes
- Tested in current Chrome, Firefox, Safari

## What it doesn't do

- Doesn't infer enum types from string values. Use a stricter schema tool if you need that.
- Doesn't detect dates or other format-specific strings. They become plain `string`.
- Doesn't generate JSON Schema, Zod schemas, or runtime validators. Use dedicated tools.
- Doesn't preserve comments. JSON doesn't support them.
- Doesn't handle very large inputs (> 1MB) gracefully. The whole tree is processed in one pass.

## Tips

For the best output, paste an array of N representative samples instead of one. The merger detects optional fields when a key appears in some samples and not others.

## License

MIT. See [LICENSE](LICENSE).

## Related

- [csv-to-anything](https://github.com/0xelitesystem/csv-to-anything), convert CSV to JSON/SQL/Markdown/TS
- [regex-tester-with-explainer](https://github.com/0xelitesystem/regex-tester-with-explainer), test and explain regex
- [single-file-saas-template](https://github.com/0xelitesystem/single-file-saas-template), ship a SaaS in one HTML file
