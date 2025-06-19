<!-- @format -->

# **LangChain Notes - Models **

## 1️⃣ **Understanding LangChain Models**

LangChain provides an easy way to interact with various **LLMs (Large Language Models)** like OpenAI, Hugging Face, Cohere, and others. It abstracts the model interaction and allows seamless integration into applications.

```
The Model Component in LangChain is a crucial part of the framework. designed to facilitate interactions with various language models and embedding models.
abstracts the complexity of working directly with different LLMS, chat models. and embedding models. providing a uniform interface to communicate with them. This makes it easier to build applications that rely on Al-generated text. text embeddings for similarity search, and retrieval-augmented generation (RAG).
```

### 🔹 Types of Models in LangChain:

1. **LLMs (Large Language Models):**

   - Example: OpenAI (`gpt-4`), Cohere, Hugging Face
   - Used for text generation, summarization, and reasoning.

2. **Chat Models:**

   - Example: `ChatOpenAI`, `ChatAnthropic`
   - Designed for chatbot-like interactions with structured inputs and outputs.

3. **Embedding Models:**
   - Example: `OpenAIEmbeddings`, `HuggingFaceEmbeddings`
   - Convert text into numerical vectors for search, similarity, and retrieval tasks.

---

## 2️⃣ **Setting Up API Keys for Models**

Since LangChain interacts with external LLM providers, API keys are required for authentication.

### 🔹 **How to Use API Keys?**

Most providers require you to set the API key in an environment variable or pass it in the model initialization.

#### ✅ **Method 1: Using Environment Variables**

- Store the API key in `.env` file:
  ```plaintext
  OPENAI_API_KEY="your_api_key_here"
  ```
- Load it in your Python script:

  ```python
  import os
  from dotenv import load_dotenv

  load_dotenv()
  openai_api_key = os.getenv("OPENAI_API_KEY")
  ```

#### ✅ **Method 2: Passing API Key Directly**

```python
from langchain.llms import OpenAI

llm = OpenAI(model_name="gpt-3.5-turbo", openai_api_key="your_api_key_here")
```

#### ✅ **Method 3: Using LangChain Configuration**

You can also set API keys in LangChain’s configuration:

```python
from langchain.chat_models import ChatOpenAI

llm = ChatOpenAI(model_name="gpt-4")
```

Ensure `OPENAI_API_KEY` is set as an environment variable.

---

## 3️⃣ **How to Organize LangChain Models in a Project?**

To keep your project structured, follow these best practices:

### 📁 **Project Structure**

```
/langchain_project
│── /config
│   ├── config.py  # Store model configurations
│   ├── .env       # Store API keys securely
│
│── /models
│   ├── llm.py     # Functions to initialize LLM models
│   ├── embeddings.py  # Functions to initialize embedding models
│
│── main.py        # Main script to run LangChain pipeline
│── requirements.txt  # Dependencies
```

### 🔹 **Example: `config.py` (Centralized Model Configuration)**

```python
import os
from dotenv import load_dotenv

load_dotenv()

OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")
MODEL_NAME = "gpt-4"
```

### 🔹 **Example: `llm.py` (Initializing LLM Model)**

```python
from langchain.chat_models import ChatOpenAI
from config import OPENAI_API_KEY, MODEL_NAME

def get_llm():
    return ChatOpenAI(model_name=MODEL_NAME, openai_api_key=OPENAI_API_KEY)

# Test
if __name__ == "__main__":
    llm = get_llm()
    print(llm.invoke("Explain LangChain in simple terms."))
```

---

## 4️⃣ **How to Check If the Model Is Working?**

### ✅ **Basic Test**

Run a simple test script:

```python
llm = get_llm()
response = llm.invoke("What is LangChain?")
print(response)
```

### ✅ **Check API Key Setup**

If an API key issue occurs, verify:

```python
import os
print("OpenAI API Key:", os.getenv("OPENAI_API_KEY"))
```

### ✅ **Debugging Errors**

Common errors:

- **Invalid API key:** Check if the key is correctly loaded.
- **Rate limits:** Some providers limit API requests; check your account.
- **Network issues:** Ensure internet connectivity.

---

## 🔥 **Conclusion**

- LangChain models allow easy interaction with LLMs.
- API keys should be securely stored in environment variables.
- Organizing code into `config.py`, `llm.py`, and structured folders improves maintainability.
- Simple function calls can test whether the model is working.

---

Here’s a **detailed breakdown** of how **Embedding Models, Semantic Search, Vector Databases, and Cosine Similarity** work together:

---

## **📌 Embedding Models, Semantic Search, Vector Databases & Cosine Similarity**

## **1️⃣ What are Embedding Models?**

Embedding models convert text, images, or data into numerical representations called **vectors**. These vectors capture the semantic meaning of the input, allowing computers to understand relationships between different pieces of information.

### 🔹 How Embeddings Work:

1. **Tokenization** – Text is broken into words/subwords.
2. **Encoding** – Each token is mapped to a numerical space.
3. **Vector Representation** – The model assigns a high-dimensional vector (e.g., 768 or 1024 dimensions) to each input.
4. **Storage & Retrieval** – These vectors are stored in a **vector database** for similarity-based search.

### 🔹 Popular Embedding Models:

- OpenAI's **text-embedding-ada-002**
- Sentence Transformers (**BERT, SBERT, T5**)
- **Hugging Face** Transformer Models
- **FastText, Word2Vec, GloVe** (older models)

---

## **2️⃣ Semantic Search & How It Works**

Semantic search improves traditional keyword-based search by **understanding meaning and intent** instead of relying on exact word matches.

### 🔹 Steps in Semantic Search:

1. **Convert the Query into an Embedding** – When a user searches, the query is converted into a vector.
2. **Retrieve Similar Vectors** – The system searches for **nearest** vectors from a database.
3. **Rank the Results** – Uses similarity measures (like **cosine similarity**) to return the most relevant results.

> **Example:** Searching for _"best places to eat pizza"_ will also return results like _"top-rated Italian restaurants"_, even if the exact words don’t match.

---

## **3️⃣ Vector Databases**

Vector databases store and efficiently retrieve **high-dimensional embeddings**.

### 🔹 How a Vector Database Works:

- **Indexing** – Stores embeddings in a structured format.
- **Nearest Neighbor Search (KNN, ANN)** – Finds the closest vectors to a given query.
- **Scalability** – Designed to handle **millions** of embeddings efficiently.

### 🔹 Popular Vector Databases:

- **FAISS** (Facebook AI Similarity Search)
- **Pinecone**
- **Weaviate**
- **ChromaDB**
- **Milvus**

---

### **4️⃣ Cosine Similarity – Measuring Similarity**

Cosine similarity measures how **close** two vectors are in **semantic meaning**.

### 🔹 Cosine Similarity Formula:

\[
\text{Similarity} = \frac{A \cdot B}{||A|| \times ||B||}
\]
Where:

- **A** and **B** are vectors.
- **||A||** and **||B||** are magnitudes (lengths) of the vectors.
- **Dot product** measures their directional similarity.

> **Example Calculation:**  
> Two vectors **A (0.8, 0.6)** and **B (0.9, 0.4)**  
> \[
> \cos(\theta) = \frac{(0.8 \times 0.9) + (0.6 \times 0.4)}{\sqrt{(0.8^2 + 0.6^2)} \times \sqrt{(0.9^2 + 0.4^2)}}
> \]
> A similarity score close to **1** means high relevance.

### 🔹 Why Use Cosine Similarity?

- Ignores magnitude differences (only considers direction).
- Works well with **high-dimensional** vectors.

---

### **🔗 How It All Works Together**

1. **User Inputs a Query** – e.g., "AI in healthcare"
2. **Query is Converted into an Embedding** using an embedding model.
3. **Vector Search Performed** in a **vector database**.
4. **Cosine Similarity Used** to rank results.
5. **Most Relevant Results** are returned.

> **Real-World Example:**

- Google Search
- Chatbot Knowledge Retrieval
- AI-Powered Recommendations (e.g., Netflix, Spotify)

---

# **🚀 Summary**

✔ **Embedding Models** → Convert text into vectors.  
✔ **Semantic Search** → Finds meaning-based matches.  
✔ **Vector Databases** → Store & retrieve embeddings.  
✔ **Cosine Similarity** → Measures how close two vectors are.

---
