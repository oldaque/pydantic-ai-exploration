# Pydantic AI Exploration

A comprehensive learning repository exploring core concepts and practical applications of **Pydantic AI**, a modern framework for building AI-powered Python applications.

## 🎯 Overview

This repository contains hands-on examples and educational notebooks demonstrating:
- **Agent architecture** and model orchestration
- **Dependency injection** patterns for secure resource management
- **Function tools** for agent-LLM interaction
- **Real-world implementations** with practical examples

## 📚 Contents

### Notebooks

#### [01 - Basic Agent Concepts](notebooks/01%20-%20Basic%20Agent%20Concepts.ipynb)
Introduction to fundamental Pydantic AI concepts through simple examples.

**Topics covered:**
- Agent initialization and configuration
- Running agents asynchronously
- Inspecting agent outputs and message flows
- Accessing model reasoning processes
- Token usage and cost analysis

#### [02 - Core Concepts](notebooks/02%20-%20Core%20Concepts.ipynb)
Deep dive into three core components of Pydantic AI.

**Topics covered:**

##### Agent
- Model configuration with `ModelSettings`
- Fallback models for reliability
- Message inspection and token tracking

##### Dependencies
- Dependency injection patterns
- Secure resource management (API keys, HTTP clients, database connections)
- Type-safe dependency access via `RunContext`
- Backend safety: keeping sensitive data away from the LLM

##### Function Tools
- **Tool types:** `@agent.tool_plain` (stateless) vs `@agent.tool` (with context)
- Tool execution flow and orchestration
- Real-world example: **Jogo do Bicho** (Brazilian animal lottery game)
- Sequential tool calling and result aggregation

## 🚀 Quick Start

### Prerequisites
```bash
python 3.10+
pip install pydantic-ai
```

### Environment Setup
Create a `.env` file with your API keys:
```
GROQ_API_KEY=your_groq_api_key
OPENAI_API_KEY=your_openai_api_key
```

### Running Notebooks
```bash
jupyter notebook notebooks/
```

## 🔍 Key Concepts

### Agent
The core abstraction in Pydantic AI that:
- Coordinates LLM calls
- Manages execution context
- Orchestrates tool invocation
- Handles message flow and reasoning

### Dependencies
Enable secure injection of shared resources:
- **Type-safe:** Full IDE support and type hints
- **Secure:** Sensitive data never reaches the LLM
- **Efficient:** Resources are shared across all tool calls
- **Flexible:** Support for any Python type

### Tools
Allow agents to perform actions and access external systems:
- **Plain tools** (`@agent.tool_plain`): Simple stateless functions
- **Context tools** (`@agent.tool`): Access dependencies and execution context
- **Auto-discovery:** Tools are automatically exposed to the LLM
- **Flexible returns:** Support strings, Pydantic models, or JSON-serializable objects

## 📊 Example: Jogo do Bicho

A practical example demonstrating tool usage in a Brazilian lottery game context:

```python
# Define dependencies
animal_game = Agent(
    model='groq:openai/gpt-oss-20b',
    deps_type=str,
    system_prompt='You are hosting Jogo do Bicho...'
)

# Tool without context
@animal_game.tool_plain
def draw_animal() -> str:
    """Draw a random animal (1-25)"""
    # Implementation...

# Tool with context
@animal_game.tool
def get_player_name(ctx: RunContext[str]) -> str:
    """Get player name from dependencies"""
    return ctx.deps

# Execute
result = await animal_game.run(
    'My guess is Cobra (Snake)',
    deps='João'
)
```

**Tool Execution Flow:**
```
User Input: "My guess is Cobra (Snake)"
    ↓
LLM decides to call: get_player_name()
    ↓ [Tool returns: "João"]
    ↓
LLM decides to call: draw_animal()
    ↓ [Tool returns: "23 - Fruta"]
    ↓
LLM builds response: "Sorry João, you guessed Cobra (Snake) but the animal drawn was 23 – Fruta. Better luck next time!"
```

## 🏗️ Repository Structure

```
pydantic-ai-exploration/
├── README.md                              # This file
├── notebooks/
│   ├── 01 - Basic Agent Concepts.ipynb   # Beginner examples
│   └── 02 - Core Concepts.ipynb          # Advanced concepts
├── .env                                   # API keys (gitignored)
├── pyproject.toml                         # Project configuration
└── uv.lock                                # Dependency lock file
```

## 💡 Learning Path

1. **Start with Basic Concepts** (`01 - Basic Agent Concepts.ipynb`)
   - Understand agent fundamentals
   - Learn to inspect execution details
   - Analyze token usage and costs

2. **Progress to Core Concepts** (`02 - Core Concepts.ipynb`)
   - Master dependency injection
   - Implement and use tools effectively
   - See real-world patterns in action

3. **Experiment & Extend**
   - Modify system prompts
   - Add new tools
   - Try different models and configurations

## 🛠️ Technologies

- **Pydantic AI** - AI framework for Python
- **Groq** - Fast LLM inference (free tier available)
- **OpenAI** - Alternative model provider
- **httpx** - Async HTTP client for dependencies
- **Jupyter** - Interactive notebook environment

## 📖 Resources

- [Pydantic AI Documentation](https://ai.pydantic.dev/)
- [Pydantic AI Models Overview](https://ai.pydantic.dev/models/overview/)
- [Groq API](https://console.groq.com/)

## 🎓 Educational Focus

This repository emphasizes:
- **Clear explanations** - Concepts broken down step-by-step
- **Practical examples** - Real-world scenarios and patterns
- **Best practices** - Security, type safety, and resource management
- **Cultural context** - Examples from Brazilian culture

## 📝 Notes

- All examples are fully functional and tested
- Comments follow English conventions for consistency
- Dependencies are managed with `uv` for reproducibility
- Each notebook is standalone and can be executed independently

## 🤝 Contributing

This is a personal learning repository. Feel free to fork, modify, and extend for your own educational purposes.

## 📄 License

This project is provided as-is for educational purposes.

---

**Last Updated:** November 2025

For questions or suggestions, feel free to explore the notebooks and experiment with the examples!