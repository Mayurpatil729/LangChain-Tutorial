# 📘🔗 LangChain Tutorial 

LangChain is a powerful framework designed to help developers build **applications with LLMs (Large Language Models)** that are modular, composable, and production-ready.

---

## 📌 What is LangChain?

LangChain is an open-source framework built to create **context-aware, language-powered applications**. It allows you to:

* Connect to **LLMs** (like OpenAI, Cohere, etc.)
* Use **chains** to structure complex tasks
* Ingest and process **external data**
* Build **memory-enabled agents**
* Handle **tools** and **retrievers**

---

## 🧩 Key Components of LangChain

### 1. 🔗 **LLMs (Large Language Models)**

Used to generate text, answer queries, summarize, etc.

* Providers: `OpenAI`, `Cohere`, `HuggingFace`, etc.
* Example:

```python
from langchain.llms import OpenAI

llm = OpenAI(temperature=0.5)
response = llm("Tell me a joke")
```

---

### 2. 🧱 **Prompts**

Templates for interactions with LLMs.

* Types:

  * `PromptTemplate`
  * `ChatPromptTemplate`
* Example:

```python
from langchain.prompts import PromptTemplate

prompt = PromptTemplate(
    input_variables=["product"],
    template="What is a good name for a company that makes {product}?",
)
```

---

### 3. 🧠 **Chains**

Connect multiple components (prompts, LLMs, tools).

* `LLMChain`, `SequentialChain`, `SimpleSequentialChain`
* Example:

```python
from langchain.chains import LLMChain

chain = LLMChain(llm=llm, prompt=prompt)
output = chain.run("toothbrush")
```

---

### 4. 🧾 **Memory**

Add memory to chains or agents to remember previous conversations.

* Types:

  * `ConversationBufferMemory`
  * `ConversationSummaryBufferMemory`
* Example:

```python
from langchain.memory import ConversationBufferMemory

memory = ConversationBufferMemory()
```

---

### 5. 🧭 **Agents**

Agents use LLMs to choose a sequence of actions with tools.

* Example use case: Web scraping, search queries, calculator tools.
* Agent Types:

  * `ZeroShotAgent`
  * `ReAct Agent`

```python
from langchain.agents import initialize_agent, load_tools

tools = load_tools(["serpapi", "llm-math"], llm=llm)
agent = initialize_agent(tools, llm, agent="zero-shot-react-description", verbose=True)

agent.run("Who is the current Prime Minister of India?")
```

---

### 6. 🛠️ **Tools**

Tools are utilities used by agents (like calculators, search APIs).

* Example tools: `SERPAPI`, `Python REPL`, `Calculator`, `Zapier`
* Tools provide agents with extended capabilities.

---

### 7. 📚 **Retrievers**

Retrievers fetch relevant documents from a knowledge base (Vector DBs).

* Examples: FAISS, Pinecone, Chroma, Weaviate
* Useful for RAG (Retrieval Augmented Generation)

```python
from langchain.vectorstores import FAISS
from langchain.embeddings.openai import OpenAIEmbeddings

embedding = OpenAIEmbeddings()
vectorstore = FAISS.load_local("index", embedding)
```

---

### 8. 📄 **Document Loaders**

Helps load data from different sources (PDFs, URLs, Notion, etc.)

```python
from langchain.document_loaders import PyPDFLoader

loader = PyPDFLoader("my_resume.pdf")
documents = loader.load()
```

---

### 9. 🧪 **Evaluation**

Tools to evaluate the performance of LLM chains or agents.

* Compare responses with ground truth
* LangSmith (optional monitoring and testing suite)

---

## 🔧 Building a LangChain App (Step-by-Step)

### Step 1: Install LangChain

```bash
pip install langchain openai
```

### Step 2: Setup LLM

```python
from langchain.llms import OpenAI
llm = OpenAI(api_key="YOUR_API_KEY", temperature=0.7)
```

### Step 3: Create Prompt

```python
from langchain.prompts import PromptTemplate

prompt = PromptTemplate(
    input_variables=["topic"],
    template="Write a poem about {topic}."
)
```

### Step 4: Run Chain

```python
from langchain.chains import LLMChain

chain = LLMChain(llm=llm, prompt=prompt)
output = chain.run("sunset")
print(output)
```

---

## 📦 Advanced Topics

### 🧠 Memory in Chains

Add memory to hold conversation state:

```python
from langchain.chains import ConversationChain
from langchain.memory import ConversationBufferMemory

conversation = ConversationChain(llm=llm, memory=ConversationBufferMemory())
conversation.run("Hello!")
conversation.run("What's my name?")
```

---

### 🤖 Creating Agents with Tools

```python
from langchain.agents import initialize_agent, load_tools

tools = load_tools(["serpapi", "llm-math"], llm=llm)
agent = initialize_agent(tools, llm, agent="zero-shot-react-description", verbose=True)
agent.run("How many people live in Mumbai?")
```

---

### 📖 Using LangChain with VectorDB (RAG)

```python
from langchain.vectorstores import FAISS
from langchain.text_splitter import CharacterTextSplitter
from langchain.embeddings.openai import OpenAIEmbeddings

text_splitter = CharacterTextSplitter(chunk_size=1000, chunk_overlap=100)
texts = text_splitter.split_documents(documents)
vectorstore = FAISS.from_documents(texts, OpenAIEmbeddings())

retriever = vectorstore.as_retriever()
```

---

## 🛡️ LangChain Ecosystem

* **LangSmith** – for debugging, monitoring, and evaluating chains/agents
* **LangServe** – for turning LangChain apps into production APIs
* **LangGraph** – build agent workflows using graphs

---

## 🔚 Conclusion

LangChain helps you build intelligent applications by chaining together LLMs, prompts, memory, and tools. Whether you're building a chatbot, knowledge assistant, or agent, LangChain provides a powerful abstraction for modular AI applications.

---
