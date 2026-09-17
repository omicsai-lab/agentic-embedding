# Agentic Embedding — RNA-Seq PCA Analysis

RNA-Seq differential expression and PCA-based embedding experiments for breast cancer
subtype classification (TCGA BRCA: Luminal A vs. Basal), plus a parallel exploration on
an independent GEO dataset (GSE240671).

## Repo structure

```
actual_rnaseq_analysis/                         Main end-to-end pipeline
├── notebooks/
│   ├── pre-processing.ipynb                    Load raw counts + sample annotations
│   ├── deseq2.ipynb / dge.ipynb / dge2.ipynb    DESeq2 normalization & differential expression
│   ├── pathway.ipynb                           Pathway-weighted gene analysis
│   ├── pca_embedding_only.ipynb                PCA embedding construction
│   ├── agentic_ai_wpca_ebedding.ipynb          Agentic/weighted-PCA embedding variant
│   ├── sig_pca_classification.ipynb            Classification using significant-gene PCA embeddings
│   ├── comparisons.ipynb                       Cross-embedding comparison
│   ├── embedding_comparison_explanation.ipynb  Write-up of comparison results
│   ├── clean_end_to_end.ipynb / clean_end_to_end_analysis.ipynb  Consolidated full pipeline
│   ├── workflow_architecture.ipynb             Pipeline/architecture overview
│   └── archive/                                Deprecated / superseded notebooks
└── results/
    └── pathway/gene_weights.csv                Pathway gene weights output

agentic_ai_pca_based_embedding_experiments/     Secondary experiments on GSE240671
├── data/                                       Raw counts + GEO series matrix (gitignored)
├── notebooks/
│   └── preprocessing.ipynb                     Sample annotation extraction & preprocessing
└── results/                                    Experiment outputs
```

## Data

Raw data files (`*.rds`, `data/`, `GDCdata/`) are gitignored and not tracked in this repo.
Expected inputs:

- **TCGA BRCA** — STAR counts + Luminal A/Basal sample labels (via `GDCdata`), used by
  `actual_rnaseq_analysis`.
- **GSE240671** — `GSE240671_raw_counts_GRCh38.p13_NCBI.tsv` and
  `GSE240671_series_matrix.txt` from GEO, used by
  `agentic_ai_pca_based_embedding_experiments`. Place them under
  `agentic_ai_pca_based_embedding_experiments/data/`.

## Workflow

1. **Pre-process** raw counts and sample metadata.
2. **Differential expression** via DESeq2 to identify significant genes.
3. **Build embeddings** — PCA over all genes, significant genes only, and pathway-weighted genes.
4. **Classify & compare** — evaluate classification performance across embedding variants.
5. **Consolidate** — `clean_end_to_end*.ipynb` notebooks tie the full pipeline together end to end.

Start with `actual_rnaseq_analysis/notebooks/workflow_architecture.ipynb` for a high-level
overview, or `clean_end_to_end_analysis.ipynb` to run the consolidated pipeline directly.
