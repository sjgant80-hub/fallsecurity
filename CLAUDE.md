# Working on FallSecurity — agent instructions

FallSecurity ships as a single self-contained browser file, `index.html`. The security
logic — the eight per-turn vertex validators (`V0`–`V7`), the `sha256` audit helper, and
the `Ω` resolver that tracks coherence across turns — lives inline in that file so the demo
runs with zero build step and zero server.

## The rule that outranks the others

**The vertex/resolver logic in `index.html` is the product. Do not edit it to make a test
pass.** If a test disagrees with the code, the test is wrong until proven otherwise: fix the
test to match observed behaviour, or remove the assertion and write down why. A test that
was changed to match a guess, or code that was changed to match a test, both defeat the
point.

## How the code is verified

- [`test.mjs`](test.mjs) is the suite. It reads [`index.html`](index.html), slices out the
  `KAPPA … Omega` block verbatim, and loads it into Node with `new Function`, so the tests
  exercise the **real** functions rather than a reimplementation. Every assertion was derived
  by running the code and recording what it actually returned (byte counts, classifier
  labels, relevance scores, coherence values, SHA-256 prefixes), never from the prose spec.
- It also imports the committed module contract, [`module.manifest.json`](module.manifest.json),
  and checks that every declared tool is internally consistent (required parameters exist,
  enums are closed, `reversible_ms` is present).
- Run it with `npm test` (which is `node test.mjs`). CI runs the same command on every push.

## Rules

- **Zero runtime dependencies.** Vanilla Node ≥ 18 and the browser platform globals
  (`crypto.subtle`, `TextEncoder`, `Blob`) only. Do not add an npm dependency.
- **Determinism.** Every function under test is pure and clock-free. Keep it that way — an
  assertion must not depend on wall-clock time, locale, or ordering. `Date.now()` appears only
  in the export/download paths, which are not asserted on.
- **Keep the extraction anchors stable.** `test.mjs` locates the logic by the literal strings
  `const KAPPA = 0.618;` and `const FallCube = {`. If you rename those, update the anchors.
- **Leave it green.** End every change with `npm test` passing.

## Design reference

The architecture and the reasoning behind each vertex are documented in [`SPEC.md`](SPEC.md).
`README.md` is the human entry point; `llms.txt` and `ai.html` are the machine-readable
dossier. This file governs how the code is changed and checked, nothing more.
