
# 🏋️ AI Physical Trainer RAG System

A specialized **Retrieval-Augmented Generation (RAG)** chatbot designed to act as an expert Physical Trainer. Unlike general AI models, this system answers questions **strictly** based on a curated set of PDF training manuals, preventing hallucinations and ensuring advice adheres to specific training methodologies.


## 🚀 Key Features

* **Strict Contextual Guardrails:** The model is prompted to answer *only* using the provided PDFs. If the answer isn't in the manual, it explicitly states "I don't know" rather than inventing exercises.
* **Hybrid Tech Stack:** Combines **Google Gemini 2.5 Flash** (high-speed generation) with **Hugging Face** (local embeddings) for a cost-effective and fast pipeline.
* **Source Transparency:** Every answer can be traced back to the specific PDF page used to generate the response.
* **Rate-Limit Friendly:** Uses local embeddings (`all-MiniLM-L6-v2`) to avoid exhausting Google API quotas during document indexing.

## 🛠️ Tech Stack

* **LLM:** Google Gemini 2.5 Flash (via `langchain-google-genai`)
* **Embeddings:** SentenceTransformers `all-MiniLM-L6-v2` (Local execution)
* **Vector Store:** FAISS (Facebook AI Similarity Search)
* **Orchestration:** LangChain
* **PDF Processing:** PyPDF

## 📂 Project Structure

Ensure your project folder is organized as follows before running the notebook:

```text
physical-trainer-rag/
│
├── training_pdfs/          # 📂 PLACE YOUR PDF MANUALS HERE
│   ├── manual_1.pdf
│   └── manual_2.pdf
│
├── .env                    # 🔑 Store your API Key here (gitignored)
├── .gitignore              # Files to exclude from git
├── notebook.ipynb          # 📓 The main application code
├── requirements.txt        # Python dependencies
└── README.md               # This documentation

```

## ⚙️ Setup & Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/physical-trainer-rag.git
cd physical-trainer-rag
```

### 2. Create a Virtual Environment (Recommended)

```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a file named `.env` in the root directory and add your Google API key:

```ini
GOOGLE_API_KEY=your_actual_api_key_here
```

> **Note:** You can get a key from [Google AI Studio](https://aistudio.google.com/).

### 5. Add Training Data

Create a folder named `training_pdfs` and drag-and-drop your physical training PDF files into it. The system requires at least one PDF to function.

## 🏃 Usage

1. Launch Jupyter Notebook:
```bash
jupyter notebook
```


2. Open `notebook.ipynb`.
3. **Run All Cells**:
* The system will load your environment variables.
* It will ingest and chunk the PDFs in `training_pdfs/`.
* It will download the embedding model (first run only) and build the FAISS vector index.
* Finally, it will initialize the strict RAG chain.


4. Scroll to **Section 5: Test the system** to modify the queries and ask your own questions.

## ⚠️ Configuration Notes

* **Timeout Fix:** The notebook includes `os.environ["HF_HUB_DOWNLOAD_TIMEOUT"] = "60"` to prevent timeouts when downloading the embedding model on slower connections.
* **Temperature:** The LLM is set to `temperature=0` to minimize creativity and maximize factual accuracy based on your documents.

## 📄 License

[MIT](https://choosealicense.com/licenses/mit/)
