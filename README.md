# Agentra

Agentra is an open-source **agentic AI chatbot** built with **Python, FastAPI, LangGraph, LangChain, Google Gemini, Tavily, ChromaDB, and SQLite**.

It is designed as a general-purpose AI assistant capable of **real-time streaming conversations, document understanding, retrieval-augmented generation (RAG), web search, conversation memory, and persistent chat history**.

---

## ✨ Features

* 🤖 Chat with an AI agent powered by **Google Gemini**
* ⚡ Stream AI responses in real time
* 📄 Upload and analyze documents
* 🧠 Retrieval-Augmented Generation (**RAG**) for uploaded files
* 🌐 Search the web using **Tavily**
* 💬 Maintain and recall conversation history
* 🧩 Agent orchestration using **LangGraph**
* 🔧 Tool-based agent workflow using **LangChain**
* 💾 Persistent storage using **SQLite**
* 🔎 Vector search using **ChromaDB**
* 🖥️ Simple web-based chat interface
* 🐳 Docker-ready
* ☁️ AWS deployment support
* 🔄 CI/CD using **GitHub Actions, Amazon ECR, and EC2**

---

## 🧠 What is Agentra?

Agentra goes beyond a traditional chatbot by combining an LLM with external tools and persistent context.

Depending on the user's request, Agentra can:

```text
                ┌──────────────────┐
                │      User        │
                └────────┬─────────┘
                         │
                         ▼
                ┌──────────────────┐
                │     Agentra      │
                │   AI Agent       │
                └────────┬─────────┘
                         │
              ┌──────────┼──────────┐
              │          │          │
              ▼          ▼          ▼
          Web Search     RAG      Memory
          (Tavily)    (ChromaDB) (SQLite)
              │          │          │
              └──────────┼──────────┘
                         ▼
                ┌──────────────────┐
                │  Google Gemini   │
                └────────┬─────────┘
                         │
                         ▼
                ┌──────────────────┐
                │   Final Response │
                └──────────────────┘
```

The agent can determine when external information or uploaded documents are required instead of relying solely on the LLM's internal knowledge.

---

## 🛠️ Tech Stack

| Technology         | Purpose                                  |
| ------------------ | ---------------------------------------- |
| **Python 3.11**    | Backend programming language             |
| **FastAPI**        | Backend API and web server               |
| **Jinja2**         | Frontend template rendering              |
| **LangGraph**      | Agent orchestration and workflow         |
| **LangChain**      | LLM integration, tools, messages and RAG |
| **Google Gemini**  | Large Language Model                     |
| **Tavily**         | Web search                               |
| **ChromaDB**       | Vector database for document retrieval   |
| **SQLite**         | Conversation and application persistence |
| **Docker**         | Containerization                         |
| **GitHub Actions** | CI/CD                                    |
| **Amazon ECR**     | Docker image registry                    |
| **Amazon EC2**     | Cloud deployment                         |

---

## 📂 Supported Documents

Agentra can process multiple document formats, including:

* PDF
* DOCX
* TXT
* Markdown (`.md`)
* Python (`.py`)
* CSV

Uploaded documents are processed and stored in the vector database so that Agentra can retrieve relevant information when answering questions.

---

## 📁 Project Structure

```text
Agentra/
│
├── app.py                  # FastAPI application and streaming endpoints
├── agent.py                # LangGraph agent and tool orchestration
├── database.py             # Conversation and persistence logic
├── rag.py                  # Document ingestion and RAG workflow
├── tools.py                # Agent tools such as web search, memory and RAG
├── requirements.txt        # Python dependencies
│
├── Dockerfile              # Docker image configuration
├── .dockerignore           # Docker ignore rules
├── .env                    # Environment variables (do not commit)
│
├── templates/
│   └── index.html          # Web interface
│
├── uploads/                # Uploaded documents
├── data/                   # SQLite database and application data
└── chroma_db/              # ChromaDB vector database
```

---

# 🚀 Getting Started

## Prerequisites

Make sure you have the following installed:

* Python 3.11
* pip or conda
* Git

You will also need:

* Google Gemini API key
* Tavily API key

For cloud deployment:

* Docker
* AWS account
* Amazon ECR repository
* Amazon EC2 instance
* GitHub Actions
* GitHub self-hosted runner

---

## 1. Clone the Repository

```bash
git clone https://github.com/Ayushi-maheshwari621/Agentra.git
```

Navigate to the project:

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

Create a `.env` file in the project root:

```env
GOOGLE_API_KEY=your_google_api_key
GOOGLE_MODEL=gemini-2.5-flash

TAVILY_API_KEY=your_tavily_api_key

LANGSMITH_TRACING=false
LANGSMITH_ENDPOINT=https://api.smith.langchain.com
LANGSMITH_API_KEY=your_langsmith_api_key
LANGSMITH_PROJECT=agentra
```

### LangSmith

If you do not want to use LangSmith tracing:

```env
LANGSMITH_TRACING=false
```

If you want to enable tracing:

```env
LANGSMITH_TRACING=true
LANGSMITH_ENDPOINT=https://api.smith.langchain.com
LANGSMITH_API_KEY=your_langsmith_api_key
LANGSMITH_PROJECT=agentra
```

> ⚠️ Never commit your `.env` file or API keys to GitHub.

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

Open the URL in your browser and start chatting with Agentra.

---

# 💬 Usage

After launching Agentra, you can:

### 1. Chat with the AI

Ask general questions and have a conversation with the Gemini-powered agent.

```text
Explain recursion in C++.
```

### 2. Analyze Documents

Upload a PDF, DOCX, TXT, Markdown, Python, or CSV file.

Then ask:

```text
Summarize this document.
```

or:

```text
What are the key points discussed in this PDF?
```

### 3. Ask Questions About Uploaded Files

Agentra uses RAG to retrieve relevant sections from uploaded documents.

```text
Based on the uploaded document, explain the methodology used.
```

### 4. Search the Web

For questions requiring current information, Agentra can use Tavily web search.

```text
Search the web for the latest developments in AI agents.
```

### 5. Maintain Conversations

Agentra stores conversation history, allowing previous messages to be recalled during conversations.

---

# 🐳 Docker Deployment

## 1. Build the Docker Image

```bash
docker build -t agentra .
```

## 2. Run the Container

```bash
docker run -d \
  --name agentra \
  --restart always \
  -p 8080:8080 \
  --env-file .env \
  agentra
```

The application will be available at:

```text
http://localhost:8080
```

---

# ☁️ AWS Deployment

Agentra can be deployed to AWS using:

```text
GitHub
   │
   ▼
GitHub Actions
   │
   ▼
Docker Build
   │
   ▼
Amazon ECR
   │
   ▼
Amazon EC2
   │
   ▼
Docker Container
   │
   ▼
Agentra
```

The deployment workflow can automatically:

1. Build the Docker image
2. Authenticate with Amazon ECR
3. Push the latest image to ECR
4. Pull the latest image on EC2
5. Stop the previous Agentra container
6. Start the updated container

---

# 🔐 AWS IAM Configuration

Create an IAM user for deployment.

For development, the following policies can be used:

```text
AmazonEC2ContainerRegistryFullAccess
AmazonEC2FullAccess
```

For production environments, it is recommended to use a **least-privilege custom IAM policy** instead of broad managed policies.

---

# 📦 Amazon ECR

Create an ECR repository for Agentra.

Example:

```text
agentra
```

The resulting image URI may look like:

```text
123456789012.dkr.ecr.us-east-1.amazonaws.com/agentra
```

For GitHub Actions, store the repository name:

```text
ECR_REPO=agentra
```

> Do not store the complete ECR URI as `ECR_REPO` if the workflow expects only the repository name.

---

# 🖥️ Amazon EC2

Create an Ubuntu EC2 instance.

If the application is being accessed directly through port `8080`, configure the security group accordingly:

```text
Type: Custom TCP
Port: 8080
Source: 0.0.0.0/0
```

For production, consider placing the application behind a **reverse proxy/load balancer** and restricting direct access to port 8080.

---

# 🐳 Install Docker on EC2

Connect to your EC2 instance and run:

```bash
sudo apt-get update -y
sudo apt-get upgrade -y
```

Install Docker:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

Add the Ubuntu user to the Docker group:

```bash
sudo usermod -aG docker ubuntu
```

Apply the group change:

```bash
newgrp docker
```

Verify Docker:

```bash
docker --version
```

---

# 🔄 GitHub Self-Hosted Runner

To use EC2 as a GitHub Actions runner:

Navigate to:

```text
GitHub Repository
→ Settings
→ Actions
→ Runners
→ New self-hosted runner
```

Select:

```text
Linux
```

Follow the commands provided by GitHub.

Start the runner:

```bash
./run.sh
```

For persistent execution, configure it as a service:

```bash
sudo ./svc.sh install
sudo ./svc.sh start
```

---

# 🔑 GitHub Secrets

Add the following secrets under:

```text
GitHub Repository
→ Settings
→ Secrets and variables
→ Actions
→ New repository secret
```

### AWS

```text
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_DEFAULT_REGION
ECR_REPO
```

### Gemini

```text
GOOGLE_API_KEY
GOOGLE_MODEL
```

### Tavily

```text
TAVILY_API_KEY
```

### LangSmith

```text
LANGSMITH_TRACING
LANGSMITH_ENDPOINT
LANGSMITH_API_KEY
LANGSMITH_PROJECT
```

Example configuration:

```text
AWS_DEFAULT_REGION=us-east-1
ECR_REPO=agentra

GOOGLE_MODEL=gemini-2.5-flash

LANGSMITH_TRACING=true
LANGSMITH_ENDPOINT=https://api.smith.langchain.com
LANGSMITH_PROJECT=agentra
```

---

# ⚙️ CI/CD Workflow

Create:

```text
.github/workflows/cicd.yaml
```

The workflow is responsible for automating the deployment pipeline:

```text
Code Push
    │
    ▼
GitHub Actions
    │
    ▼
Build Docker Image
    │
    ▼
Push to Amazon ECR
    │
    ▼
EC2 pulls latest image
    │
    ▼
Stop old container
    │
    ▼
Start new container
    │
    ▼
🚀 Agentra Updated
```

This allows new versions of Agentra to be deployed without manually rebuilding and running the application on EC2.

---

# 🧩 Architecture

At a high level, Agentra consists of the following components:

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
          │   Gemini   │   │   Tavily   │   │   RAG      │
          │    LLM     │   │ Web Search │   │ ChromaDB   │
          └────────────┘   └────────────┘   └────────────┘
                                  │
                                  ▼
                         ┌─────────────────┐
                         │     SQLite      │
                         │ Conversation DB │
                         └─────────────────┘
```

---

# 🔮 Future Improvements

Potential future additions to Agentra include:

* 🔐 User authentication
* 👤 Multiple user accounts
* 🧠 Long-term memory
* 📚 Improved multi-document RAG
* 🔍 Hybrid search
* 🧰 More AI tools
* 🖼️ Multimodal image understanding
* 🎙️ Voice conversations
* 📊 Agent execution tracing
* 🧑‍💻 Code execution capabilities
* ☁️ Scalable cloud deployment
* 🔒 Production-grade authentication and authorization

---

# 🔒 Security Notes

* Never commit `.env` to GitHub.
* Store secrets using GitHub Secrets or a dedicated secret manager.
* Do not expose API keys in frontend code.
* Use least-privilege IAM policies in production.
* Rotate API keys immediately if they are accidentally exposed.
* Avoid using development settings such as `reload=True` in production.
* Restrict publicly accessible ports whenever possible.

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

5. Push the branch.

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
