# Quick Start Guide: AnnData Summarizer Agent

## 1. Get Your Free Groq Key
1. Go to [console.groq.com](https://console.groq.com)
2. Sign up (or log in)
3. Click **API Keys** → **Create API Key**
4. Copy the key (starts with `gsk_`)

## 2. Install Dependencies
```bash
pip install -r requirements.txt
```

## 3. Open the Notebook
```bash
jupyter notebook adata_summarizer_agent.ipynb
```

## 4. Use It

### Option A: Quick Summary (No AI)
```python
import scanpy as sc
from adata_summarizer_agent import summarize

adata = sc.read_h5ad('your_data.h5ad')
summarize(adata)  # Tables + plots only
```

### Option B: Full Summary with AI Insights
```python
summarize(adata, groq_api_key='gsk_YOUR_KEY_HERE')
```

### Option C: Chat with Your Data
```python
from adata_summarizer_agent import chat

chat(adata, groq_api_key='gsk_YOUR_KEY_HERE')
```

## Real-World Use Cases at Elucidata

✅ **GEO Dataset Evaluation**: Download GSE\*\*\*\*\*\*.h5ad, run summarize() → instant QC report for client intake  
✅ **Post-Filtering Validation**: After your scRNA-seq QC pipeline → verify clustering + cell type distributions  
✅ **Treg/Autoimmunity Studies**: Rapid cell population profiling for literature dataset comparisons  
✅ **Knowledge Graph Entity Extraction**: Use AI summaries to identify key cell types and marker genes for biological entities  
✅ **Collaboration Handoffs**: Share interactive plots + summaries with non-bioinformatician team members  

## Typical Runtime
- **Small dataset** (5k cells): 30 seconds
- **Medium dataset** (50k cells): 2–3 minutes
- **Large dataset** (200k+ cells): 5–10 minutes (with AI), <2 min without AI

## Outputs Generated
- Interactive HTML tables (searchable, sortable)
- Plotly visualizations (zoom, hover, export to PNG)
- Markdown summary (optional, with AI)
- Chat interface for ad-hoc exploration

## Troubleshooting

**"ModuleNotFoundError: scanpy"**
→ `pip install scanpy`

**"Invalid API key"**
→ Regenerate at console.groq.com

**"Plots not showing"**
→ Ensure you're running in Jupyter; try `!pip install plotly-orca`

**Large datasets hang**
→ Subset to 10k cells first; AI summaries degrade with >100k cells

## Need Help?
- Check SKILL.md for detailed feature documentation
- Slack: @Sanya or reach out in #bioinformatics
- GitHub: Link to repo once shared org-wide

---

**Happy analyzing!** 🧬
