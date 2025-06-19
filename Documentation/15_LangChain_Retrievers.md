<!-- @format -->

### **Retrievers in LangChain** 🧑‍💻

A **retriever** is a component in LangChain that fetches relevant documents or information from a data source based on a user's query. Retrievers are essential for improving the effectiveness of **search engines** and **question-answering systems**. They help retrieve the most relevant content from vast data sources, often using semantic search or other advanced algorithms.

---

### **Types of Retrievers** 🔍

#### 1. **Wikipedia Retriever** 📚

- **Definition**: A retriever that queries the **Wikipedia API** to fetch relevant content for a given query.
- **How It Works**:

  1. The user enters a query (e.g., "Albert Einstein").
  2. The retriever sends the query to the **Wikipedia API**.
  3. It retrieves the most relevant Wikipedia articles related to the query.
  4. The content is returned as **LangChain objects** for further processing.

  **Use Case**: This is useful when you need to fetch general information from Wikipedia based on user queries.

---

#### 2. **Vector Store Retriever** 🧠

- **Definition**: A retriever that fetches documents from a **vector store** using **semantic similarity** based on vector embeddings.
- **How It Works**:

  1. Documents are stored in a **vector store** (e.g., FAISS, Pinecone).
  2. Each document is represented as a **vector** (embedding).
  3. When the user enters a query, it is also **converted into a vector**.
  4. The retriever compares the query vector with the stored vectors to find the **most similar** documents.

  **Use Case**: Used for **semantic search**, where the query is matched with documents that have similar meanings, even if the exact words don’t match.

---

#### 3. **Maximal Marginal Relevance (MMR) Retriever** 🔄

- **Definition**: A retrieval algorithm designed to reduce redundancy in search results while ensuring high relevance to the query.
- **How It Works**:

  1. MMR tries to select documents that are relevant to the query but **diverse** in content, avoiding repetition.
  2. It balances **relevance** and **diversity** by considering documents that are both relevant and different from others.

  **Why Use MMR Retriever?**:

  - In a typical similarity search, retrieved documents may be **too similar** to each other, repeating the same information.
  - MMR avoids this by picking documents that provide **diverse perspectives** while maintaining **relevance**.

  **Use Case**: Particularly useful in **RAG (Retrieval-Augmented Generation)** pipelines, where the context window should contain **relevant but diverse** information.

---

#### 4. **Multi-Query Retriever** 🔀

- **Definition**: A retriever that allows querying with **multiple queries** simultaneously, returning results for all queries.
- **How It Works**:

  1. Instead of a single query, the system can handle **multiple queries** in parallel.
  2. Each query can be processed independently or collectively to return relevant results for all.

  **Use Case**: This is useful in cases where **multiple aspects** of a query need to be explored, or when a user provides **complex multi-part queries**.

---

### **Key Points to Remember** 📝:

- **Retriever**: A component that fetches relevant documents based on a query.
- **Wikipedia Retriever**: Queries Wikipedia for content related to a query.
- **Vector Store Retriever**: Fetches documents based on **semantic similarity** using vectors.
- **MMR Retriever**: Reduces redundancy and increases **diversity** of results while maintaining relevance.
- **Multi-Query Retriever**: Handles multiple queries at once to return results for each.

---

### **Contextual Compression Retriever** 🔄

- **Definition**: An advanced retriever in LangChain that improves retrieval quality by **compressing** documents after retrieval, keeping only the **relevant content** based on the user's query.
- **How It Works**:

  1. Retrieves the relevant documents based on the query.
  2. Compresses the documents to remove irrelevant or redundant information.
  3. Only the **contextually relevant** content remains for further processing.

  **Use Case**: Ideal for improving efficiency and relevance in retrieval systems by **filtering out unnecessary details** from the documents.

---

### **BM25Retriever** 📏

- **Definition**: A retriever that uses the **BM25** ranking function, a probabilistic model, to retrieve documents based on **term frequency** and **inverse document frequency (TF-IDF)**.
- **How It Works**:

  1. BM25 ranks documents by how well the terms in the query match the terms in the document.
  2. It uses factors like **term frequency** (how often a word appears) and **document frequency** (how common a word is across documents).

  **Use Case**: Often used for traditional **keyword-based search** in information retrieval systems.

---

### **MultiVectorRetriever** 🔀

- **Definition**: A retriever that combines multiple vector representations (embeddings) of documents to improve retrieval quality by using **different types of embeddings**.
- **How It Works**:

  1. Combines multiple vector embeddings, allowing for a richer representation of the documents.
  2. Retrieves documents by considering several vectors to make the search more **comprehensive**.

  **Use Case**: Useful when documents need to be represented from different perspectives, improving the overall **retrieval accuracy**.

---

### **ParentDocumentRetriever** 🧳

- **Definition**: A retriever designed to retrieve documents based on a **parent-child relationship**. It focuses on fetching documents related to a main or parent document.
- **How It Works**:

  1. Retrieves the **parent document** first.
  2. Then, fetches **child documents** that are directly or indirectly related to the parent.

  **Use Case**: Ideal when dealing with structured documents that have hierarchical relationships, such as **articles with sub-sections** or **research papers with references**.

---

### **EnsembleRetriever** 🏗️

- **Definition**: A retriever that combines the outputs of multiple other retrievers to provide a **combined result**.
- **How It Works**:

  1. It integrates multiple retrievers (e.g., BM25, Vector Store) and merges the results.
  2. It uses different retrieval techniques to ensure **diverse and accurate results**.

  **Use Case**: Ideal for complex systems where multiple types of queries need to be handled using various retrieval methods.

---

### **LangChain Official Documentation - Retrievers** 📜

For detailed information on all the retrievers in LangChain, you can check the **official LangChain documentation** on retrievers:

👉 [LangChain Retrievers Documentation](https://langchain.readthedocs.io/en/latest/modules/retrievers.html)

---
