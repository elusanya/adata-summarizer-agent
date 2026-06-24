# AnnData Summarizer Agent

**Rapid AI-powered analysis of single-cell RNA-seq data with free inference via Groq.**

## Overview

Automatically generate comprehensive summaries of AnnData objects with tables, visualizations, and AI-driven biological insights. Supports both guided analysis (with Claude/Groq LLM) and standalone visualization (tables + plots only).

## Use Cases

- **Exploratory Data Analysis (EDA)**: Instantly understand dataset structure, cell populations, gene expression patterns, and technical metrics
- **Collaborative Handoffs**: Share data summaries with collaborators without manual report generation
- **Preprocessing QC**: Validate post-filtering/normalization steps with automated statistical summaries
- **Publication Support**: Generate figures and summary tables for manuscript supplements
- **Dataset Evaluation**: Rapidly assess public datasets (GEO, CellxGene) before committing to downstream analysis

## Getting Started

### Prerequisites
```
python >= 3.8
scanpy
numpy, scipy
plotly
groq  # Optional, for AI-powered summaries
```

### Installation
```bash
pip install scanpy plotly groq numpy scipy
```

### Minimal Example

**Without AI** (tables + plots only):
```python
from adata_summarizer_agent import summarize
import scanpy as sc

adata = sc.read_h5ad('your_data.h5ad')
summarize(adata)
```

**With AI** (requires free Groq API key):
```python
# Get free Groq key at console.groq.com
summarize(adata, groq_api_key='gsk_...')
```

### Interactive Chat with Data
```python
from adata_summarizer_agent import chat
import scanpy as sc

adata = sc.read_h5ad('your_data.h5ad')
chat(adata, groq_api_key='gsk_...')
```

## Features

### Automatic Summary Includes:
- **Dataset Metrics**: Observations, variables, memory footprint, sparsity
- **Cell Annotations**: Unique cell types, cluster distributions, composition plots
- **Gene Statistics**: Top expressed genes, variance metrics, gene ontology summaries
- **Technical QC**: Mitochondrial/ribosomal content, doublet flags, batch effects
- **Dimensionality Reduction**: UMAP/t-SNE plot summaries and clustering interpretation
- **Biological Insights**: AI-generated interpretation of cell populations and gene signatures (with Groq)

### Visualization
- Interactive Plotly figures (zoom, hover, save as PNG)
- Heatmaps for top genes by cell type
- Distribution plots for continuous variables
- Composition/stacked bar charts for categorical metadata

### Optional AI Layer
- Free inference via Groq (Llama 3-70b) — no OpenAI credits needed
- Contextual interpretation of gene clusters and cell populations
- Natural language queries on dataset structure

## Customization

### Adjust Output Verbosity
```python
summarize(adata, groq_api_key=key, verbose=True)  # Full markdown + plots
summarize(adata)  # Tables + plots only
```

### Use Alternative LLM
Replace Groq with Claude API:
```python
# Modify the agent code to swap groq client with anthropic.Anthropic()
```

## Productivity Gains

- **Time Saved**: ~45 min/dataset (vs. manual EDA + plot generation)
- **Consistency**: Standardized QC reporting across projects
- **Collaboration**: Non-bioinformaticians can understand data structure immediately
- **Iteration Speed**: Rapid dataset evaluation for pipeline decisions

## Output

All outputs are rendered in Jupyter notebook as:
- Interactive HTML tables (searchable, sortable)
- Interactive Plotly visualizations (saved as .html for sharing)
- Markdown-formatted summaries (exportable to PDF)
- Chat interface for ad-hoc queries

## Limitations & Caveats

- Requires **valid H5AD or AnnData-compatible format** (not raw FASTQ/BAM)
- AI summaries best with **>100 cells** (sparse datasets may have low signal)
- Groq API has **rate limits** (free tier: ~30 requests/min)
- **Does not replace domain expertise** — use as discovery tool, validate biological claims

## Examples

### Example 1: Public Dataset EDA
```python
import scanpy as sc
from adata_summarizer_agent import summarize

# Download from CellxGene or GEO
adata = sc.datasets.pbmc68k_reduced()
summarize(adata, groq_api_key='gsk_...')
```

### Example 2: Post-QC Validation
```python
# After your own filtering/normalization
adata_qc = adata[adata.obs['qc_pass'] == True]
summarize(adata_qc)  # No AI needed if you know what to expect
```

### Example 3: Dataset Comparison
```python
for dataset_path in ['study_A.h5ad', 'study_B.h5ad']:
    adata = sc.read_h5ad(dataset_path)
    print(f"\n### {dataset_path}")
    summarize(adata)
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| `ModuleNotFoundError: scanpy` | `pip install scanpy` |
| Groq API key invalid | Regenerate at [console.groq.com](https://console.groq.com) |
| Large dataset hangs | Subset to 10k cells for initial run; AI summaries don't scale to >100k cells efficiently |
| Plots not rendering | Ensure `plotly` is installed; try `pio.renderers.default = "notebook"` |

## Contributing

Found a bug or want to add a feature (e.g., spatial transcriptomics support, DEG summaries)? Contributions welcome.

## Author

**Sanya Puri** | Elucidata Corporation | Bioinformatics Specialist

## License

MIT

---

**Questions?** Reach out in Slack or via internal wiki.
