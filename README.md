# Shreygpt
 
sHREYGPT is an open-source agentic AI chatbot built with Python, FastAPI, LangGraph, LangChain, Google Gemini, Tavily, ChromaDB, and SQLite.

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
git clone https://github.com/entbappy/BappyGPT.git
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
  -p 8080:8080 \
  --env-file .env \
  bappygpt
The app will be available at:

http://localhost:8080
AWS CI/CD Deployment with GitHub Actions
This project can be deployed to AWS using:

GitHub Actions
Amazon ECR
Amazon EC2
Docker
GitHub self-hosted runner
1. Create an IAM User
Create an IAM user for deployment and attach the following policies:

AmazonEC2ContainerRegistryFullAccess
AmazonEC2FullAccess
You can also use a more restricted custom IAM policy for production.

2. Create an ECR Repository
Create an Amazon ECR repository.

Example full ECR image URI:

315865595366.dkr.ecr.us-east-1.amazonaws.com/bappygpt
For GitHub Secrets, only save the repository name:

ECR_REPO=bappygpt
Do not save the full ECR URI as ECR_REPO.

3. Create an EC2 Instance
Create an Ubuntu EC2 instance.

Recommended inbound security group rule:

Type: Custom TCP
Port: 8080
Source: 0.0.0.0/0
4. Install Docker on EC2
Connect to your EC2 instance and run:

sudo apt-get update -y
sudo apt-get upgrade -y
Install Docker:

curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
Add the Ubuntu user to the Docker group:

sudo usermod -aG docker ubuntu
newgrp docker
Check Docker:

docker --version
5. Configure EC2 as a GitHub Self-Hosted Runner
Go to your GitHub repository:

Settings → Actions → Runners → New self-hosted runner
Select Linux and follow the commands shown by GitHub.

After setup, start the runner:

./run.sh
For production, you can configure the runner as a service:

sudo ./svc.sh install
sudo ./svc.sh start
GitHub Secrets
Add the following secrets in your GitHub repository:

AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_DEFAULT_REGION
ECR_REPO

GOOGLE_API_KEY
GOOGLE_MODEL
TAVILY_API_KEY
LANGSMITH_TRACING
LANGSMITH_ENDPOINT
LANGSMITH_API_KEY
LANGSMITH_PROJECT
Path:

GitHub Repository → Settings → Secrets and variables → Actions → New repository secret
Example:

AWS_DEFAULT_REGION=us-east-1
ECR_REPO=bappygpt
GOOGLE_MODEL=gemini-2.5-flash
LANGSMITH_TRACING=true
LANGSMITH_ENDPOINT=https://api.smith.langchain.com
LANGSMITH_PROJECT=bappygpt
GitHub Actions Workflow
Create this file:

.github/workflows/cicd.yaml
This workflow will:

Build your Docker image
Push the image to Amazon ECR
Pull the latest image on EC2
Stop the old container
Run the new container
Usage
After running locally or deploying to AWS:

Open the app in your browser.
Start chatting with the AI assistant.
Upload documents to use them as context.
Ask questions about uploaded files.
Ask current-information questions to trigger web search.
Continue conversations with saved chat history.
Example Questions
Summarize the uploaded PDF.
Search the web for the latest AI agent news.
Based on my uploaded document, what are the key points?
Calculate 125 * 48 / 6.
Notes
Do not commit your .env file to GitHub.
Keep API keys inside GitHub Secrets for deployment.
For production, avoid using reload=True in Uvicorn.
Make sure port 8080 is open in your EC2 security group.
Rotate any API keys that were accidentally exposed publicly.
Contributing
Contributions are welcome.

To contribute:

Fork the repository.
Create a new branch.
Make your changes.
Submit a pull request.
License
This project is open source. Please check the repository license for usage terms.
