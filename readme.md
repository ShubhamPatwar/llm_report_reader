# 🏥 Medical Report RAG Assistant

An end-to-end Retrieval-Augmented Generation (RAG) application that allows users to query pathology and diagnostic reports using natural language.

The system extracts information from PDF-based medical reports, converts the report into semantically meaningful chunks, stores them in a vector database, retrieves relevant medical information based on user queries, and generates accurate responses using an LLM through OpenRouter.

---

## 🚀 Project Objective

Medical reports often contain multiple sections such as:

- Liver & Kidney Panel
- Lipid Profile
- Thyroid Profile
- HbA1c
- Vitamin D
- CBC

Patients and healthcare professionals may need to quickly retrieve specific information without manually reading the entire report.

This project aims to build an intelligent question-answering system that can:

- Understand medical reports
- Retrieve relevant sections
- Answer user questions in natural language
- Demonstrate an end-to-end RAG architecture

---

## 🏗️ Architecture

```text
Medical PDF
    ↓
PyPDF Text Extraction
    ↓
Semantic Section-Based Chunking
    ↓
LangChain Documents
    ↓
SentenceTransformer Embeddings
    ↓
FAISS Vector Database
    ↓
Retriever
    ↓
OpenRouter LLM
    ↓
Natural Language Answer
```

---

## 🔧 Technologies Used

### PDF Processing
- PyPDF

### RAG Framework
- LangChain

### Embedding Model
- SentenceTransformers
- all-MiniLM-L6-v2

### Vector Database
- FAISS

### LLM Provider
- OpenRouter

### Programming Language
- Python

---

## 📌 Features Implemented

### 1. PDF Report Extraction

Medical reports are extracted using PyPDF.

```python
from pypdf import PdfReader
```

The extracted text is consolidated across all report pages.

---

### 2. Semantic Chunking

Instead of fixed-size chunking, the report is split using domain-specific medical section headers such as:

```text
LIVER & KIDNEY PANEL, SERUM
LIPID SCREEN, SERUM
THYROID PROFILE,TOTAL, SERUM
HbA1c (GLYCOSYLATED HEMOGLOBIN), BLOOD
COMPLETE BLOOD COUNT; CBC
```

This approach preserves medical context and improves retrieval quality.

---

### 3. LangChain Document Creation

Each medical section is converted into a LangChain Document object.

Example:

```python
Document(
    page_content="HbA1c : 10.0 %",
    metadata={
        "section":"HbA1c"
    }
)
```

---

### 4. Embedding Generation

Text chunks are converted into dense vector representations using:

```text
sentence-transformers/all-MiniLM-L6-v2
```

These embeddings capture semantic meaning and enable similarity search.

---

### 5. Vector Database Indexing

Embeddings are stored inside FAISS for efficient nearest-neighbor retrieval.

```python
FAISS.from_documents(...)
```

---

### 6. Retrieval-Augmented Generation

When a user asks a question:

```text
What is my HbA1c?
```

The system:

1. Converts the query into an embedding
2. Retrieves relevant report sections
3. Injects retrieved context into the prompt
4. Sends the augmented prompt to an LLM via OpenRouter
5. Generates a final answer

Example response:

```text
Your HbA1c result is 10.0%.
```

---

## 💡 Example Queries

```text
What is my HbA1c?

Show my kidney function results.

Summarize my lipid profile.

What are my thyroid values?

List all abnormal parameters.
```

---

## 📂 Project Structure

```text
medical-rag/
│
├── reports/
│   └── sample_report.pdf
│
├── data/
│   └── extracted_text.txt
│
├── notebooks/
│   └── experimentation.ipynb
│
├── src/
│   ├── pdf_extractor.py
│   ├── chunking.py
│   ├── embeddings.py
│   ├── vector_store.py
│   ├── retriever.py
│   └── rag_pipeline.py
│
├── requirements.txt
│
└── README.md
```

---

## 🧠 Key Learnings

This project helped in understanding:

- Retrieval-Augmented Generation (RAG)
- Semantic chunking strategies
- Embedding models
- Vector databases
- Similarity search
- LangChain document abstraction
- Prompt engineering
- OpenRouter integrations
- Medical document intelligence

---

## 🔮 Future Improvements

- Multi-PDF support
- Streamlit/Flask chatbot interface
- Medical guideline knowledge base integration
- Hybrid search (Vector + Keyword Search)
- Metadata filtering
- Patient report comparison
- Clinical recommendation engine
- Multi-agent workflow using CrewAI

---

## 🎯 Outcome

Successfully developed a complete RAG pipeline capable of answering questions from pathology reports using semantic retrieval and LLM-based response generation.

The project demonstrates practical implementation of:

- LangChain
- FAISS
- Embeddings
- Prompt Engineering
- Retrieval-Augmented Generation (RAG)

and serves as a foundation for healthcare-focused AI assistants.