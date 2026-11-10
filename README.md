# Example: power utility repository

Copy this repository for each new organization. The utility in it is fictional.

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
4. Propose products with `suggest_products.py`, check them against the price sheet, and copy them
   to `curation/<year>.json`.

See [`adding-organization.md`](https://github.com/Strompreise-Schweiz/tariff-core/blob/main/docs/adding-organization.md).

## Structure

| Path | Content | Who changes it |
|---|---|---|
| `config/source.json` | Data sources | Person |
| `curation/<year>.json` | Corrections and product mapping, each with a reason | Person |
| `curation/<year>.source.json` | Hand-written source, only if needed | Person |
| `data/**` | Generated data | GitHub Actions only |
