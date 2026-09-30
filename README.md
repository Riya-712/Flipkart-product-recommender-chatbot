# 🛒 Flipkart Product Recommender Chatbot

[Demo](http://localhost:8501)

A **Retrieval-Augmented Generation (RAG) based product recommendation chatbot** that helps users discover products using natural-language queries.

The application retrieves relevant product reviews from a **Qdrant vector database** using semantic similarity and provides context-grounded recommendations through a **Groq-hosted LLM**. The chatbot interface is built with **Streamlit**.

---

## 📌 Project Overview

Traditional product search relies heavily on keywords and exact matches. This project uses **semantic search + RAG** to understand the meaning behind a user's query and retrieve relevant product reviews.

For example, instead of searching for an exact product name, a user can ask:

> "I need a Bluetooth headset with good bass and long battery life."

The system:

1. Understands the user's query.
2. Converts the query into an embedding.
3. Searches the Qdrant vector database for semantically similar reviews.
4. Retrieves relevant product-review context.
5. Passes the retrieved context to the LLM.
6. Generates a natural-language product recommendation.
7. Displays the response through the Streamlit chatbot interface.

---

## 🎯 Objectives

* Build a conversational product recommendation system.
* Implement a complete **RAG pipeline** using LangChain.
* Use semantic search instead of keyword-only product matching.
* Store and retrieve product-review embeddings using Qdrant.
* Generate recommendations grounded in retrieved review information.
* Support conversational follow-up questions.
* Build an interactive web interface using Streamlit.

---

## 🏗️ System Architecture

```text
                         ┌──────────────────────┐
                         │        User          │
                         │  Natural Language    │
                         │       Query          │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │      Streamlit       │
                         │      Frontend        │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │    LangChain RAG     │
                         │       Pipeline       │
                         └──────────┬───────────┘
                                    │
                                    ▼
                     ┌─────────────────────────────┐
                     │     Query Embedding         │
                     │ BAAI/bge-base-en-v1.5       │
                     └──────────────┬──────────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │       Qdrant         │
                         │    Vector Database   │
                         │                      │
                         │ Product Reviews      │
                         │ 768-Dimensional      │
                         │ Vectors              │
                         └──────────┬───────────┘
                                    │
                              Top-K Reviews
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │      Groq LLM        │
                         │    GPT-OSS 120B      │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │ Product Recommendation│
                         │       Response       │
                         └──────────────────────┘
```

---

# 🛠️ Tech Stack

| Category               | Technology            |
| ---------------------- | --------------------- |
| Programming Language   | Python                |
| LLM Framework          | LangChain             |
| LLM Provider           | Groq                  |
| LLM                    | GPT-OSS 120B          |
| Embeddings             | BAAI/bge-base-en-v1.5 |
| Vector Database        | Qdrant                |
| Frontend               | Streamlit             |
| Data Processing        | Pandas                |
| Environment Management | python-dotenv         |
| Version Control        | Git / GitHub          |

---

# 🗄️ Qdrant Setup

Create a Qdrant Cloud collection named:

```text
flipkart_database
```

The application uses:

```text
Embedding Model:
BAAI/bge-base-en-v1.5

Vector Dimension:
768

Distance:
Cosine
```

---

# 📥 Data Ingestion

Run:

```powershell
python ingest_data.py
```

The ingestion pipeline:

```text
Flipkart CSV
     ↓
Data Converter
     ↓
LangChain Documents
     ↓
BGE Embeddings
     ↓
Qdrant
```

After successful ingestion, the Qdrant collection contains the product-review vectors used by the chatbot.

---

# 🔍 Key Features

### Semantic Product Search

Understands the semantic meaning of a query rather than relying only on exact keywords.

### Review-Based Recommendations

Recommendations are generated using retrieved product-review information.

### Vector Search

Qdrant enables similarity-based retrieval over product reviews.

### Conversational Interaction

Users can ask follow-up questions while maintaining conversational context.

### RAG Architecture

The application combines retrieval with LLM generation to provide context-grounded responses.

### Interactive UI

Streamlit provides a simple conversational interface for interacting with the recommendation system.

---

# 📌 Limitations

The current system primarily relies on product-review text and product-name metadata.

Therefore, recommendations should be interpreted as **review-based recommendations**, rather than a complete e-commerce recommendation engine.

The system does not currently model:

* Real-time inventory
* Current product prices
* User purchase history
* User clickstream behavior
* Collaborative filtering
* Personalized user profiles

---


