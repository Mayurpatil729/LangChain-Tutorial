<!-- @format -->

# 📄 Document Loaders in LangChain

## 🧐 What are Document Loaders?

Document loaders in **LangChain** are components used to **load data from various sources** into a standardized format (usually as **Document objects**). These objects are then used for **chunking, embedding, retrieval, and generation** in LangChain pipelines.

### 🚀 Why Use Document Loaders?

✅ **Standardizes different data formats** into a uniform structure.
✅ **Supports multiple sources** like text files, PDFs, web pages, and CSVs.
✅ **Prepares documents** for processing, chunking, and embedding in vector databases.

---

## 📚 Types of Document Loaders

### 1️⃣ **TextLoader** 📝

**TextLoader** is a simple and commonly used document loader in LangChain that reads **plain text (.txt) files** and converts them into LangChain **Document objects**.

🔹 **Use Case:**

- Ideal for loading **chat logs, transcripts, scanned text, code snippets**, or any **plain text data** into a LangChain pipeline.

🔹 **Limitation:**

- Works **only with .txt files** and does not support other document formats.

🔹 **Example:**

```python
from langchain.document_loaders import TextLoader

loader = TextLoader("sample.txt")
documents = loader.load()
print(documents[:2])  # Preview first two documents
```

---

### 2️⃣ **PyPDFLoader** 📄

**PyPDFLoader** is a document loader that extracts text from **PDF files**, converting each page into a **Document object**.

🔹 **How it Works:**

- Uses the **PyPDF library** to extract text from PDF documents.
- Not ideal for **scanned PDFs** or documents with **complex layouts**.

🔹 **Limitations:**

- Struggles with **images, tables, and scanned PDFs**.

🔹 **Example:**

```python
from langchain.document_loaders import PyPDFLoader

loader = PyPDFLoader("sample.pdf")
documents = loader.load()
print(documents[:2])
```

---

### 3️⃣ **DirectoryLoader** 📁

**DirectoryLoader** is a document loader that **loads multiple documents** from a **directory (folder)**.

🔹 **Features:**

- Loads **all files** in a directory.
- Supports **recursive search** through **subfolders**.
- Works with multiple file types (e.g., `.txt`, `.csv`, `.pdf`).

🔹 **Lazy Loading vs. Eager Loading:**

- **Eager Loading:** Loads **everything at once** and returns a **list of objects**.
  - Best when the **number of documents is small** and you need **everything upfront**.
- **Lazy Loading:** Fetches **documents one at a time** as needed (**streaming approach**).
  - Useful for **large datasets** to save memory.

🔹 **Example:**

```python
from langchain.document_loaders import DirectoryLoader

loader = DirectoryLoader("./documents", glob="**/*.txt", show_progress=True)
documents = loader.load()
```

---

### 4️⃣ **WebBaseLoader** 🌐

**WebBaseLoader** is used to **load and extract text** from **web pages (URLs)**.

🔹 **How it Works:**

- Uses **BeautifulSoup** to parse HTML and extract **visible text**.

🔹 **When to Use:**

- Ideal for **blogs, news articles, and public websites** with **static text**.

🔹 **Limitations:**

- Doesn’t handle **JavaScript-heavy pages** (use **SeleniumURLLoader** for that).
- Loads **only static content** (not dynamic elements rendered after page load).

🔹 **Example:**

```python
from langchain.document_loaders import WebBaseLoader

loader = WebBaseLoader("https://example.com")
documents = loader.load()
print(documents[0].page_content)
```

---

### 5️⃣ **CSVLoader** 📊

**CSVLoader** loads data from **CSV files** and converts each row into a **Document object**.

🔹 **Features:**

- Loads CSV files **row by row**, treating each row as a **separate document**.
- Works well for **structured data** like **spreadsheets, customer records, or tabular datasets**.

🔹 **Example:**

```python
from langchain.document_loaders import CSVLoader

loader = CSVLoader("data.csv")
documents = loader.load()
print(documents[:2])
```

---

## 🎯 **Conclusion**

🚀 Document loaders **bridge the gap** between raw data and AI-driven workflows in LangChain.
📂 By using **TextLoader, PyPDFLoader, DirectoryLoader, WebBaseLoader, and CSVLoader**, we can **ingest data from multiple sources** efficiently.
⚡ Choosing the right loader **depends on your use case** – whether it’s structured text, PDFs, or live web content.

---

With **LangChain document loaders**, you can **build powerful AI applications** that process data from multiple sources seamlessly! 🚀💡
