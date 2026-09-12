# Agentra 🤖

**Agentra** is an open-source **agentic AI chatbot** built with Python, FastAPI, LangGraph, LangChain, Google Gemini, Tavily, ChromaDB, and SQLite.

It is designed to provide an intelligent conversational experience with real-time streaming, document understanding, retrieval-augmented generation (RAG), web search, conversation memory, and persistent chat history.

---

## ✨ Features

* 🤖 AI-powered conversations using **Google Gemini**
* ⚡ Real-time streaming of AI responses
* 📄 Upload and analyze documents
* 🧠 Retrieval-Augmented Generation (**RAG**) for uploaded files
* 🌐 Web search using **Tavily**
* 💬 Conversation history and memory
* 🧩 Agent orchestration using **LangGraph**
* 🔧 Tool integration using **LangChain**
* 💾 Persistent conversation storage using **SQLite**
* 🔎 Vector search using **ChromaDB**
* 🖥️ Simple web-based chat interface
* 📚 Support for multiple document formats

---

## 🧠 What is Agentra?

Agentra is more than a traditional chatbot. It combines a large language model with external tools, document retrieval, and conversation persistence to provide more useful and context-aware responses.

Depending on the user's request, Agentra can:

* Answer general questions using Google Gemini.
* Search the web for up-to-date information.
* Retrieve relevant information from uploaded documents.
* Maintain context across conversations.
* Stream responses in real time.

### High-Level Workflow

```text
                    ┌──────────────────┐
                    │      User        │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │     Agentra      │
                    │    AI Agent      │
                    └────────┬─────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
              ▼              ▼              ▼
        ┌──────────┐   ┌──────────┐   ┌──────────┐
        │  Gemini  │   │  Tavily  │   │   RAG    │
        │   LLM    │   │   Search │   │ ChromaDB │
        └──────────┘   └──────────┘   └──────────┘
              │              │              │
              └──────────────┼──────────────┘
                             ▼
                    ┌──────────────────┐
                    │  Final Response  │
                    │  + Chat History  │
                    └──────────────────┘
```

---

## 🛠️ Tech Stack

| Technology                  | Purpose                                     |
| --------------------------- | ------------------------------------------- |
| **Python 3.11**             | Backend programming language                |
| **FastAPI**                 | Backend API and web server                  |
| **Jinja2**                  | Frontend template rendering                 |
| **LangGraph**               | Agent orchestration and workflow management |
| **LangChain**               | LLM integration, tools, messages, and RAG   |
| **Google Gemini**           | Large Language Model                        |
| **Tavily**                  | Web search                                  |
| **ChromaDB**                | Vector database for document retrieval      |
| **SQLite**                  | Conversation history and persistence        |
| **HTML / CSS / JavaScript** | Web-based chat interface                    |

---

## 📄 Supported Documents

Agentra supports uploading and processing the following file formats:

* PDF (`.pdf`)
* DOCX (`.docx`)
* TXT (`.txt`)
* Markdown (`.md`)
* Python (`.py`)
* CSV (`.csv`)

Uploaded documents can be processed and indexed in ChromaDB. Agentra can then retrieve relevant information from these documents to answer user questions using RAG.

---

## 📁 Project Structure

```text
Agentra/
│
├── app.py                  # FastAPI application and streaming endpoints
├── agent.py                # LangGraph agent and tool orchestration
├── database.py             # Conversation and persistence logic
├── rag.py                  # Document ingestion and RAG workflow
├── tools.py                # Agent tools such as web search, memory, and RAG
├── requirements.txt        # Python dependencies
│
├── templates/
│   └── index.html          # Frontend web interface
│
├── uploads/                # Uploaded documents
├── data/                   # SQLite database and application data
└── chroma_db/              # ChromaDB vector database storage
```

---

# 🚀 Getting Started

## Prerequisites

Make sure you have the following installed:

* Python 3.11
* pip or Conda
* Git

You will also need:

* Google Gemini API key
* Tavily API key

---

## 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/Agentra.git
```

Navigate to the project directory:

```bash
cd Agentra
```

---

## 2. Create a Virtual Environment

Using Conda:

```bash
conda create -n agentra python=3.11 -y
```

Activate the environment:

```bash
conda activate agentra
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

# 🔑 Environment Variables

Create a `.env` file in the project root directory.

```env
GOOGLE_API_KEY=your_google_api_key
GOOGLE_MODEL=gemini-2.5-flash

TAVILY_API_KEY=your_tavily_api_key

LANGSMITH_TRACING=false
LANGSMITH_ENDPOINT=https://api.smith.langchain.com
LANGSMITH_API_KEY=your_langsmith_api_key
LANGSMITH_PROJECT=agentra
```

### LangSmith Configuration

If you do not want to use LangSmith tracing, set:

```env
LANGSMITH_TRACING=false
```

To enable tracing, configure:

```env
LANGSMITH_TRACING=true
LANGSMITH_ENDPOINT=https://api.smith.langchain.com
LANGSMITH_API_KEY=your_langsmith_api_key
LANGSMITH_PROJECT=agentra
```

> ⚠️ **Security:** Never commit your `.env` file or API keys to GitHub. Add `.env` to your `.gitignore` file.

---

# 💻 Run Locally

Start the FastAPI application:

```bash
python app.py
```

The application will be available at:

```text
http://127.0.0.1:8080
```

Open the URL in your browser to start using Agentra.

---

# 💬 Usage

## 1. Chat with Agentra

Ask general questions and interact with the Gemini-powered AI assistant.

Example:

```text
Explain recursion in C++ with an example.
```

## 2. Upload and Analyze Documents

Upload a PDF, DOCX, TXT, Markdown, Python, or CSV file.

Then ask questions such as:

```text
Summarize the uploaded document.
```

```text
What are the key points discussed in this PDF?
```

## 3. Ask Questions Using RAG

Agentra retrieves relevant information from uploaded documents to provide context-aware answers.

Example:

```text
Based on the uploaded document, explain the methodology used.
```

## 4. Search the Web

Agentra can use Tavily to retrieve current information from the web.

Example:

```text
Search the web for the latest developments in AI agents.
```

## 5. Conversation Memory

Agentra stores conversation history, allowing users to continue conversations and recall relevant previous messages.

---

# 🧩 Architecture

Agentra consists of several interconnected components:

```text
                         ┌─────────────────┐
                         │      User       │
                         └────────┬────────┘
                                  │
                                  ▼
                         ┌─────────────────┐
                         │    FastAPI      │
                         │     Server      │
                         └────────┬────────┘
                                  │
                                  ▼
                         ┌─────────────────┐
                         │    LangGraph    │
                         │   Agent Engine  │
                         └────────┬────────┘
                                  │
                 ┌────────────────┼────────────────┐
                 │                │                │
                 ▼                ▼                ▼
          ┌────────────┐   ┌────────────┐   ┌────────────┐
          │   Gemini   │   │   Tavily   │   │    RAG     │
          │    LLM     │   │ Web Search │   │  ChromaDB  │
          └────────────┘   └────────────┘   └────────────┘
                 │                │                │
                 └────────────────┼────────────────┘
                                  ▼
                         ┌─────────────────┐
                         │     SQLite      │
                         │ Conversation DB │
                         └─────────────────┘
```

---

# 🔮 Future Improvements

Potential future additions to Agentra include:

* 🔐 User authentication and authorization
* 👤 Support for multiple users
* 🧠 Improved long-term memory
* 📚 Advanced multi-document RAG
* 🔍 Hybrid search capabilities
* 🧰 Additional AI tools and integrations
* 🖼️ Multimodal image understanding
* 🎙️ Voice-based conversations
* 📊 Enhanced agent execution tracing
* 🧑‍💻 Code execution capabilities
* 🔒 Production-grade security

---

# 🔒 Security Notes

* Never commit `.env` files or API keys to GitHub.
* Keep API keys on the backend.
* Do not expose secret credentials in frontend code.
* Validate uploaded files before processing them.
* Use secure configuration practices when running the application.
* Avoid using development settings such as `reload=True` in production environments.

---

# 🤝 Contributing

Contributions are welcome!

To contribute:

1. Fork the repository.
2. Create a new branch.

```bash
git checkout -b feature/your-feature
```

3. Make your changes.
4. Commit your changes.

```bash
git commit -m "Add new feature"
```

5. Push your branch.

```bash
git push origin feature/your-feature
```

6. Open a Pull Request.

---

# 📜 License

Agentra is an open-source project.

Please check the repository's license for the terms and conditions governing its use, modification, and distribution.

---

## ⭐ Support

If you find Agentra useful, consider giving the repository a ⭐ on GitHub.

**Agentra — An AI agent that can think, search, retrieve, and respond.**
