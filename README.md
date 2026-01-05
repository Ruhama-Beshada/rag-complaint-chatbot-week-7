🧠 RAG Complaint Chatbot

Intelligent Complaint Analysis for Financial Services

📄 License

MIT License
Language: Python

📌 Project Overview

This project implements a Retrieval-Augmented Generation (RAG) chatbot built on the Consumer Financial Protection Bureau (CFPB) consumer complaint dataset.
The system enables users to ask natural-language questions about financial consumer complaints and receive accurate, context-aware answers backed by real complaint evidence, with retrieved sources shown for transparency.

The chatbot is designed to support internal stakeholders such as Product, Customer Support, Risk, and Compliance teams by transforming unstructured complaint narratives into actionable insights.

This work was completed as part of 10 Academy – AI Mastery (Week 7 Challenge).

🧩 Key Features

Semantic search over real consumer complaints

Evidence-based answers using Retrieval-Augmented Generation

Source transparency (retrieved complaint chunks displayed)

Modular, production-ready pipeline

Simple and clean Gradio chat interface

📚 Table of Contents

Project Overview

Dataset

Tasks

Task 1: Exploratory Data Analysis (EDA)

Task 2: Text Chunking, Embedding, and FAISS Indexing

Task 3: RAG Pipeline

Task 4: Interactive Chat Interface

Project Structure

Installation

Usage

Results & Deliverables

Future Improvements

License

📊 Dataset

The project uses the Consumer Financial Protection Bureau (CFPB) Consumer Complaints Dataset, which contains real consumer narratives related to financial products and services.

Dataset details:

Total complaints used: 82,164

Filtered to key financial products:

Credit Cards

Personal Loans

Savings Accounts

Other major retail financial products

Cleaned and prepared dataset: filtered_complaints.csv

Source: CFPB Consumer Complaints Database

🛠 Tasks
Task 1: Exploratory Data Analysis (EDA)

Objective:
Understand the structure, length, and quality of complaint narratives to guide preprocessing and model design.

Steps Completed:

Loaded and inspected consumer_complaints.csv

Analyzed narrative length distribution

Range: 0 – 6,469 words

Majority of complaints are short

Visualized narrative length distribution (right-skewed)

Cleaned complaint text:

Lowercasing

Removed special characters

Removed boilerplate phrases

Filtered complaints to relevant financial products

Deliverables:

filtered_complaints.csv

Narrative length histogram

Notebook: notebooks/task1_eda.ipynb

Task 2: Text Chunking, Embedding, and FAISS Indexing

Objective:
Convert complaint narratives into a semantic search-ready vector database.

Steps Completed:

Sampled ~15,000 complaints while preserving product distribution

Split long narratives into overlapping chunks to maintain context

Generated embeddings using:

SentenceTransformer("all-MiniLM-L6-v2")

Built a FAISS vector store for fast similarity search

Stored metadata for each chunk:

complaint_id

product

chunk_index

text

Deliverables:

Notebook: notebooks/text_chunking_embedding.ipynb

FAISS index: vector_store/faiss_index.bin

Metadata file: vector_store/metadata.pkl

Task 3: RAG Pipeline

Objective:
Implement the Retrieval-Augmented Generation pipeline combining semantic retrieval and answer generation.

Steps Completed:

Implemented retrieve() function:

Retrieves top-k relevant complaint chunks using FAISS

Implemented generate_answer() function:

Generates answers grounded in retrieved evidence

Built a modular pipeline in src/pipeline.py

Tested pipeline with real user-style queries

Deliverables:

Pipeline module: src/pipeline.py

Supporting modules:

src/retrieval.py

src/generator.py

Notebook for testing: notebooks/task3_rag_pipeline.ipynb

Evaluation table and analysis included in final report

Task 4: Interactive Chat Interface

Objective:
Create a user-friendly interface for non-technical users to interact with the RAG system.

Implementation:

Built using Gradio (app.py)

Core Features:

Text input for user queries

“Ask” button to submit questions

Instant display of generated answers

Display of retrieved sources for transparency

“Clear” button to reset conversation

Deliverables:

app.py (Gradio application)

Screenshots / GIFs for report

Clean and intuitive UI

🗂 Project Structure
rag-complaint-chatbot/
├── app.py                        # Gradio chat interface
├── filtered_complaints.csv       # Cleaned dataset
├── notebooks/
│   ├── task1_eda.ipynb
│   ├── text_chunking_embedding.ipynb
│   └── task3_rag_pipeline.ipynb
├── src/
│   ├── __init__.py
│   ├── pipeline.py               # RAG pipeline
│   ├── retrieval.py              # Retrieval logic
│   └── generator.py              # Answer generation logic
├── vector_store/
│   ├── faiss_index.bin
│   └── metadata.pkl
├── requirements.txt
└── README.md

⚙️ Installation

Clone the repository:

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


Gradio will provide a local URL — open it in your browser to start chatting with the RAG chatbot.

📈 Results & Deliverables

EDA insights: complaint length distribution and cleaning strategy

FAISS vector store: enables fast semantic search

RAG pipeline: modular retrieval + generation logic

Interactive chatbot: fully functional Gradio application

Final report: evaluation table, analysis, and UI screenshots

🚀 Future Improvements

Token-by-token streaming responses

Integration of larger or fine-tuned LLMs

Multi-turn conversation memory

Web deployment (Streamlit Cloud, Hugging Face Spaces, or similar)

Advanced evaluation metrics (faithfulness, relevance, latency)

📜 License

This project is licensed under the MIT License.
See the LICENSE file for details.
