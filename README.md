# Shreygpt
 
SHREYGPT is an open-source agentic AI chatbot built with Python, FastAPI, LangGraph, LangChain, Google Gemini, Tavily, ChromaDB, and SQLite.

It supports real-time streaming chat, document uploads, retrieval-augmented generation (RAG), web search, conversation memory, and a simple web UI.

Features
Chat with an AI agent powered by Google Gemini
Stream responses in real time
Upload documents such as PDF, DOCX, TXT, MD, PY, and CSV
Use uploaded files as context through RAG
Search the web with Tavily for current information
Store and recall conversation history
Simple FastAPI-based web interface
Docker-ready deployment
AWS CI/CD support using GitHub Actions, ECR, and EC2
Project Overview
This project combines:

FastAPI for the backend server and API endpoints
Jinja2 for rendering the frontend UI
LangGraph for agent orchestration
LangChain for tools, messages, and RAG workflow
Google Gemini as the LLM provider
Tavily for web search
ChromaDB for vector search over uploaded documents
SQLite for conversation and persistence
Docker for containerized deployment
Prerequisites
Make sure you have the following installed:

Python 3.11
pip or conda
Git
Google API key for Gemini
Tavily API key for web search
Optional for deployment:

Docker
AWS account
Amazon ECR repository
EC2 instance
GitHub Actions self-hosted runner
Getting Started
1. Clone the repository
 https://github.com/VINNU7890/shreygpt
2. Navigate to the project directory
cd BappyGPT
3. Create a virtual environment
Using conda:

conda create -n bappygpt python=3.11 -y
4. Activate the virtual environment
conda activate bappygpt
5. Install dependencies
pip install -r requirements.txt
Environment Variables
Create a .env file in the project root directory.

GOOGLE_API_KEY=your_google_api_key
GOOGLE_MODEL=gemini-2.5-flash

TAVILY_API_KEY=your_tavily_api_key

LANGSMITH_TRACING=false
LANGSMITH_ENDPOINT=https://api.smith.langchain.com
LANGSMITH_API_KEY=your_langsmith_api_key
LANGSMITH_PROJECT=bappygpt
If you do not want to use LangSmith tracing, keep:

LANGSMITH_TRACING=false
Run Locally
Start the FastAPI app:

python app.py
The app will be available at:

http://127.0.0.1:8080
Project Structure
BappyGPT/
│
├── app.py                  # FastAPI app and streaming chat endpoints
├── agent.py                # LangGraph agent setup and tool orchestration
├── database.py             # Conversation and persistence logic
├── rag.py                  # Document ingestion and RAG logic
├── tools.py                # Agent tools such as web search, memory, and RAG
├── requirements.txt        # Python dependencies
├── Dockerfile              # Docker image configuration
├── .dockerignore           # Docker ignore rules
│
├── templates/
│   └── index.html          # Frontend UI
│
├── uploads/                # Uploaded documents
├── data/                   # SQLite database and app data
└── chroma_db/              # ChromaDB vector database storage
Docker Deployment
1. Build the Docker image
docker build -t bappygpt .
2. Run the Docker container
docker run -d \
  --name bappygpt \
  --restart always \
  -p 8081:8081 \
  --env-file .env \
   shreygpt
The app will be available at:

http://localhost:8081
 
