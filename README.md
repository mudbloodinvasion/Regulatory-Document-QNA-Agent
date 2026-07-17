# Regulatory-Document-QNA-Agent
An AI-powered agent that answers compliance-related questions based on a provided PDF document (e.g., a specific regulation), with explicit citations (section + page number) for every answer.

Built as a focused, demo-ready RAG (Retrieval-Augmented Generation) pipeline - no heavy infrastructure, just clean code.

---

## Objective

Develop an AI agent that:
- Reads a regulatory/compliance PDF
- Answers user questions strictly based on that document
- Explicitly cites the section and page number for every answer
- Clearly indicates when a question cannot be answered from the document

---

## Key Features

- Retrieval: RAG pipeline that extracts relevant context chunks from the uploaded PDF
- Citation: Every answer includes the page number (and section, where available) it was sourced from
- Free to run: Uses free embeddings (HuggingFace) + free-tier LLM (Google Gemini) - no paid API required
- Self-contained: Anyone can run this notebook with just their own free API key and a PDF - no extra setup

---

## Tech Stack

| Component | Tool |
|---|---|
| Language | Python 3 (Google Colab) |
| Orchestration | LangChain |
| PDF Loading | PyPDFLoader (pypdf) |
| Embeddings | HuggingFace sentence-transformers (free, local) |
| Vector Store | ChromaDB / FAISS |
| LLM | Google Gemini (free tier) |
| UI (optional) | Gradio |

---

## How to Run

### Option 1: Run in Google Colab (recommended)
1. Click the badge below to open the notebook directly in Colab:

   [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR-USERNAME/YOUR-REPO/blob/main/notebook.ipynb)

2. Click Runtime -> Run all
3. When prompted:
   - Upload your PDF (the regulation/compliance document you want to query)
   - Enter your free Gemini API key (get one at https://aistudio.google.com/app/apikey)
4. Scroll to the bottom and start asking questions in the test cells

### Option 2: Clone and run locally
```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPO.git
cd YOUR-REPO
pip install -r requirements.txt
jupyter notebook notebook.ipynb
```

---

## Repository Structure

```
├── notebook.ipynb        # Main Colab notebook (full pipeline)
├── README.md              # This file
├── requirements.txt        # Python dependencies
└── sample_docs/            # (optional) sample regulation PDFs for testing
```

---

## How It Works (Pipeline)

1. Document Loading - PDF is loaded with page-level metadata preserved
2. Chunking - Text is split into overlapping chunks, keeping page numbers attached to each chunk
3. Embeddings & Vector Store - Chunks are embedded and stored in a vector database for similarity search
4. Retrieval - Given a question, the most relevant chunks are retrieved
5. Answer Generation - The LLM generates an answer using only the retrieved context, and is prompted to cite the page/section it used
6. Citation Enforcement - Output is formatted to always show the source page number alongside the answer

---

## Limitations

- Answers are only as good as the PDF's text extractability (scanned/image-only PDFs may need OCR, not currently included)
- Free-tier LLM (Gemini) may have rate limits on heavy usage
- Section-level citation depends on how clearly the source PDF is structured (page-number citation is always reliable; section-name citation is best-effort)

---

## License

This project was built for academic/educational purposes.
