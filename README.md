# bm25_retriever

`bm25_retriever` is a persistent BM25 retriever for use with LangChain, built on top of `rank_bm25`.

## Features

- Save and load BM25 retriever to/from disk
- Easily integrate with LangChain `Document` format
- Simple API for creating, persisting, and querying retrievers

## Installation

```bash
pip install bm25_retriever
```

## Usage
```python
from langchain_core.documents import Document
from bm25_retriever.retriever import PersistentBM25Retriever

# Sample documents
docs = [
    Document(page_content="The quick brown fox jumps over the lazy dog"),
    Document(page_content="A fox fled from danger"),
    Document(page_content="Dogs are loyal companions"),
    Document(page_content="Foxes are cunning and agile"),
]

# Step 1: Create a retriever with a specified save directory
save_directory = "bm25_storage"
retriever = PersistentBM25Retriever(documents=docs, save_dir=save_directory, persist=True)
# Step 2: Persist the retriever to the specified directory
# retriever.persist()

# Step 3: Load the retriever from the directory with a custom k value
loaded_retriever = PersistentBM25Retriever.from_persist_dir(save_dir=save_directory, k=3)

# Step 4: Use the loaded retriever to retrieve documents
query = "fox"
results = loaded_retriever.get_relevant_documents(query)

# Print the retrieved documents
print(f"Retrieved {len(results)} documents for query '{query}':")
for i, doc in enumerate(results, 1):
    print(f"{i}. {doc.page_content}")
```
