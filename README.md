# 🧠 RAG Complaint Chatbot  
### Intelligent Complaint Analysis for Financial Services

**License:** MIT  
**Language:** Python

---

## 📌 Project Overview

This project implements a **Retrieval-Augmented Generation (RAG) chatbot** built using the **Consumer Financial Protection Bureau (CFPB) consumer complaint dataset**.

The system allows users to ask natural-language questions about consumer complaints and receive **accurate, context-aware answers grounded in real complaint data**, with **retrieved sources shown for transparency**.

The chatbot is designed to support internal teams such as **Product**, **Customer Support**, **Risk**, and **Compliance** by transforming unstructured complaint narratives into **searchable, evidence-backed insights**.

This project was completed as part of **10 Academy – AI Mastery (Week 7 Challenge)**.

---

## ✨ Key Features

- Semantic search over real CFPB consumer complaints  
- Retrieval-Augmented Generation (RAG) for grounded answers  
- Source transparency (retrieved complaint chunks displayed)  
- Modular and extensible pipeline architecture  
- Clean and user-friendly Gradio chat interface  

---

## 📚 Table of Contents

- [Project Overview](#-project-overview)
- [Dataset](#-dataset)
- [Tasks](#-tasks)
  - [Task 1: Exploratory Data Analysis (EDA)](#task-1-exploratory-data-analysis-eda)
  - [Task 2: Text Chunking, Embedding, and FAISS Indexing](#task-2-text-chunking-embedding-and-faiss-indexing)
  - [Task 3: RAG Pipeline](#task-3-rag-pipeline)
  - [Task 4: Interactive Chat Interface](#task-4-interactive-chat-interface)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Usage](#-usage)
- [Results & Deliverables](#-results--deliverables)
- [Future Improvements](#-future-improvements)
- [License](#-license)

---

## 📊 Dataset

The project uses the **Consumer Financial Protection Bureau (CFPB) Consumer Complaints Dataset**, which contains real consumer narratives related to financial products and services.

**Dataset Details:**
- Total complaints used: **82,164**
- Filtered to key financial products:
  - Credit Cards  
  - Personal Loans  
  - Savings Accounts  
  - Other major retail financial products
- Cleaned and prepared dataset: `filtered_complaints.csv`

**Source:** CFPB Consumer Complaints Database

---

## 🛠 Tasks

### Task 1: Exploratory Data Analysis (EDA)

**Objective:**  
Understand the structure, length, and quality of complaint narratives to guide preprocessing and model development.

**Steps Completed:**
- Loaded and inspected the raw complaint dataset
- Analyzed complaint narrative lengths  
  - Range: **0 – 6,469 words**
  - Majority of complaints are short
- Visualized narrative length distribution (right-skewed)
- Cleaned complaint text:
  - Lowercasing
  - Removal of special characters
  - Removal of boilerplate phrases
- Filtered complaints to relevant financial products

**Deliverables:**
- `filtered_complaints.csv`
- Complaint length histogram
- Notebook: `notebooks/task1_eda.ipynb`

---

### Task 2: Text Chunking, Embedding, and FAISS Indexing

**Objective:**  
Transform complaint narratives into a **semantic search–ready vector database**.

**Steps Completed:**
- Sampled ~15,000 complaints while preserving product proportions
- Split long narratives into overlapping chunks to maintain context
- Generated embeddings using:
  - `SentenceTransformer("all-MiniLM-L6-v2")`
- Built a **FAISS vector store** for fast similarity search
- Stored metadata for each chunk:
  - `complaint_id`
  - `product`
  - `chunk_index`
  - `text`

**Deliverables:**
- Notebook: `notebooks/text_chunking_embedding.ipynb`
- FAISS index: `vector_store/faiss_index.bin`
- Metadata file: `vector_store/metadata.pkl`

---

### Task 3: RAG Pipeline

**Objective:**  
Build the **Retrieval-Augmented Generation pipeline** that combines semantic retrieval with answer generation.

**Steps Completed:**
- Implemented a `retrieve()` function to fetch top-k relevant chunks from FAISS
- Implemented a `generate_answer()` function to produce grounded answers
- Modularized the pipeline in `src/pipeline.py`
- Tested the pipeline using realistic user queries

**Deliverables:**
- Pipeline module: `src/pipeline.py`
- Supporting modules:
  - `src/retrieval.py`
  - `src/generator.py`
- Testing notebook: `notebooks/task3_rag_pipeline.ipynb`
- Evaluation table and analysis included in the final report

---

### Task 4: Interactive Chat Interface

**Objective:**  
Provide a **user-friendly interface** for non-technical users to interact with the RAG system.

**Implementation:**
- Built using **Gradio** (`app.py`)

**Core Features:**
- Text input for user questions
- “Ask” button to submit queries
- Instant display of generated answers
- Display of retrieved sources for transparency
- “Clear” button to reset the conversation

**Deliverables:**
- `app.py` (Gradio application)
- Screenshots / GIFs for the final report
- Clean and intuitive UI

---

## 🗂 Project Structure

rag-complaint-chatbot/
├── app.py # Gradio chat interface
├── filtered_complaints.csv # Cleaned dataset
├── notebooks/
│ ├── task1_eda.ipynb
│ ├── text_chunking_embedding.ipynb
│ └── task3_rag_pipeline.ipynb
├── src/
│ ├── init.py
│ ├── pipeline.py # RAG pipeline
│ ├── retrieval.py # Retrieval logic
│ └── generator.py # Answer generation logic
├── vector_store/
│ ├── faiss_index.bin
│ └── metadata.pkl
├── requirements.txt
└── README.md


---

## ⚙️ Installation

Clone the repository:

```bash
git clone https://github.com/<your-username>/rag-complaint-chatbot.git
cd rag-complaint-chatbot


Create and activate a virtual environment:

python -m venv venv
venv\Scripts\Activate.ps1   # Windows PowerShell


Install dependencies:

pip install -r requirements.txt

▶️ Usage
Run RAG Pipeline (Optional – for testing)
from src.pipeline import rag_pipeline

query = "What are common issues with credit cards?"
answer, sources = rag_pipeline(query)

print(answer)
print(sources)

Run Interactive Chat Interface
python app.py


Gradio will provide a local URL. Open it in your browser to start chatting with the RAG chatbot.

📈 Results & Deliverables

EDA insights: complaint length distribution and cleaning strategy

FAISS vector store enabling semantic search

Modular RAG pipeline (retrieval + generation)

Fully functional Gradio chatbot with source transparency

Final report including evaluation, analysis, and screenshots

🚀 Future Improvements

Token-by-token streaming responses

Integration of larger or fine-tuned LLMs

Multi-turn conversation memory

Cloud deployment (Streamlit Cloud, Hugging Face Spaces, etc.)

Advanced evaluation metrics (faithfulness, relevance, latency)
