# BM25 vs BGE-small: Sparse and Dense Information Retrieval

![Python](https://img.shields.io/badge/Python-3.9-blue?logo=python)
![NLP](https://img.shields.io/badge/Domain-NLP-green)
![Task](https://img.shields.io/badge/Task-Information%20Retrieval-orange)
![Evaluation](https://img.shields.io/badge/Evaluation-TREC%20%7C%20MS%20MARCO-purple)

## Project Overview

This project presents an experimental comparison of two fundamental approaches to Information Retrieval (IR): **BM25**, a traditional sparse lexical retrieval algorithm, and **BGE-small**, a neural dense retrieval model designed to capture semantic relationships between queries and documents.

The main objective is to investigate the differences between lexical matching and semantic retrieval, evaluate their effectiveness across established information retrieval benchmarks, and analyze their retrieval performance using standard IR evaluation metrics.

Both methods are implemented and evaluated independently, without using hybrid retrieval, reranking, or reciprocal rank fusion.

## Retrieval Approaches

### 1. BM25 — Sparse Retrieval

BM25 is a probabilistic ranking function that estimates document relevance based on query-term frequency, inverse document frequency, and document length normalization.

**Key characteristics:**
- Lexical term matching
- Sparse document representation
- Statistical relevance scoring
- Efficient CPU-based retrieval

### 2. BGE-small — Dense Retrieval

BGE-small (`BAAI/bge-small-en-v1.5`) is a transformer-based embedding model that maps queries and documents into dense vector representations. Retrieval is performed by comparing their semantic representations.

**Key characteristics:**
- Contextual semantic representations
- Dense vector embeddings
- Semantic similarity-based retrieval
- FAISS-based vector search

## Datasets and Benchmarks

The experiments use three established information retrieval evaluation datasets:

| Dataset | Number of Queries |
|---|---:|
| TREC DL 2019 | 43 |
| TREC DL 2020 | 54 |
| MS MARCO dev.small | 2,000 |

For each query, the top 1,000 retrieved documents are considered for evaluation.

## Evaluation Metrics

The retrieval systems are evaluated using the following standard metrics:

| Metric | Description |
|---|---|
| nDCG@10 | Ranking quality in the top 10 results |
| MRR@10 | Reciprocal rank of the first relevant result |
| nDCG@100 | Ranking quality in the top 100 results |
| MAP | Mean Average Precision |
| Recall@10 | Relevant documents retrieved in the top 10 |
| Recall@100 | Relevant documents retrieved in the top 100 |
| Recall@1000 | Relevant documents retrieved in the top 1,000 |

## Experimental Results

### TREC DL 2019

| Metric | BM25 | BGE-small | Improvement |
|---|---:|---:|---:|
| nDCG@10 | 0.5169 | **0.7197** | +0.2028 |
| MRR@10 | 0.6812 | **0.8597** | +0.1785 |
| nDCG@100 | 0.5204 | **0.6531** | +0.1327 |
| MAP | 0.3077 | **0.4597** | +0.1520 |
| Recall@10 | 0.1675 | **0.2614** | +0.0939 |
| Recall@100 | 0.5252 | **0.6320** | +0.1068 |
| Recall@1000 | 0.7762 | **0.8252** | +0.0490 |

### TREC DL 2020

| Metric | BM25 | BGE-small |
|---|---:|---:|
| nDCG@10 | 0.5264 | **0.7121** |
| MRR@10 | 0.6629 | **0.8337** |
| nDCG@100 | 0.5437 | **0.6356** |
| MAP | 0.3326 | **0.4812** |
| Recall@10 | 0.2823 | **0.3813** |
| Recall@100 | 0.6208 | **0.6950** |
| Recall@1000 | 0.8275 | **0.8434** |

### MS MARCO dev.small

| Metric | BM25 | BGE-small |
|---|---:|---:|
| nDCG@10 | 0.3253 | **0.5065** |
| MRR@10 | 0.2907 | **0.4568** |
| nDCG@100 | 0.3788 | **0.5526** |
| MAP | 0.2971 | **0.4602** |
| Recall@10 | 0.4469 | **0.6784** |
| Recall@100 | 0.7047 | **0.8937** |
| Recall@1000 | 0.8794 | **0.9820** |

## Key Findings

The experimental results show that BGE-small outperforms BM25 across all reported evaluation metrics and all three benchmarks.

Key observations include:

- **Improved ranking quality:** BGE-small achieves higher nDCG scores, indicating better ranking of relevant documents.
- **Better early retrieval:** Higher MRR@10 values indicate that relevant documents are more likely to appear near the top of the results.
- **Improved semantic matching:** Dense embeddings can capture semantic relationships beyond exact keyword overlap.
- **Higher recall:** BGE-small retrieves a larger proportion of relevant documents, particularly on MS MARCO dev.small.

These findings highlight the effectiveness of dense semantic retrieval while demonstrating the importance of evaluating retrieval systems across multiple benchmarks.

## Computational Analysis

The experiments also compare the computational characteristics of both approaches.

| Metric | BM25 | BGE-small |
|---|---:|---:|
| Hardware | CPU | NVIDIA Tesla T4 |
| Indexing / Embedding Time | 7.44 min | 93.22 min |
| Storage Requirements | 1.18 GB | 4.43 GB |
| Total Search Time | 193.43 sec | 20.37 sec |
| Average Query Time | 92.24 ms | 9.71 ms |

**Note:** BM25 and BGE-small were executed on different hardware configurations. Therefore, the observed retrieval times should be interpreted as experimental measurements under the reported configurations, not as a hardware-controlled comparison of intrinsic algorithmic speed.

BGE-small requires more initial preparation time and storage, while achieving lower measured query latency in these experiments.

## Technologies and Tools

- Python
- PyTorch
- Hugging Face Transformers
- Sentence-Transformers
- BAAI/bge-small-en-v1.5
- FAISS
- NumPy
- Pandas
- TREC DL Benchmarks
- MS MARCO

## Project Structure

```text
BM25-vs-BGE-small/
│
├── notebooks/
│   ├── BM25_Retrieval.ipynb
│   ├── BGE_Dense_Retrieval.ipynb
│   └── Evaluation_and_Comparison.ipynb
│
├── results/
│   ├── TREC_DL19/
│   ├── TREC_DL20/
│   └── MS_MARCO/
│
├── figures/
│   ├── retrieval_comparison.png
│   ├── ranking_metrics.png
│   └── computational_analysis.png
│
├── README.md
└── requirements.txt
```

*The directory structure is provided as a recommended organization for the repository.*

## Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/BM25-vs-BGE-small.git
cd BM25-vs-BGE-small
```

Install the required dependencies:

```bash
pip install -r requirements.txt
```

Download the required datasets and configure their paths before running the notebooks.

## Skills Demonstrated

This project demonstrates practical experience in:

- Information Retrieval and Search Systems
- Sparse and Dense Retrieval
- Semantic Search and Text Embeddings
- Transformer-based NLP Models
- Vector Search and FAISS
- Benchmark Design and Evaluation
- Ranking Metrics and Performance Analysis
- Python-based Machine Learning Experiments
- Computational Efficiency Analysis

## Conclusion

This project provides a systematic comparison of traditional lexical retrieval and neural semantic retrieval. Across TREC DL 2019, TREC DL 2020, and MS MARCO dev.small, BGE-small achieves consistently stronger retrieval effectiveness than BM25. The experiments also reveal the trade-off between initial computational cost, storage requirements, and query-time performance.

The results demonstrate the practical value of dense retrieval models for semantic search and provide an experimental foundation for understanding modern information retrieval systems.

---

**Focus Areas:** Artificial Intelligence | Machine Learning | NLP | Information Retrieval | Semantic Search
