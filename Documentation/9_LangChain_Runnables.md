# 🏗️ Runnables in Chains

## 🔹 What Are Runnables?
Runnables are modular and reusable components used in chains that execute specific tasks in a structured workflow. They act as **building blocks** in a pipeline, where each runnable performs a function and passes data to the next step.

---
## 🔹 Why Do Runnables Exist? 🤔
Runnables exist to provide a **structured and efficient** way to build AI workflows. Instead of manually coding logic for sequential or parallel execution, runnables allow for:
- **Modular composition** 🏗️ (breaking down complex workflows into smaller units)
- **Reusability** 🔄 (reuse existing components without rewriting code)
- **Scalability** 📈 (support for sequential, parallel, and conditional execution)
- **Flexibility** ⚙️ (custom workflows using simple primitives)

---

# 🏷️ Types of Runnables

## 1️⃣ **Task-Specific Runnables** 🎯
These are runnables designed for specific tasks, such as:
- **Text Processing** 📝 (Summarization, Translation, Tokenization)
- **Data Fetching** 🌐 (Fetching APIs, Database Queries)
- **AI Model Execution** 🤖 (Calling an LLM for text generation)

**Example:**
```python
from langchain.schema.runnable import Runnable

def fetch_data(url):
    return requests.get(url).json()

fetch_runnable = Runnable(fetch_data)
```

---

## 2️⃣ **Runnable Primitives** 🏗️
Runnable Primitives are fundamental building blocks that handle various execution patterns.

### 📌 **1. RunnableSequence** 🏁
A `RunnableSequence` executes multiple runnables **sequentially**, where the output of one step is the input for the next. It is useful for **structured workflows**.

🔹 **Use Case:** A pipeline where a document is fetched, summarized, and then translated.

**Example:**
```python
from langchain.schema.runnable import RunnableSequence

pipeline = RunnableSequence(fetch_runnable, summarize_runnable, translate_runnable)
result = pipeline.invoke("https://example.com/article")
```

---

### 📌 **2. RunnableParallel** 🔀
A `RunnableParallel` runs multiple runnables **simultaneously**, each receiving the same input but processing it independently.

🔹 **Use Case:** Running **sentiment analysis, keyword extraction, and summarization** in parallel.

**Example:**
```python
from langchain.schema.runnable import RunnableParallel

parallel_pipeline = RunnableParallel(
    sentiment=sentiment_runnable,
    keywords=keyword_runnable,
    summary=summarization_runnable
)

results = parallel_pipeline.invoke("This is a great product! Highly recommended.")
```
📌 Output: `{ 'sentiment': 'Positive', 'keywords': ['great product'], 'summary': 'Highly recommended' }`

---

### 📌 **3. RunnablePassthrough** 🔄
A `RunnablePassthrough` **returns the input as output** without any modification. It is mainly used for debugging or as a placeholder.

🔹 **Use Case:** When a step is optional, but you still want to maintain the pipeline structure.

**Example:**
```python
from langchain.schema.runnable import RunnablePassthrough

passthrough = RunnablePassthrough()
output = passthrough.invoke("Hello, World!")  # Output: "Hello, World!"
```

---

### 📌 **4. RunnableLambda** 🔣
A `RunnableLambda` allows defining **custom logic** as a lambda function, making it easy to perform inline transformations.

🔹 **Use Case:** Applying **custom processing** without creating a separate function.

**Example:**
```python
from langchain.schema.runnable import RunnableLambda

uppercase_runnable = RunnableLambda(lambda x: x.upper())
output = uppercase_runnable.invoke("hello")  # Output: "HELLO"
```

---

### 📌 **5. RunnableBranch** 🌿
A `RunnableBranch` executes different runnables **based on conditions**.

🔹 **Use Case:** Running different workflows for different types of inputs.

**Example:**
```python
from langchain.schema.runnable import RunnableBranch

def is_question(text):
    return text.endswith("?")

branch = RunnableBranch(
    (is_question, qa_runnable),
    default_runnable
)

output = branch.invoke("What is AI?")  # Runs qa_runnable
```

---

# 🚀 **Why Use Runnables?**
✅ **Modularity** – Break down workflows into reusable units
✅ **Parallel & Sequential Execution** – Handle different types of workflows efficiently
✅ **Flexibility** – Combine different primitives to create complex pipelines
✅ **Scalability** – Run workflows for AI applications, automation, and data processing

By using Runnables, developers can build **robust**, **scalable**, and **efficient** AI-powered applications! 🚀🔥



