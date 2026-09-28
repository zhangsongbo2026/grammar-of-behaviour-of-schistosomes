# schistosome-grammar-v4

**Transfer cost, not transfer success: a measured migration of the structural grammar of behaviour from viruses to schistosomes.**

Code, data and results for the V4 revision of the schistosome behaviour grammar
(target journal: *Nature Communications*). Every number in the manuscript is
injected from `results/master_numbers.json` by the build script — no hand-typed
statistics anywhere in the text.

## What this repository contains

| Directory | Contents |
|---|---|
| `data/` | Real open data: 23 mitochondrial sequences (`fasta/`, accessions in `panel_labels.csv`), TRPtracker natural-variant table (1,377 records), ERA5 daily temperature & precipitation for six endemic foci (1990–2025), monthly aggregate |
| `scripts/` | Full pipeline, one command per experiment |
| `results/` | Every number in the manuscript as JSON; `master_numbers.json` is the single numeric source |
| `figures/` | Figs. 1–6 and Extended Data Figs. 1–9 (PNG 300 dpi + PDF) |
| `manuscript/` | DOCX (native OMML, XSD-validated 0 errors), PDF (XeLaTeX, 31 pages, 0 missing characters), LaTeX, Markdown source, cover letter |
| `preregistry/` | Frozen rehearsal-registry rules, archived blind scores for six documented hybrid events, falsifiable resistance-surveillance prediction, SHA-256 integrity hash |

## Headline results (V4)

- **Host range**: sequence layer beats the clade-only baseline — macro-F1 0.475 vs 0.248;
  exact paired permutation one-sided P = 0.046; clade-cluster bootstrap [0.123, 0.482];
  P(Delta R > 0) = 0.987.
- **Human infection**: grammar's primary estimator not separated (P(Delta R > 0) = 0.884);
  but a Gaussian naive-Bayes control reaches **0.790** on identical folds — earlier negative
  verdicts were estimator-limited, not feature-limited (ledger row P9).
- **Rehearsals**: under the official calibrated estimator (nested temperature-scaled GB,
  ECE 0.477 → 0.244) all six literature-documented hybrid events score 0.00–0.26 —
  abstention-leaning; nearest-neighbour rule 3/6. The pre-calibration "1.00 hit" on the
  Senegal hybrid zone is identified as an estimator artifact.
- **Resistance boundary**: confirmed on an independent community resource — TRPtracker:
  92.2% of 345 functionally profiled natural TRPM_PZQ variants are wild type; the most
  desensitising circulating allele shifts potency only **2.4-fold vs 377-fold** laboratory,
  exactly the boundary-excluded regime predicted at WHO 2024 coverage (u = 0.396).
- **Climate** (daily ERA5 + IPCC AR6 ensemble bands + precipitation gate): Richard-Toll
  loses 67% [54, 79] of annual transmission potential by 2100 (SSP2-4.5; 89% under
  SSP5-8.5); Mwache 43%/76%; Chinese foci within ±7%; Ukerewe stable; 82% of
  Richard-Toll months fall below the 25 mm moisture floor.
- **Markov budget**: strong axiom falsified (rho = −0.196, permutation P = 0.002;
  epsilon_M = 0.111) — schistosome behaviour is carried by co-evolved snail–parasite
  pairing, i.e. by lineage history, not by genome sequence.

## Reproducibility

```bash
pip install -r requirements.txt

# one command per experiment (in order):
python scripts/e10_analysis.py          # sequence layer + Markov budget + LOSO
python scripts/e10b_adjudication.py     # paired bootstrap adjudication (V3 baseline)
python scripts/e20_stats_upgrade.py     # permutation test, clade bootstrap, convergence
python scripts/e21_estimators_nn.py     # calibration + NN baseline + 6 rehearsals
python scripts/e22_baselines.py         # estimator comparison suite
python scripts/e11_network2.py          # STRING topology (see note below)
python scripts/e23_climate_v4.py        # daily ERA5 + precipitation + AR6 bands
python scripts/e24_paleo_v4.py          # 17 palaeo anchors, weighted posteriors
python scripts/master_numbers.py        # single-source numeric aggregation
python scripts/build_v4_text.py && python scripts/build_v4_text2.py
python scripts/figures.py && python scripts/ed_figures.py && python scripts/figures_v4.py
python scripts/build_docx_v4.py         # pandoc -> OMML -> XSD validation
```

**STRING note**: the STRING v12.0 bulk files used for the network layer
(`protein.links.detailed.v12.0`, taxids 6182/6183/6184/6185/6186/6188/31246/48269,
score >= 0.7) total ~300 MB and are therefore not committed; `scripts/e11_download_string.py`
re-downloads them with resume. The derived topology descriptors for the four species
processed end-to-end are committed in `results/e11_string_topology.json`.

## Data provenance (all downloads 2026-09-27)

- NCBI Nucleotide / ENA — mitochondrial genomes (accessions in `data/panel_labels.csv`)
- STRING v12.0 — protein-protein interactions
- TRPtracker (Marchant lab) — natural TRPM_PZQ variants with relative-activity values
- Open-Meteo archive API (ERA5) — daily temperature and precipitation
- IPCC AR6 WGI — SPM.1 likely ranges (CMIP6 ensemble bands)

Seeds: 42 (LOSO fits), 2026 (permutation tests), 7 (rehearsals), 5 (baseline suite),
11 (label-noise test). Software: Python 3.11, scikit-learn 1.3.0, networkx 3.6.1.

No generative model was used for any datum, figure or number. Coverage limitations are
reported as results (see manuscript Discussion and Table 3 roadmap).

## License

MIT (code). Data files retain the licences of their original sources.
