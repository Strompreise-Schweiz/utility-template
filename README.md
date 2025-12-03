# Elektrizitätswerk Wangen Electricity Data

This repository provides **open electricity data** for [elektrizitaetswerk-wangen](./data/supplier.json).  It is part of the [Strompreise Schweiz](https://www.strompreise-schweiz.ch) initiative.

## Contents

- **`/data`**  
  JSON files containing detailed information about the electricity supplier, its tariffs, and prices.

- **`/assets`**  
  Supplier logo and related visual assets.

All data is structured in a machine-readable way to support integration with external applications and services.

## Data Validation

Every dataset is automatically validated against the [`supplier-data-validation`](https://github.com/Strompreise-Schweiz/supplier-data-validation) schemas using GitHub Actions. This ensures consistent structure and reliable data quality across suppliers.

## Usage

The data can be freely used for:

- Research and analysis  
- Integration into applications and services  
- Visualizations and comparisons  

If you build something cool with it, we’d love to hear about it!

## Website

For more information about the initiative and to explore Swiss electricity tariffs, visit [www.strompreise-schweiz.ch](https://www.strompreise-schweiz.ch).

## License

The data in the [`/data`](./data) folder is licensed under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

Logos and other materials in the [`/assets`](./assets) folder are provided for reference only and may be subject to separate rights.
