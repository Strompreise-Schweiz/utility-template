# Example: power utility repository

Copy this repository for a utility that gets its own repo: one with dynamic tariffs, or one that
maintains its data itself. Utilities with constant and multilevel tariffs only go into the hub repo
[`strompreise-schweiz.github.io`](https://github.com/Strompreise-Schweiz/strompreise-schweiz.github.io)
instead. The utility in this template is fictional.

After creating the repo, enable Settings > Pages > Source "GitHub Actions" and add the repo to
`repositories.json` in the hub repo. The data is then served at
`https://data.strompreise-schweiz.ch/<repo>/`.

Then replace this paragraph and the ones above with a short description of the utility, and add the
badges that show whether its file follows the [OpenAPI definitions of the VSE](https://github.com/Strompreise-Schweiz/tariff-core/tree/main/schemas/vse). Replace
`<repo>` with the repo name:

```markdown
[![VSE 1.0.0](https://img.shields.io/endpoint?url=https%3A%2F%2Fdata.strompreise-schweiz.ch%2F<repo>%2Fbadges%2Fvse-1.0.0.json)](data/vse-conformance.json)
[![VSE 1.0.1](https://img.shields.io/endpoint?url=https%3A%2F%2Fdata.strompreise-schweiz.ch%2F<repo>%2Fbadges%2Fvse-1.0.1.json)](data/vse-conformance.json)
```

## Three tariff forms

| `tariffForm` | Meaning | Example here |
|---|---|---|
| `constant` | One price at all times | Sample Energy Single Rate |
| `multilevel` | Prices by month, weekday or time | Sample Energy Dual Rate |
| `dynamic` | Prices published each day for the next day | Sample Grid Dynamic |

## What a new organization needs

1. Create the repo from this template and adapt `config/source.json`.
2. Enter a `url` in `static.sources`. If the utility has no usable JSON, write the source by hand as
   `curation/<year>.source.json`.
3. For dynamic tariffs, add an entry in `dynamic` and start the workflow by hand once.
4. Propose products with `suggest-products.ts`, check them against the price sheet, and copy them
   to `curation/<year>.json`.

See [`adding-organization.md`](https://github.com/Strompreise-Schweiz/tariff-core/blob/main/docs/adding-organization.md).

## Structure

| Path | Content | Who changes it |
|---|---|---|
| `config/source.json` | Data sources | Person |
| `curation/<year>.json` | Corrections and product mapping, each with a reason | Person |
| `curation/<year>.source.json` | Hand-written source, only if needed | Person |
| `data/**` | Generated data | GitHub Actions only |
