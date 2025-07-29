# Text_to_SQL_1

Natural Language to SQL Generator with RAG and SQLCoder
This project enables users to ask natural language questions and receive accurate SQL queries using a Retrieval-Augmented Generation (RAG) approach. It combines sentence embeddings, FAISS indexing for schema retrieval, and a fine-tuned large language model (sqlcoder-7b-2) for SQL generation.

# Features

Embedding-based retrieval of relevant schema chunks

Vector search using FAISS for contextual grounding

Instruction-tuned SQL generation using the SQLCoder model

Multi-difficulty question management (Very Easy to Toughest)

Extensible schema definition and querying logic

# Components

Schema Preparation: Define tables and columns in a structured format

Embedding Model: Uses all-MiniLM-L6-v2 from SentenceTransformers to vectorize schema

Vector Indexing: Leverages FAISS for similarity search on schema chunks

Prompt Engineering: Dynamically constructs SQL prompts using [INST]...[/INST] format

LLM Inference: Uses Hugging Face Transformers pipeline with defog/sqlcoder-7b-2 for generating SQL

# Workflow

Prepare schema chunks as text blocks

Encode schema using a sentence embedding model

Index vectors using FAISS

Accept user question as natural language

Retrieve top-k relevant schema pieces

Construct SQL-specific prompt with [INST] wrapper

Pass prompt to local or remote SQLCoder model

Display the SQL query as output

# Requirements

Hugging Face Transformers

SentenceTransformers

FAISS (CPU or GPU)

PyTorch

A downloaded or accessible copy of the SQLCoder model

Example Use Case
Ask: “Show top 3 product categories by revenue in 2024 with at least 5 unique customers per category.”

The model will return a SQL query using the relevant schema, such as joining orders, order_items, and products with appropriate filters and aggregations.

# Future Enhancements

UI integration for interactive querying

Support for custom database dialects (PostgreSQL, MySQL, etc.)

Schema extraction from live DBs or DDL scripts

SQL execution and result rendering

Question:
how many customers have same first name?

Return only the SQL query. [/INST] SELECT c.name, COUNT(c.customer_id) AS COUNT FROM customers c WHERE c.name ilike 'John%' GROUP BY c.name HAVING COUNT(c.customer_id) > 1 ORDER BY COUNT DESC NULLS LAST;
