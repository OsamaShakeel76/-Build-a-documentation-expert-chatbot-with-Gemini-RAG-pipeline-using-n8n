# 🤖 Build a Documentation Expert Chatbot with Gemini RAG Pipeline (n8n)

This project implements a **documentation expert AI chatbot** using a **Gemini-powered Retrieval-Augmented Generation (RAG) pipeline**, fully orchestrated with **n8n**.  
The chatbot is designed to answer user questions **accurately and reliably** using **only official documentation**, eliminating hallucinations and unsupported answers.

---

## 🔍 What This Project Does

- Crawls and indexes official documentation (e.g., n8n docs)
- Cleans, chunks, and embeds documentation using **Google Gemini embeddings**
- Stores embeddings in an **in-memory vector store**
- Exposes a **chat interface** where users can ask questions
- Retrieves relevant documentation chunks and generates **grounded answers**
- Enforces **strict RAG rules**: answers are based *only* on retrieved content

---

## 🧠 Architecture Overview

### Two-Part RAG Workflow

#### 1️⃣ Indexing Flow (Run Once)
Builds the knowledge base:
- Fetches all documentation links
- Extracts and cleans page content
- Splits text into overlapping chunks
- Generates embeddings using **Gemini**
- Stores vectors in an **in-memory vector store**

> ⚠️ Note: The vector store is **not persistent**. If n8n restarts, indexing must be re-run.

#### 2️⃣ Chat Flow (Live)
Handles user interaction:
- Accepts user queries via a public chat URL
- Converts the query into embeddings
- Retrieves relevant documentation chunks
- Uses **Gemini 2.5 Flash** to synthesize a response
- Returns a clear, factual, documentation-backed answer

---

## 🛠 Key Technologies

- **n8n** – Workflow orchestration
- **Google Gemini 2.5 Flash** – LLM for chat + embeddings
- **RAG (Retrieval-Augmented Generation)** – Grounded QA
- **In-Memory Vector Store** – Fast semantic search
- **LangChain nodes (n8n-native)** – Agent, memory, embeddings

---

## 🧩 Core Components

- **Documentation Scraper** – Collects all doc pages
- **Text Cleaner & Splitter** – Prepares data for embedding
- **Vector Store (In-Memory)** – Stores embeddings
- **RAG AI Agent** – Enforces strict documentation-only answers
- **Chat Trigger (Public URL)** – User-facing interface
- **Conversation Memory** – Enables follow-up questions

---

## 🚀 Setup Instructions

### Step 1: Configure Google Gemini Credentials
1. Open any Gemini node (Chat or Embeddings)
2. Create a new **Google AI credential**
3. Paste your **Google AI API Key**
4. Apply it to all Gemini nodes

### Step 2: Build the Knowledge Base
1. Locate the **Start Indexing** manual trigger
2. Click **Execute Workflow**
3. Wait ~15–20 minutes for indexing to complete

### Step 3: Activate the Chatbot
1. Activate the workflow
2. Open the **RAG Chatbot** node
3. Use:
   - **Open Chat** (inside n8n), or
   - **Public URL** (external chat interface)

---

## 💬 Example Questions

- *How does the IF node work in n8n?*
- *What is a sub-workflow?*
- *How does error handling work in n8n?*

---

## ✅ Design Principles

- ❌ No hallucinations
- 📚 Documentation as the **single source of truth**
- 🔍 Semantic search for precision
- 🧠 Memory-aware conversations
- ⚡ Fast inference with Gemini Flash

---

## 📌 Limitations

- Vector store is **session-based**
- Requires re-indexing after n8n restart
- Not intended for real-time document updates without re-run


