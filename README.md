# 🚀 RAG API with FastAPI, ChromaDB, Ollama & Kubernetes

An end-to-end **Retrieval-Augmented Generation (RAG)** API built using FastAPI, ChromaDB, and a locally hosted LLM (TinyLlama via Ollama), containerized with Docker and deployed to Kubernetes (Minikube).

This project demonstrates practical AI infrastructure concepts including vector retrieval, model serving, container orchestration, and CI automation.

---

## 🧠 Overview

This project implements a lightweight RAG pipeline:

1. User submits a query via HTTP  
2. Relevant context is retrieved from ChromaDB  
3. Context is injected into the prompt  
4. TinyLlama (via Ollama) generates the final response  
5. API returns grounded answer  

The dataset currently includes semantic documentation around:
- Kubernetes fundamentals  
- Nextwork concepts  

---

## 🏗 Architecture

```bash
User Request
     ↓
FastAPI (/query)
     ↓
ChromaDB (Vector Search)
     ↓
Context Injection
     ↓
Ollama (TinyLlama LLM)
     ↓
Generated Response
```


## Deployment Layer:


---

## 🔧 Tech Stack

- **FastAPI** – REST API framework  
- **Uvicorn** – ASGI server for running FastAPI  
- **ChromaDB** – Vector database for semantic retrieval  
- **Ollama** – Local LLM runtime  
- **TinyLlama** – Lightweight LLM model  
- **Docker** – Containerization  
- **Kubernetes (Minikube)** – Orchestration  
- **GitHub Actions** – CI for semantic document validation  

---

## 📦 Features

- Vector-based semantic search using embeddings  
- Context-aware prompt generation  
- Local LLM inference via Ollama  
- Dockerized application  
- Kubernetes deployment (Deployment + Service)  
- NodePort exposure  
- CI pipeline for document validation checks  
- Environment-based configuration  
- Optional mock LLM mode for testing  

---

## 🐳 Running Locally (Development Mode)

### Install Dependencies

```bash
pip install -r requirements.txt
```
### Start Ollama
```bash
ollama serve
```
### Ensure Tinyllama is installed

Tinyllama is the LLM that is being used inside Ollama to generate a response for our API

```bash
ollama pull tinyllama
```
### Run embed.py

This initializes the vector DB

```bash
python embed.py
```

### Run API
```bash
uvicorn app:app --reload
```
API is available at http://127.0.0.1:8000

### Example Request

```bash
curl -X POST "http://127.0.0.1:8000/query" \ -G --data-urlencode "q=What is Kubernetes?"
```
## 🐳 Docker Usage

## Build Image
```bash
docker build -t rag-app .
```

## Run Container
```bash
docker run -p 8000:8000 rag-app
```
## ☸ Kubernetes Deployment (Minikube)

### 1️⃣ Point Docker to Minikube
```bash
minikube docker-env | Invoke-Expression
```
### 2️⃣ Build Image Inside Cluster
```bash
docker build -t rag-app .
```
### 3️⃣ Deploy
```bash
kubectl apply -f k8s/
```
### 4️⃣ Access Service
```bash
minikube service rag-app-service --url
```
## 🔄 CI Pipeline

The project includes a GitHub Actions workflow that:

- Validates document structure

- Performs semantic integrity checks

- Builds the Docker image

- Ensures application startup consistency

This ensures RAG document changes maintain expected semantic behavior.

This project was built as part of the NextWork AI DevOps challenge

