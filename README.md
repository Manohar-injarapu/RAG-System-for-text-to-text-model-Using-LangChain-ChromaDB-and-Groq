# RAG-System-for-text-to-text-model-Using-LangChain-ChromaDB-and-Groq

This project implements a Retrieval-Augmented Generation (RAG) system that allows users to ask natural language questions and receive accurate, context-aware answers extracted from a PDF document.

Instead of relying only on a language model’s memory, the system retrieves relevant document content from a vector database and augments the LLM response with grounded information.

RAG system flow:

PDF Document
   ↓
Document Loading
   ↓
Text Chunking
   ↓
Vector Embeddings
   ↓
ChromaDB (Vector Store)
   ↓
Retriever
   ↓
Groq LLM (LLaMA 3.3)
   ↓
Accurate Text Response

-> Environment Setup & Dependencies
  -Google Colab is used as the execution environment.
  -Required libraries are installed using a requirements.txt file.
  -The Groq API key is set as an environment variable to securely access Groq’s LLM services.
  - The PDF is saved locally for further processing

-> Document Loading (PDF Parsing)
  -PyPDFLoader from LangChain is used to:
  -Read the PDF
  -Convert each page into a structured document object

-> Text Chunking (Preprocessing)
  -CharacterTextSplitter splits the document into , Chunk size: 200 characters , Overlap: 50 characters
  - overlap ensures Context is not lost between chunks

-> Embedding Generation (Semantic Representation)
  - HuggingFaceEmbeddings using:Each text chunk is converted into a numerical vector
  - These embeddings capture semantic meaning

->Vector Storage with ChromaDB
  -Vectors are persisted locally (persist_directory="vector_db")
  -Persistent storage for reuse,Easy LangChain integration using chromaDB

-> Retriever Creation
  -ChromaDB is converted into a retriever using , vectordb.as_retriever()
  -Finds the most relevant text chunks, Uses vector similarity instead of keyword matching

 -> LLM Integration Using Groq API
   -llama-3.3-70b-versatile, Temperature is set to 0 for deterministic and factual responses

 ->RetrievalQA Chain (RAG Core)
   -RetrievalQA chain connects:Retriever (ChromaDB), LLM (Groq)
   - these steps involved:
      -User submits a query
      -Relevant document chunks are retrieved
      -Retrieved context is injected into the LLM prompt
      -LLM generates a grounded answer

->Conclusion
This project demonstrates a production-ready RAG system that overcomes traditional LLM limitations by grounding responses in external documents. By combining LangChain orchestration, ChromaDB vector storage, and Groq’s high-performance LLMs, the system delivers accurate, explainable, and context-aware answers from unstructured data sources like PDFs.
  
