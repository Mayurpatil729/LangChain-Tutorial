
# 📌 **Chains in LangChain**  

### 🧐 **1. What and Why is Chains?**  

In **LangChain**, a **Chain** is a sequence of steps where the output of one step becomes the input of another. This helps in structuring complex LLM workflows efficiently.  

🔹 **Why use Chains?**  
✅ Simplifies multi-step reasoning.  
✅ Reduces redundant code by reusing components.  
✅ Improves modularity and debugging.  

LangChain provides different types of chains to handle various workflows. Let’s explore them!  

---

## 🔗 **2. Simple Chain**  

A **Simple Chain** consists of a **Prompt**, a **Language Model**, and an **Output Parser** connected in a sequence.  

💡 **Example:**  

```python
from langchain.prompts import PromptTemplate
from langchain.llms import OpenAI
from langchain.chains import LLMChain

# Define the prompt
prompt = PromptTemplate.from_template("What is the capital of {country}?")

# Create a simple chain
llm = OpenAI(model="gpt-4")
chain = LLMChain(prompt=prompt, llm=llm)

# Run the chain
response = chain.run({"country": "France"})
print(response)  # Output: "Paris"
```

📌 **Breakdown:**  
- Takes `country` as input.  
- Fills the template and queries the LLM.  
- Returns the model’s response.  

---

## 🔄 **3. Sequential Chain**  

A **Sequential Chain** is when multiple chains run in **series**, where the output of one chain is passed as the input to the next.  

🛠 **Use Case:** Multi-step reasoning, dialogue generation, research automation.  

💡 **Example:**  

```python
from langchain.chains import SimpleSequentialChain

# Define two chains
first_chain = LLMChain(prompt=PromptTemplate.from_template("Who is {person}?"), llm=llm)
second_chain = LLMChain(prompt=PromptTemplate.from_template("Summarize: {info}"), llm=llm)

# Create a sequential chain
chain = SimpleSequentialChain(chains=[first_chain, second_chain])

# Run the chain
result = chain.run({"person": "Elon Musk"})
print(result)
```

📌 **Flow:**  
1️⃣ First chain fetches information about *Elon Musk*.  
2️⃣ Second chain summarizes that information.  

---

## ⚡ **4. Parallel Chain**  

A **Parallel Chain** allows multiple chains to execute **simultaneously** and return results together.  

🛠 **Use Case:** Running multiple LLM queries independently.  

💡 **Example:**  

```python
from langchain.chains import RunnableParallel

# Define multiple chains
capital_chain = LLMChain(prompt=PromptTemplate.from_template("What is the capital of {country}?"), llm=llm)
language_chain = LLMChain(prompt=PromptTemplate.from_template("What language is spoken in {country}?"), llm=llm)

# Run chains in parallel
chain = RunnableParallel(capital=capital_chain, language=language_chain)
result = chain.invoke({"country": "Germany"})

print(result)  
# Output: {"capital": "Berlin", "language": "German"}
```

📌 **Flow:**  
- **Both chains execute independently** without waiting for each other.  
- Returns a **dictionary** containing results from all chains.  

---

## 🔀 **5. Conditional Chain**  

A **Conditional Chain** allows for dynamic decision-making based on inputs.  

🛠 **Use Case:** Choosing different LLMs, varying response format, conditional logic.  

💡 **Example:**  

```python
from langchain.schema import RunnableLambda
from langchain.chains import RunnableBranch

# Define conditions
def choose_chain(input):
    return "long_chain" if len(input["text"]) > 50 else "short_chain"

short_chain = LLMChain(prompt=PromptTemplate.from_template("Summarize in one sentence: {text}"), llm=llm)
long_chain = LLMChain(prompt=PromptTemplate.from_template("Write a detailed summary: {text}"), llm=llm)

# Create conditional chain
chain = RunnableBranch(
    (lambda x: len(x["text"]) > 50, long_chain),
    (lambda x: True, short_chain),  # Default case
)

# Run the chain
result = chain.invoke({"text": "The quick brown fox jumps over the lazy dog."})
print(result)
```

📌 **Flow:**  
- If the input text is long, the **long_chain** executes.  
- If short, the **short_chain** executes.  

---

## 🏗 **Understanding `chain = prompt | model | parser`**  

In **LangChain**, a chain follows a pipeline structure:  

**📌 `chain = prompt | model | parser`**  

🔹 **Prompt:** Defines how the input is structured.  
🔹 **Model:** Processes the prompt using an LLM.  
🔹 **Parser:** Parses and formats the LLM output.  

💡 **Example:**  

```python
from langchain.output_parsers import StrOutputParser

prompt = PromptTemplate.from_template("Who is {name}?")
parser = StrOutputParser()

chain = prompt | llm | parser  # Equivalent to a full chain

response = chain.invoke({"name": "Albert Einstein"})
print(response)  
```

📌 **Flow:**  
1️⃣ **Prompt** formats input.  
2️⃣ **LLM** processes the prompt.  
3️⃣ **Parser** cleans and structures the output.  

---

## 📊 **Visualizing Chain Execution with `get_graph().print_ascii()`**  

LangChain allows **visualizing** the structure of a chain using ASCII diagrams.  

💡 **Example:**  

```python
chain.get_graph().print_ascii()
```

🔍 **Output (for a sequential chain):**  

```
   (input)
      |
  LLMChain  --> LLMChain
      |
   (output)
```

📌 **Benefits:**  
✅ Helps in debugging.  
✅ Shows dependencies between chains.  
✅ Useful for complex workflows.  

---

## 🎯 **Conclusion**  

Chains in LangChain provide a **structured** and **modular** way to build LLM-powered applications.  

💡 **Key Takeaways:**  
✅ **Simple Chain** – Directly maps input → output.  
✅ **Sequential Chain** – Passes output from one chain to another.  
✅ **Parallel Chain** – Runs multiple chains simultaneously.  
✅ **Conditional Chain** – Executes chains based on conditions.  
✅ **Pipeline Model** – `prompt | model | parser`.  
✅ **Graph Visualization** – Helps debug and optimize chains.  

---

