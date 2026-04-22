# BBB Cross-Species Atlas — Gene Expression Browser

A static website for exploring gene expression across the Blood-Brain Barrier (BBB) single-cell atlas spanning six species.

## Features
- **Gene Search**: Search 7,685 orthologous genes by human, mouse, macaque, marmoset, rat, or pig symbol
- **Expression Dot Plot**: Size = fraction of cells expressing, color = mean expression
- **Bar Chart**: Per-species / per-cell-type expression
- **Conservation Panel**: Expressolog Pearson r across species
- **UMAP Explorer**: Cross-species UMAP with Canvas rendering
- **Cell Type Markers**: Top markers per species and cell type
- **RMT Drug Targets**: Translatability assessment for 10 receptor-mediated transcytosis targets

## Data
- **6 species**: Human, Macaque, Marmoset, Mouse, Rat, Pig
- **7 BBB cell types**: Capillary EC (Cap_EC), Arterial EC (Art_EC), Venous EC (Ven_EC), Pericyte, SMC, Fibroblast, EC (unclassified)
- **7,685 orthologous genes** (6-way intersection)
- **144,064 cells total**

Not all cell types are present in every species — see `data/metadata.json` → `cell_types_per_species`. Rat and pig have only a few shared cell types and are excluded from conservation means (flagged in the UI).

## Architecture
Single-page app. Everything is in `index.html` (HTML + CSS + JS inline). Data lives in `data/`:

- `metadata.json` — species list, cell types, colors, RMT panel, translatability
- `gene_index.json` — 7,685 gene rows with ortholog symbols + `max_mean` + `is_rmt`
- `gene_data.json` — per-gene per-species per-cell-type expression + conservation + RMT info
- `umap_coords.json` — 30,000 UMAP points (downsampled)
- `markers.json` — top markers per species × cell type
- `expr_table.csv` — flat expression table (mean + pct) for download

## Deployment (GitHub Pages)
This repo is already wired to `https://github.com/rustlab1/BBB_species_browser`. After a push to `main`, GitHub Pages will serve from the repo root. `.nojekyll` is present so the `_archive/` prefix is not required — Jekyll is disabled.

## Local Preview
```bash
python -m http.server 8000
# Then open http://localhost:8000
```

## Citation
If you use this atlas, please cite the underlying single-cell datasets:
- Vanlandewijck et al. (2018) Nature
- Pfau et al. (2024)
- Yang et al. (2022)
- Wälchli et al. (2024)
- Chiou et al. (2023)
- Wang et al. (2022) — pig GSE193975
