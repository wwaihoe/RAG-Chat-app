# RAG Chat
A web application that allows users to upload documents to a knowledge base which is used by a LLM to generate relevant responses. When a document is uploaded to the application, the text is extracted and split into concise documents. These documents are stored in a vector store indexed by their embeddings generated by an embedding model. Upon receiving a query in the chat, the vector store will retrieve the documents which are the most similar by comparing the embeddings of the documents with the query. This document is then incorporated into the prompt to the LLM as context for answering the query.
The chat model also has a memory feature and keeps track of the chat history of the ongoing chat and uses it as context for generating the next response.

![RAGChat screenshot](https://github.com/wwaihoe/RAG-Chat/assets/91514179/06512f90-5a81-4bf4-bd85-652ce3517e98)

## How to run
1. Download GGUF models from [Hugging Face](https://huggingface.co/models) and put them in `chat-model/models`
2. Run command `docker compose up --build` to build and run containers.
3. Upon completion, RAG Chat will run on localhost:8000

## Flow of Events
![System Workflow Diagram](https://github.com/wwaihoe/RAG-Chat/assets/91514179/613c29d5-a22d-4ff5-a56d-b3ec7f90b3cb)

Demo
https://github.com/wwaihoe/RAG-Chat/assets/91514179/f2faf433-501b-471d-b5e3-b9ac086db65f

## Microservices Architecture
The web application consists of 3 Docker containers which are run together using docker compose. Each of the services run on each container are loosely coupled and modular, with each service having a well-defined and focused scope and function. This ensures that the application is less prone to complete failure with the benefit of fault isolation, whereby a failure in one service would not bring down the entire application The independent deployments of the services also allows updates to the application in the future to be more seamless. Lastly, there is an added benefit of scalability as each service can be scaled up independently based on demand, allowing for more efficient use of resources.

### Docker Services (Containers)
1. front-end
   - User interface
3. chat-model
   - Generates text response using LLM and document retrieved from retrieval-model
3. retrieval-model
   - Builds vector store from user documents
   - Retrieves relevant documents for knowledge augmented generation by chat-model

### Frameworks and Models
Frameworks:<br>
1. front-end
   - Next.js, React
3. chat-model
   - llama.cpp, LangChain, FastAPI, Uvicorn
3. retrieval-model
   - ChromaDB, SentenceTransformers, PyPDF2, FastAPI, Uvicorn
<br>
Embedding Model:<br>
all-mpnet-base-v2
<br>
<br>
LLMs Tested:<br>
Meta-Llama-3-8B-Instruct-GGUF


