# NSW Road Rules RAG Assistant — Test-Driven RAG

**Group 56**

## Team Members

| Student ID | Full Name | Role |
|---|---|---|
| s4224928 | Sahana Sree Kumaresan | Data Engineering |
| s4222858 | Chris Benny Vadakkan | Knowledge Base Architecture |
| s4220177 | Neil Anton Dsouza | RAG Pipeline Development |
| s4225140 | Vineet Nilesh Bangera | Evaluation & Testing |

## Project Aim

This project develops and evaluates a Retrieval-Augmented Generation (RAG) chatbot that answers NSW road rule questions by grounding its responses in the official NSW Road User's Handbook, evaluated against real questions from the official Driver Knowledge Test (DKT) question bank.

## Domain / Knowledge Base

**Domain:** NSW road rules (text-based content only)

**Source:** NSW Road User's Handbook (212 pages), published by Transport for NSW.

Sign and diagram-based content was deliberately excluded from scope, as it would require image-based retrieval methods beyond this project's intended focus.

## Tech Stack

| Component | Tool |
|---|---|
| PDF text extraction | pdfplumber |
| Chunking | Custom chunking (~150 words per chunk, with overlap) |
| Embeddings | sentence-transformers (`all-MiniLM-L6-v2`) |
| Vector store | ChromaDB |
| LLM | Ollama (`llama3.2:3b`) |
| Interface | Streamlit *(in progress)* |
| Evaluation | Recall@K, MRR, NDCG (retrieval); BERTScore, ROUGE-1 (answer quality, in progress) |


Run the notebooks in order: `01_ingest_handbook.ipynb` → `02_extract_dkt.ipynb` → `03_retrieval_eval.ipynb`.

## Evaluation Framework

We evaluate the RAG pipeline using metrics adapted from the Walert paper:

- **Retrieval quality:** Recall@1, Recall@5, MRR, and NDCG@5 on a golden set of 20 known questions, 10 paraphrased ("inferred") questions, and 10 deliberately out-of-scope questions
- **Hallucination control:** Manual verification that out-of-scope questions (e.g. other states' rules, unrelated topics) are correctly declined rather than answered
- **Answer quality (in progress):** BERTScore and ROUGE-1 against official DKT answers

**Preliminary results:** Recall@1: 60%, Recall@5: 90%, MRR: 0.706, NDCG@5: 0.746

See `docs/Milestone1_Report.docx` for full details.

## Project Management

- **Trello board:** [https://trello.com/invite/b/6a8795d3d87bde00f98e23ea/ATTI9cb8f6358fc52fb36844844b03c7e2dfEAE3D954/wil-56](https://trello.com/invite/b/6a8795d3d87bde00f98e23ea/ATTI9cb8f6358fc52fb36844844b03c7e2dfEAE3D954/wil-56)

## Status

Current milestone: **Milestone 1** 

## Acknowledgements

This project is inspired by and reproduces components of [Walert](https://github.com/rmit-ir/walert), developed by RMIT's School of Computing Technologies.
