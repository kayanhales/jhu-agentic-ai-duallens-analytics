# DualLens Analytics

A RAG-powered investment analysis system that combines quantitative financial data with qualitative AI initiative documents to rank and recommend technology companies for investment.

Built as a project for the Agentic AI course at Johns Hopkins University (Week 4).

---

## What It Does

Traditional investment analysis focuses on financial metrics alone. DualLens takes a dual-lens approach — combining the numbers with the strategy to produce a more complete picture.

Given a set of companies (GOOGL, MSFT, IBM, NVDA, AMZN), the system:

- Pulls 3-year stock price history and financial metrics via the yFinance API
- Ingests each company's AI initiative documents (PDFs) into a vector database
- Uses RAG to answer natural language questions about each company's AI strategy
- Evaluates response quality using an LLM-as-Judge framework (groundedness + relevance)
- Scores and ranks companies for investment potential using both data streams

---

## Architecture

```
PDF Documents ──► Text Chunking ──► OpenAI Embeddings ──► ChromaDB Vector Store
                                                                    │
User Query ──────────────────────────────────────────► Similarity Retrieval
                                                                    │
Financial Data (yFinance) ───────────────────────────► LLM (gpt-4o-mini) ──► Ranked Output
```

---

## Key Concepts Demonstrated

| Concept | Details |
|---|---|
| **RAG pipeline** | End-to-end implementation from document ingestion to retrieval-augmented generation |
| **OpenAI API** | gpt-4o-mini with parameter tuning (temperature, max_tokens, top_p, frequency_penalty) |
| **OpenAI Embeddings** | text-embedding-ada-002 for document vectorization |
| **ChromaDB** | Vector store with similarity search |
| **LangChain** | Document loading, text splitting, and retrieval orchestration |
| **LLM-as-Judge** | Automated evaluation of RAG output quality on groundedness and relevance dimensions |
| **Prompt engineering** | System messages, user message templates, and iterative refinement |

---

## Tech Stack

- Python
- OpenAI API (gpt-4o-mini, text-embedding-ada-002)
- LangChain + LangChain-OpenAI
- ChromaDB
- yFinance
- PyPDF / PyPDFDirectoryLoader
- Matplotlib / Pandas
- Jupyter Notebook

---

## Setup

```bash
git clone https://github.com/kayanhales/jhu-agentic-ai-duallens-analytics.git
cd duallens-analytics
pip install -r requirements.txt
```

Create a `config.json` file:

```json
{
  "API_KEY": "your_openai_api_key_here",
  "OPENAI_API_BASE": "https://api.openai.com/v1"
}
```

Then open the notebook:

```bash
jupyter notebook JHU_AgenticAI_Project_1_Learners_Notebook-3.ipynb
```

---

## What I Learned

- Combining quantitative and qualitative data sources produces significantly better decision support than either alone
- Chunk size and overlap meaningfully affect retrieval quality — this required real trial and error
- Prompt structure (system message vs. user message framing) has a large impact on output consistency
- LLM-as-Judge is a practical evaluation pattern that doesn't require labeled ground truth data
