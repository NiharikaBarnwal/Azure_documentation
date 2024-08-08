# Day-20 : Project-2 (RAG application using LLaMa and OpenAI)

## Table of Contents
1. [Introduction](#introduction)
2. [Importance of Memory in LLMs](#importance-of-memory-in-llms)
3. [Project Overview](#project-overview)
4. [Steps to Implement the Project](#steps-to-implement-the-project)
5. [Detailed Explanation of Key Components](#detailed-explanation-of-key-components)
    - [Data Chunking and Embedding](#data-chunking-and-embedding)
    - [Vector Databases](#vector-databases)
    - [Retrieval Augmented Generation Process](#retrieval-augmented-generation-process)
    - [LLaMA Model Interface and Parameter Tuning](#llama-model-interface-and-parameter-tuning)
    - [Enhancing the Conversational AI System](#enhancing-the-conversational-ai-system)
6. [Conclusion](#conclusion)

## Introduction
Retrieval Augmented Generation (RAG) is a process where a model is provided with data (PDFs, text, Excel sheets) to generate answers based on user queries. This process is particularly useful when handling large datasets by distributing them into smaller chunks, embedding them, and storing them in a vector database. This allows for efficient retrieval of relevant information.

## Importance of Memory in LLMs
LLMs are stateless, meaning they lack awareness of previous interactions, leading to potential hallucinations when asked follow-up questions. To mitigate this, we use mechanisms like ConversationBufferMemory to maintain chat history, or history-aware retrievers to provide context-aware responses.

## Project Overview
In this project, we create an application that leverages RAG using the Meta-Llama-3-70B-Instruct model hosted on Azure ML. The model retrieves vectors stored in a local vector database (FAISS) and generates answers to user queries. The project involves setting up a conversational AI system that maintains context and retrieves relevant information efficiently.

In this project, we implemented RAG by:
1. Distributing large data into small chunks.
2. Embedding these chunks.
3. Storing the embeddings in a vector database.
4. Retrieving similar embeddings based on user queries.
5. Augmenting the retrieved embeddings to create new representations.
6. Generating answers using the new representations.

## Steps to Implement the Project

### 1. Create a Resource Group (RG)
- Go to the Azure portal.
- Navigate to "Resource groups".
- Click "Create".
- Enter the necessary details (name, region).
- Click "Review + create".

### 2. Create an Azure Machine Learning Workspace
- Navigate to Azure Machine Learning and click on "Create".
- Provide a name and select networking options (choose public for testing).
- Leave other settings as default.

### 3. Launch Azure ML Studio
- Launch Studio and navigate to the Model Catalog.
- Choose a model (e.g., Meta-Llama-3-70B-Instruct).
- Provide a deployment name.

### 4. Install Azure CLI
- Open the terminal and install Azure CLI.
- Login to Azure using `az login`.

### 5. Write the Code for the Chatbot
- Create a virtual machine (VM) with access to all ports.
- Connect to the VM using Remote Desktop Protocol (RDP).
- Configure the VM as a web server.
- Install Python on the VM.

### 6. Upload and Run the Code
- Upload your code to the VM (e.g., in the `inetpub` directory).
- Install necessary packages using `pip install -r requirements.txt`.
- Run the chatbot using Streamlit: `streamlit run chat_fe.py --server.port 8080`.
- Configure an inbound rule for port 8080.

## Detailed Explanation of Key Components

### Data Chunking and Embedding
- **PyPDF2**: Used to load and read PDF files.
- **RecursiveCharacterTextSplitter**: Divides the PDF into smaller chunks for easier processing.
- **HuggingFaceEmbedding**: Converts the chunks into embeddings.
- **ConversationBufferMemory**: Stores conversation history to provide context.
- **Streamlit**: Framework to build and deploy the chatbot interface.

### Vector Databases
Vector databases store and manage embeddings. Examples include:
- **FAISS** (Facebook AI Similarity Search) - Local (A local vector database for efficient similarity search.)
- **CHROMA** - Local
- **PostgreSQL**
- **Amazon OpenSearch**
- **MongoDB**
- **Pinecone**

### Retrieval Augmented Generation Process
1. **Retrieval**: Retrieves embeddings similar to the user's query.
2. **Augmented**: Selects top items and augments them to create new representations.
3. **Generation**: Uses the new representation to generate answers to the query.

### LLaMA Model Interface and Parameter Tuning
Once connected, we develop an interface to interact with the model through the Azure ML endpoint. Key parameters to adjust include:
- **Temperature**: Controls the creativity of the model's responses. Higher values result in more diverse outputs.
- **Max Tokens**: Sets the maximum length of responses.
- **Top p**: Uses nucleus sampling to balance response quality and diversity.

### Enhancing the Conversational AI System
- **Retrieval System Integration**: Transforms the input vector database into a retriever for efficient context fetching.
- **Chain Construction**: Combines the model interface, retriever, and memory into a cohesive conversational system.
- **Error Handling and Logging**: Implement robust error handling and logging to ensure smooth operation and easy debugging.


## Conclusion
By distributing large data into smaller chunks, embedding, and storing in a vector database, RAG enables efficient retrieval and generation of answers to user queries. This project demonstrates the end-to-end implementation of a RAG-based chatbot deployed on Azure, utilizing various tools and technologies to achieve the desired outcome.
