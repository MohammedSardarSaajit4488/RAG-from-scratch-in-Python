# 🧠 RAG From Scratch in Python

A complete **Retrieval-Augmented Generation (RAG)** system built from scratch in plain Python, in under 50 lines of code. It runs **100% locally** with [Ollama](https://ollama.com), so it is free and private, and your documents never leave your machine.

> Built while following the tutorial [How to Build RAG From Scratch in 50 Lines of Python](https://youtu.be/f9uAG3AQGWM) by Tech With Tim.

---

## 📌 Table of Contents

- [The Problem](#-the-problem)
- [What is RAG?](#-what-is-rag)
- [How It Works](#-how-it-works)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Usage](#-usage)
- [What I Learned](#-what-i-learned)
- [Next Steps](#-next-steps)
- [Acknowledgements](#-acknowledgements)

---

## ❓ The Problem

A normal LLM has never seen your private data: your notes, handbooks, or PDFs. Ask it something like *"What's the alarm code at my cafe?"* and it will either say it doesn't know or **make something up** (hallucinate).

## 💡 What is RAG?

**Retrieval-Augmented Generation** fixes this by giving the model the right information at question time:

1. **Retrieve** the most relevant pieces of your documents.
2. **Augment** the prompt with those pieces as context.
3. **Generate** an answer grounded in your actual data.

No retraining or fine-tuning is needed.

## ⚙️ How It Works

```
 Your documents
       │
       ▼
┌──────────────┐   ┌──────────────┐   ┌──────────────────┐
│ 1. Chunking  │ → │ 2. Embedding │ → │ In-memory vector │
│ split text   │   │ text→vectors │   │ store (a list)   │
└──────────────┘   └──────────────┘   └──────────────────┘
                                                │
 User question ── embed ── 3. Similarity search ┘
                                  │ top-k relevant chunks
                                  ▼
                     ┌─────────────────────────┐
                     │ 4. Prompt + context     │
                     │    → local LLM (Ollama) │
                     └─────────────────────────┘
                                  │
                                  ▼
                     Grounded answer ✅
```

| Step | What happens |
|------|--------------|
| **0. Models** | Pull a local embedding model and a local chat model via Ollama |
| **1. Chunking** | Split documents into small, meaningful pieces |
| **2. Embedding** | Convert each chunk into a vector that captures its meaning |
| **3. Searching** | Embed the question and find the closest chunks with cosine similarity |
| **4. Calling the LLM** | Pass the retrieved chunks and the question to the LLM to produce an answer |

## ✨ Features

- 🪶 **Tiny**: the whole pipeline fits in under 50 lines of Python
- 🔒 **Private**: everything runs locally, with no API keys and no data sent out
- 💸 **Free**: uses open-source models through Ollama
- 🚫 **No heavy frameworks**: no LangChain and no pre-built vector database
- 🎓 **Educational**: every step is simple enough to read and understand

## 🛠 Tech Stack

- **Python 3.9+**
- **[Ollama](https://ollama.com)**: runs the embedding and chat models locally
- **Plain Python**: lists and cosine similarity act as the "vector database"

## 📁 Project Structure

```
.
├── rag.py            # The full RAG pipeline
├── data/             # Your source documents (e.g. dataset.txt)
├── requirements.txt  # Python dependencies
└── README.md
```

> Adjust the file names above to match your repository.

## 🚀 Getting Started

### Prerequisites

- [Python 3.9+](https://www.python.org/downloads/)
- [Ollama](https://ollama.com/download) installed and running

### Installation

```bash
# 1. Clone the repo
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>

# 2. (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Pull the models with Ollama
ollama pull <embedding-model>
ollama pull <chat-model>
```

Replace `<embedding-model>` and `<chat-model>` with the models you used in your `rag.py`.

## ▶️ Usage

```bash
python rag.py
```

Then ask a question about your documents:

```
Ask a question: What's the alarm code at the cafe?
Answer: <answer grounded in your documents>
```

## 📚 What I Learned

- **Why LLMs hallucinate** on private data, and how RAG grounds answers in real sources
- **Chunking**: how chunk size and overlap affect retrieval quality
- **Embeddings**: turning text into vectors that capture meaning
- **Cosine similarity**: ranking chunks by how close they are to the question
- **Prompt construction**: injecting retrieved context into the LLM prompt
- **Running LLMs locally** with Ollama for free, private AI apps
- That a vector database is just *vectors plus similarity search*, which a list can do at small scale

## 🔭 Next Steps

- [ ] Load real files (PDFs, Markdown, DOCX) instead of plain text
- [ ] Smarter chunking (sentence or paragraph aware, with overlap)
- [ ] Persist embeddings to disk so they aren't recomputed each run
- [ ] Move to a vector database (FAISS, Chroma, Qdrant) as data grows
- [ ] Add a chat history and a simple UI (Streamlit or Gradio)
- [ ] Show source citations alongside each answer

## 🙏 Acknowledgements

- [Tech With Tim](https://www.youtube.com/channel/UC4JX40jDee_tINbkjycV4Sg) for the original tutorial
- [Ollama](https://ollama.com) for making local LLMs easy

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

⭐ If you found this useful, consider giving the repo a star!
