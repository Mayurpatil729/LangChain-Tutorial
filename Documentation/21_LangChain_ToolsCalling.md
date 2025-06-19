
# 🛠️ LangChain — Detailed Notes on Tools

---

## 🌟 What is a Tool in LangChain?

- A **Tool** in LangChain is **simply a Python function or method**, packaged so that a Language Model (LLM) can:
  - **Recognize** it,
  - **Understand** its purpose,
  - **Call** it when necessary during task execution.
  
- A Tool acts as the **"hands"** of the LLM — enabling it to **interact with the external world**: APIs, databases, systems, files, etc.

---

## ⚡ Common Built-in Tools

| Tool Name | Purpose | Example |
|:---|:---|:---|
| 🔎 DuckDuckGo Tool | Perform web search queries. | "Find today's news headlines." |
| 💻 Shell Tool | Execute commands in the system shell. | "List all files in a directory (`ls`)." |
| 🔗 API Tool | Access external APIs and fetch data. | "Get weather info from OpenWeather API." |
| 🗄️ Database Tool | Query or update a database. | "Fetch user data from SQL database." |

---

# 🔥 Core Concepts: Tool Lifecycle

---

## 🔗 1. Tool Binding

**Tool Binding** = **Introducing tools to the LLM and registering them properly**.

✅ **Why is Binding Needed?**
- So that the LLM **knows what tools exist**.
- So it **understands** how and when to use them.
- So it **knows** the **required input format** for each tool.

✅ **Tool Binding Involves**:
1. **Tool Name** 🏷️ — Unique identifier for the tool.
2. **Tool Description** 📜 — Explains clearly what the tool does.
3. **Input Schema** 🗂️ — Defines what input arguments are required, using typing or Pydantic models.

✅ **Example**:
```python
tool = Tool(
    name="search_tool",
    description="Useful for searching the internet for current information.",
    func=search_function
)
```
✅ **Result**:  
The LLM is now *aware* of `search_tool` and can think about using it.

---

## 📞 2. Tool Calling

**Tool Calling** = **LLM's decision-making process** to use a specific tool during its reasoning.

✅ **How Tool Calling Works**:
- The LLM **analyzes** the situation or query.
- It **decides** if using a tool will help.
- It **selects** the appropriate tool (by its registered name).
- It **prepares structured input arguments** for that tool (according to the tool's schema).

✅ **Important**:
- LLM **only suggests** tool usage.
- **It does NOT directly run** the tool itself.
- It outputs the suggestion as a **structured message** (like a JSON object).

✅ **Example**:
> "Use `multiply_tool` with `number1=7` and `number2=8`."

✅ **What Happens Internally**:
```json
{
  "tool": "multiply_tool",
  "arguments": {
    "number1": 7,
    "number2": 8
  }
}
```

---

## ⚙️ 3. Tool Execution

**Tool Execution** = **Running the actual Python function** suggested by the LLM.

✅ **How Execution Works**:
- LangChain or your backend **reads the tool suggestion**.
- It **locates** the correct Python function by the tool name.
- It **calls** the function, passing the arguments the LLM proposed.
- The **function runs** and **returns the output**.

✅ **Example**:
Suppose `multiply_tool` is defined as:
```python
def multiply_tool(number1: int, number2: int) -> int:
    return number1 * number2
```
- After execution:
  - Input = `number1=7`, `number2=8`
  - Output = **56**

✅ **Key Insight**:
- **Tool Execution happens outside** the LLM.
- **The system does the real work** based on LLM's reasoning.

---

# 📦 Types of Tools in LangChain

There are **different ways** to define tools:

| Type | Description | When to Use |
|:---|:---|:---|
| 🛠️ Built-in Tools | Pre-made tools available in LangChain. | Quickly use common services (e.g., web search, database read). |
| ✍️ Custom Tools | User-defined tools you write yourself. | For calling APIs, custom logic, database queries, business operations. |

---

# 🏗️ How to Create Custom Tools

✅ **3 Main Ways**:

1. **Using `@tool` Decorator**:
   - Quick and simple.
   - Annotate any Python function.

   ```python
   from langchain.tools import tool
   
   @tool
   def add_numbers(x: int, y: int) -> int:
       return x + y
   ```

2. **Using `StructuredTool` with Pydantic**:
   - Structured input validation.
   - Good for complex input formats.

   ```python
   from langchain.tools import StructuredTool
   from pydantic import BaseModel
   
   class AddInput(BaseModel):
       x: int
       y: int

   def add_numbers(inputs: AddInput) -> int:
       return inputs.x + inputs.y

   tool = StructuredTool.from_function(add_numbers)
   ```

3. **Using `BaseTool` (Advanced)**:
   - Full custom control.
   - Build highly customized behaviors.
   - Base class for all tools in LangChain.

---

# 🛍️ Toolkit

✅ **Definition**:
- A **Toolkit** is a **collection (bundle)** of multiple related tools packaged together.

✅ **Purpose**:
- Organize tools around a specific domain or system (e.g., Drive toolkit, Database toolkit).
- Make it easier to plug-and-play multiple tools at once.

✅ **Example**:
- `GoogleDriveToolkit` may include:
  - `upload_file`
  - `download_file`
  - `list_folders`
  - `search_files`

---

# 🎯 Full Summary

| Stage | Meaning | Example |
|:---|:---|:---|
| 🔗 Tool Binding | Register the tool and its schema. | Bind `search_tool`. |
| 📞 Tool Calling | LLM suggests which tool to use. | "Use `multiply_tool` with 7 and 8." |
| ⚙️ Tool Execution | System runs the tool and returns result. | Run `multiply_tool(7, 8) ➔ 56`. |

---

# 💡 Important Points to Remember

- The LLM **thinks and suggests**, but **does not execute** any function.
- The **application backend** or **LangChain agent** is responsible for **tool execution**.
- Proper **descriptions** and **schemas** help the LLM use tools **intelligently**.
- **Custom tools** make LangChain extremely powerful for your own APIs, databases, apps, and systems.

---

# 🛠️ LangChain Tools — Cheat Sheet

---

🔹 **Tool** = A Python function packaged for LLMs to understand and call.  

🔹 **Built-in Tools** = Ready-to-use (e.g., DuckDuckGo search, Shell tool, APIs, Databases).  

🔹 **Custom Tools** = Your own functions, APIs, or app logic made usable by LLMs.  

🔹 **Tool Binding** = Register the tool ➔ give name, description, input schema.  

🔹 **Tool Calling** = LLM suggests a tool name + input arguments (structured output).  

🔹 **Tool Execution** = Actual Python function runs based on LLM's suggestion.

🔹 **3 Ways to Create Custom Tools**:
- `@tool` decorator (easy)
- `StructuredTool` + Pydantic (structured input)
- `BaseTool` (full control)

🔹 **Toolkit** = A bundle of related tools packaged together for reusability.

🔹 **Important**: LLM **suggests**, LangChain/backend **executes**.

---

✅ **Flow**:  
**Binding ➔ Calling ➔ Execution** — (Repeat until task is completed!)

---

