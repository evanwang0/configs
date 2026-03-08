# ESLint Config Philosophy

## Catch Bugs, Not Opinions

Nearly every "Possible Problems" rule is an error — the config is strict about **correctness** (unreachable code, unsafe operations, misused promises). But it deliberately leaves subjective style choices off: `no-nested-ternary`, `no-continue`, `no-plusplus`, `no-param-reassign`, `complexity`, `max-lines`, and all artificial limit rules are disabled. The config trusts the developer's judgment on structure.

## Maximize Type Safety

The TypeScript layer is aggressive about closing escape hatches:

- All `no-unsafe-*` rules are errors
- `no-explicit-any`, `no-non-null-assertion`, `strict-boolean-expressions` are enforced
- `switch-exhaustiveness-check` and `use-unknown-in-catch-callback-variable` push for exhaustive handling
- `type` is preferred over `interface` (`consistent-type-definitions`)

## Embrace Modern Idioms

The config consistently pushes toward modern JS/TS patterns: `prefer-const`, `prefer-template`, `prefer-destructuring`, `prefer-arrow-callback`, `prefer-nullish-coalescing`, `prefer-optional-chain`, `prefer-find`, `no-var`, `object-shorthand`. Legacy patterns are actively discouraged.

## Disciplined Imports and Types

Type imports are treated as first-class:

- `consistent-type-imports` with inline style
- `consistent-type-exports`
- `import/no-duplicates` and `import/consistent-type-specifier-style` at top-level
- `no-import-type-side-effects`

## Opinionated Formatting

Formatting is fully codified via `@stylistic` rather than left to debate:

- 2-space indentation, double quotes, semicolons
- Stroustrup brace style, trailing commas on multiline
- LF line endings, no tabs, no trailing spaces
- Object/array newlines enforced consistently

## Pragmatic, Not Dogmatic

Several common "strict" rules are intentionally off: `no-console`, `no-empty-function`, `no-magic-numbers`, `require-await`, `explicit-function-return-type`. The config leans on TypeScript's inference where it's reliable and avoids rules that create busywork without preventing real mistakes.

## Proper Rule Delegation

When a base ESLint rule has a TypeScript-aware equivalent, the base rule is disabled and the `@typescript-eslint` version takes over (e.g., `no-unused-vars`, `no-redeclare`, `no-loop-func`). Similarly, `@stylistic/js` rules are turned off in favor of `@stylistic/ts` equivalents for TypeScript files.
