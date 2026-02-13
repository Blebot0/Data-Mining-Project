# Reddit Hyperlink Network: Dataset Comparison, Selection, and EDA

## 📖 Overview

This project is a **Data Mining Course (CSCE 676)** checkpoint that selects a dataset supporting both course-covered and external techniques, then performs exploratory data analysis (EDA) on the chosen dataset. It provides:

- **Dataset Comparison**: Systematic evaluation of three candidate datasets (Reddit Hyperlink Network, Sentiment140, Hate Speech) across data quality, algorithmic feasibility, bias, and ethical considerations.
- **Dataset Selection**: Justified choice of the **Reddit Hyperlink Network** for graph mining, PageRank, community detection, and association-rule mining, plus external techniques (GNNs/node embeddings, temporal and signed network analysis).
- **Exploratory Data Analysis**: Data loading, preparation, graph construction, degree distributions, sentiment analysis, PageRank, Louvain community detection, and subreddit co-link pattern mining (Apriori / association rules).

The notebook (`237007751_checkpoint1.ipynb`) accompanies a data mining course project and documents data basics, collection, cleaning, and bias awareness for the Reddit hyperlink network.

**Author:** Keshav Kapur | **UIN:** 237007751

---

## 📦 Installation

Clone this repository and install dependencies:

```bash
git clone https://github.com/<your-username>/Data-Mining-Project.git
cd Data-Mining-Project
pip install -r requirements.txt
```

**Dependencies** (see `requirements.txt`): `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `mlxtend`, `urllib3`, `networkx`.

For a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate  
pip install -r requirements.txt
```

---

## ⚡ Quick Start

### 1. Add Reddit Hyperlink Data

The notebook downloads the **Reddit Hyperlink Network** (SNAP) automatically if not present:

- **Body links**: [soc-redditHyperlinks-body.tsv](https://snap.stanford.edu/data/soc-redditHyperlinks-body.tsv) (~319 MB)
- **Title links**: [soc-redditHyperlinks-title.tsv](https://snap.stanford.edu/data/soc-redditHyperlinks-title.tsv) (~369 MB)

Place them in `data/` or run the notebook; it will create `data/` and download when needed.

### 2. Run the Notebook

Open and run all cells in `237007751_checkpoint1.ipynb`:

```bash
jupyter notebook 237007751_checkpoint1.ipynb
# or
jupyter lab 237007751_checkpoint1.ipynb
```

The notebook uses **body** links as the primary dataset (more substantive than title-only links).

### 3. Main Workflow in the Notebook

| Section | Description |
|--------|-------------|
| **(A)** | Identification of three candidate datasets (Reddit, Sentiment140, Hate Speech) |
| **(B)** | Comparative analysis (tasks, quality, feasibility, bias, ethics) |
| **(C)** | Dataset selection: Reddit Hyperlink Network + rationale and trade-offs |
| **(D)** | EDA: load TSVs → prepare & clean → build directed graph → degree distributions → sentiment → PageRank → community detection → Apriori/association rules |
| **(E)** | Initial insights, hypotheses, and research questions |
---

## 📊 Example Output

**Graph summary (body links):**

| Metric | Value |
|--------|--------|
| Nodes (subreddits) | 35,776 |
| Unique directed edges | 137,821 |
| Total hyperlinks (multi-edges) | 286,561 |
| Density | ~0.0001 |
| Time range | 2013-12-31 → 2017-04-30 |

**Core columns (after preparation):**

| Column | Description |
|--------|-------------|
| `SOURCE_SUBREDDIT` | Subreddit that posts the link |
| `TARGET_SUBREDDIT` | Subreddit being linked to |
| `POST_ID` | Reddit post ID |
| `TIMESTAMP` | When the link was posted |
| `POST_LABEL` | Link sentiment: +1 (positive) or -1 (negative) |

**Sample frequent 2-itemsets (co-linked subreddit pairs):**

- `askreddit` + `iama`, `askreddit` + `pics`, `askreddit` + `todayilearned`, …
- Association rules (e.g. `mhocpress` → `mhoc`) with confidence and lift.

---

## 🧩 Key Features

- **Deterministic data pipeline**: Load body/title TSVs → rename columns → parse timestamps → aggregate multi-edges (weight, average sentiment).
- **Directed signed graph**: NetworkX `DiGraph` with edge attributes `weight` and `avg_sentiment` for PageRank and signed/temporal analysis.
- **Graph statistics**: Density, in/out degree, WCC/SCC, reciprocity.
- **Visualizations**: Degree distributions (in/out), sentiment distribution, temporal activity, PageRank rankings, community subgraphs.
- **Community detection**: Louvain method to find subreddit clusters (gaming, politics, memes, etc.).
- **Association rules**: Baskets = “source subreddit → set of target subreddits”; Apriori + confidence/lift for co-link patterns.

---

## 📝 Notes

- **Data**: Reddit Hyperlink Network from [SNAP (Stanford)](https://snap.stanford.edu/data/soc-RedditHyperlinks.html). Research/academic use; data derived from public Reddit posts.
- **Bias**: English-language and popular subreddits dominate; sentiment labels are crowdsourced. See Section (B) in the notebook for a full bias and ethics discussion.
- **Scale**: ~35K nodes and ~138K unique edges (body) fit in memory; NetworkX and mlxtend run on a typical laptop.
- Data files are not committed (too large); the notebook downloads them when needed.

---

## ✨ Citation

If you use this dataset or build on this code, please cite the Reddit Hyperlink Network paper:

```bibtex
@inproceedings{kumar2018community,
  title={Community Interaction and Conflict on the Web},
  author={Kumar, Srijan and Hamilton, William L. and Leskovec, Jure and Jurafsky, Daniel},
  booktitle={Proceedings of the 2018 World Wide Web Conference (WWW 2018)},
  year={2018},
}
```

Dataset: [SNAP – Reddit Hyperlink Network](https://snap.stanford.edu/data/soc-RedditHyperlinks.html).
