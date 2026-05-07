# BBB Cross-Species Atlas — Discovery Toolkit

A static web app for exploring gene expression and drug-delivery biology across the Blood-Brain Barrier (BBB) single-cell atlas spanning six species.

## Tabs / features

- **Expression** — Dot plot, bar chart, cross-species bar chart, and per-species z-score across cell types.
- **UMAP** — 30,000-cell joint UMAP coloured by cell type / species / gene; option to split by species.
- **Conservation** — Pearson r vs human across reliable species (macaque, marmoset, mouse) with reliability badges.
- **BBB Pathways** — 21 curated gene families (tight junctions, efflux pumps, RMT receptors, transcytosis regulators, SLC families, GPCRs, Wnt-BBB induction, …) tagged as **Help** (drug delivery / nutrient supply) or **Hindrance** (barrier / efflux). Each gene card shows in-atlas status, max mean expression, top cell type, conservation r and τ specificity at a glance.
- **Drug Permeability** — 35 curated CNS-relevant drugs (high / moderate / low permeability + carrier-mediated + biologic / engineered) with their BBB transporter targets. Click any drug to see the live cross-species expression profile of every transporter it interacts with.
- **Cross-Talk** — 40 curated ligand–receptor pairs scored as ligand-mean (sender) × receptor-mean (receiver) per species. Shows a sender × receiver heatmap, a ranked pair table, and a per-pair × per-species conservation heatmap that highlights species-specific vs broadly conserved signaling.
- **Compare** — Side-by-side dot plots of two genes plus an A-vs-B mean-expression scatter (Pearson r) and per-cell-type log₂ fold-change.
- **Heatmap** — Multi-gene heatmap across all 27 (species × cell type) groups with z-score / log10 / raw normalization, hierarchical clustering, and one-click presets (RMT panel, tight junctions, efflux, capillary EC markers).
- **Specificity** — τ index (Yanai et al. 2005) per species; surface highly cell-type-specific genes with optional minimum-expression and τ thresholds.
- **Markers** — Within-species top markers per cell type with sortable score / log₂FC / padj / pct_in / pct_out.
- **Sidebar gene card** — RMT badge, family badges, external links to NCBI, UniProt, Human Protein Atlas, Open Targets, GeneCards, OMIM, Ensembl. "Use as A / B / + Heatmap" hand-offs.
- **All-human-gene search** — Symbols outside the 6-way ortholog intersection (e.g. CLDN5, ABCB1, GLUT1, ACTA2) are still searchable: the toolkit shows their curated BBB family information plus external links rather than a dead-end.

## Data files

- `metadata.json` — species list, cell types, colors, RMT panel, translatability categories
- `gene_index.json` — 7,685 gene rows with ortholog symbols + max_mean + is_rmt
- `gene_data.json` — per-gene per-species per-cell-type expression + conservation + RMT info
- `umap_coords.json` — 30,000 UMAP points (downsampled)
- `markers.json` — top markers per species × cell type
- `expr_table.csv` — flat expression table for download
- `gene_families.json` — 21 curated BBB gene families (235 gene entries; 144 in atlas, 91 curated-but-absent shown with informative badges)
- `drugs.json` — 35 curated CNS-relevant drugs with BBB-permeability category and transporter targets
- `lr_pairs.json` — 40 curated ligand–receptor pairs at the BBB neurovascular unit

## Atlas scope

- **6 species** — Human, Macaque, Marmoset, Mouse, Rat, Pig
- **7 BBB cell types** — Capillary EC (Cap_EC), Arterial EC (Art_EC), Venous EC (Ven_EC), Pericyte, SMC, Fibroblast, EC (unclassified)
- **7,685 orthologous genes** (6-way intersection)
- **144,064 cells total**
- **Vascular only** — astrocytes, microglia, neurons, oligodendrocytes are not present (parent datasets enriched for vascular cells)

Not all cell types are present in every species. Rat and pig have only a few shared cell types and are excluded from conservation means (flagged in the UI).

## Architecture

Single-page app. Everything is in `index.html` (HTML + CSS + JS inline). Data lives in `data/`.

## Local preview

```bash
python -m http.server 8000
# Then open http://localhost:8000
```

## Deployment (GitHub Pages)

Wired to `https://github.com/rustlab1/BBB_species_browser`. After a push to `main`, GitHub Pages rebuilds the site from the repo root. `.nojekyll` is present so Jekyll is disabled.

## Citation

If you use this atlas, please cite the underlying single-cell datasets:
- Vanlandewijck et al. (2018) Nature
- Pfau et al. (2024)
- Yang et al. (2022)
- Wälchli et al. (2024)
- Chiou et al. (2023)
- Wang et al. (2022) — pig GSE193975
