# RAG-AISafety

[![Python Versions](https://img.shields.io/badge/python-3.10%20%7C%203.11%20%7C%203.12-blue)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-red.svg)](https://opensource.org/licenses/MIT)

<div align="center">
	<img src="https://github.com/JuaniAlvarezC/RAG-AISafety/blob/main/images/AISafety.jpg" width="500" height="330">
</div>

## Overview

This project demonstrates a Retrieval‑Augmented Generation (RAG) pipeline that ingests content from a public Notion page and enables context‑aware question answering using the OpenAI ChatGPT API.

Source Notion Page:
https://jalvarezc.notion.site/AIS-5b9ffa2c525f481ea08ed801d8ef7896

## Data Ingestion

1. Notion API (notion-client)
   - Authenticate with an internal integration token
   - Fetch the target page and all sub‑pages recursively via client.blocks.children.list
   - Convert each page into a LangChain Document

2. Chunking
   - Use RecursiveCharacterTextSplitter (chunk size 1024, overlap 100)
   - Preserve start indices for traceability

3. Embedding & Storage
   - Generate embeddings with FastEmbedEmbeddings
   - Persist chunks in a Chroma vector store (langchain-chroma)

Key ingestion function: ingest_notion_page(integration_token, page_id, persist_dir)

## RAG Pipeline

1. Model
   - ChatOpenAI from langchain-openai (e.g. gpt-3.5-turbo)

2. Retriever
   - Chroma vector store as retriever (search type similarity, top‑k=3)

3. Chain
   - Prompt template with instructions and context placeholders
   - Document chain via create_stuff_documents_chain
   - Retrieval chain assembled with create_retrieval_chain

Key chain function: rag_chain_openai(db_path)

## Technologies

- Python 3.8+

- Notion API (notion-client)

- LangChain

- langchain-openai

- langchain-chroma

- ChromaDB

- FastEmbedEmbeddings

## License

This project is released under an MIT license.
