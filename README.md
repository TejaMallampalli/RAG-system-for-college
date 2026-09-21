# RAG - Retrieval Augmented Generation

A production-ready RAG system to answer questions from your own documents without LLM hallucination.

## What is RAG?

LLMs don't know your private data. RAG solves this by storing your documents in a Vector Database and retrieving relevant context at query time to feed to the LLM.

## Why RAG over Fine-Tuning?No Hallucination 
 - Answers from your docs only Up-to-date
 - Just re-ingest new docs Sources
 - Shows where answer came from cheaper
 - No need to retrain model

**Formula: LLM + Your Data = Accurate & Grounded Answer**

## Architecture
-> Ingestion Pipeline -> Vector DB -> User Query -> Retrieval Pipeline -> LLM -> Answer with Sources


### 1. Ingestion Pipeline
The process of getting data into the Vector DB.

1. **Load:** Load data from PDFs, DOCX, TXT, CSV, Websites.
2. **Chunking:** Split large docs into smaller chunks (e.g., 500 tokens with 50 token overlap) - LLMs have limited context.
3. **Embedding:** Convert each chunk into a vector (numerical representation) using an embedding model.
4. **Store:** Save vectors + metadata into Vector DB.

**Flow: Load -> Chunk -> Embed -> Store**

### 2. Retrieval Pipeline
The process of answering a user query.

1. **Query Embedding:** Convert user question into a vector.
2. **Similarity Search:** Search Vector DB for Top-K most similar chunks (cosine similarity).
3. **Re-ranking (Optional):** Use Cross-Encoder to re-rank and filter best chunks.
4. **Generation:** Send retrieved chunks + user query to LLM to generate final answer.

**Flow: Query -> Embed -> Search -> Re-rank -> Generate**


- **Orchestration:** LangChain
- **Embedding Model:** RecursiveCharacterTextSplitter
- **Vector DB:** ChromaDB
- **LLM:** Llama 3
- **Backend:** Python
