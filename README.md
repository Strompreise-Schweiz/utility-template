# Example: power utility repository

Copy this repository for a utility that gets its own repo: one with day prices (dynamic tariffs), or
one that maintains its data itself. Utilities without day prices go into the hub repo
[`strompreise-schweiz.github.io`](https://github.com/Strompreise-Schweiz/strompreise-schweiz.github.io)
instead. The utility in this template is fictional.

After creating the repo, enable Settings > Pages > Source "GitHub Actions" and add the repo to
`repositories.json` in the hub repo. The data is then served at
`https://data.strompreise-schweiz.ch/<repo>/`.

Then replace this paragraph and the ones above with a short description of the utility, and add the
badges that show whether its yearly file follows the [OpenAPI definitions of the VSE](https://github.com/Strompreise-Schweiz/tariff-core/tree/main/schemas/vse). Replace
`<repo>` with the repo name:

```markdown
[![VSE 1.0.0](https://img.shields.io/endpoint?url=https%3A%2F%2Fdata.strompreise-schweiz.ch%2F<repo>%2Fbadges%2Fvse-1.0.0.json)](data/checks.json)
[![VSE 1.0.1](https://img.shields.io/endpoint?url=https%3A%2F%2Fdata.strompreise-schweiz.ch%2F<repo>%2Fbadges%2Fvse-1.0.1.json)](data/checks.json)
```

## Three tariff forms

| `tariffForm` | Meaning | Example here |
|---|---|---|
| `constant` | One price at all times | Sample Energy Single Rate |
| `multilevel` | Prices by month, weekday or time | Sample Energy Dual Rate |
| `dynamic` | Prices published each day for the next day | Sample Grid Dynamic |

All three are in the yearly file. The prices of a dynamic tariff come from an API of the utility, one
entry under `prices` in `config/source.json`.

## Where what is

| Question | Place | Changed by |
|---|---|---|
| Where does the data come from? | `config/source.json` | a person |
| What does a person change? | `curation/<year>.json`, each change with a reason | a person |
| What is wrong with it? | `data/checks.json` | GitHub Actions |
| What is published? | `data/`: `sources/` as the utility sent it, the rest built from it | GitHub Actions |

`curation/<year>.source.json` is a hand-written yearly file, only for a utility without usable JSON.

## What a new organization needs

1. Create the repo from this template and adapt `config/source.json`.
2. Enter the `url` of the yearly file under `tariffs`. If the utility has no usable JSON, write the
   file by hand as `curation/<year>.source.json` and enter it as `file`.
3. For dynamic tariffs, add an entry under `prices` with exactly the `prices.dynamic.url` of the
   yearly file, and start "Update prices" by hand once.
4. Propose products with `suggest-products.ts`, check them against the price sheet, and copy them
   to `curation/<year>.json`. A product with a dynamic tariff gets one file per day in `data/products/`.

See [`adding-organization.md`](https://github.com/Strompreise-Schweiz/tariff-core/blob/main/docs/adding-organization.md).

## Workflows

| Workflow | When | What |
|---|---|---|
| Update prices | Three times each evening | Download the day prices, build |
| Update tariffs | Weekly, and on a change to `curation/` or `config/` | Download the yearly file, build |
| Validate | On push | Check everything |
| Deploy site | After each update | Publish `data/` under `data.strompreise-schweiz.ch/<repo>/` |
