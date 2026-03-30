# LLM-Based Recruitment Tool

Build an AI-powered job matching application using RAG, LangGraph agents, and Google Gemini to match candidates with relevant job opportunities.

## Tech Stack

- **Python 3.9+** - Main programming language
- **Google Gemini** - LLM via `langchain-google-genai`
- **LangGraph** - Agent framework for tool orchestration
- **ChromaDB** - Vector database for job embeddings
- **Sentence Transformers** - Text embeddings via `langchain-huggingface`
- **Chainlit** - Interactive chat UI
- **LangChain** - LLM application framework
- **Pydantic** - Configuration management
- **Pytest** - Testing framework
- **Black** - Code formatting

## Setup & Run

1. Install dependencies (use virtual environment recommended):
```bash
pip install -r requirements.txt
```

2. Configure environment:
```bash
cp env.example .env
```

Edit `.env` with your Google API key:
```bash
LANGCHAIN_VERBOSE=true
GEMINI_LLM_MODEL="gemini-2.0-flash-lite"
GOOGLE_API_KEY="your-google-api-key-here"
```

Get a free API key from [Google AI Studio](https://aistudio.google.com/).

3. Build the vector database:
```bash
python backend/etl.py
```

4. Run the application:
```bash
python -m chainlit run -w backend/app.py
```

5. Run tests:
```bash
python -m pytest tests
```

6. Format code:
```bash
black --line-length=88 .
```

## Project Structure

```
├── backend/
│   ├── app.py                         # Chainlit entry point
│   ├── config.py                      # Settings management
│   ├── llm_factory.py                 # Gemini LLM factory
│   ├── utils.py                       # PDF to Markdown converter
│   ├── etl.py                         # ETL pipeline (jobs.csv → ChromaDB)
│   ├── retriever.py                   # Vector similarity search
│   └── models/
│       ├── chatgpt_clone.py           # Chat with memory
│       ├── jobs_finder.py             # RAG-based job finder
│       ├── jobs_finder_agent.py       # LangGraph agent
│       └── resume_summarizer_chain.py # Resume summarization
├── dataset/
│   └── jobs.csv                       # Job listings dataset
├── tests/                             # Test suite
├── assignment.md                      # Detailed instructions
├── README.md
└── requirements.txt
```

## Key Concepts Covered

- **Retrieval-Augmented Generation (RAG)** - Combining vector search with LLM generation
- **LLM Agents** - LangGraph-based agents with tool calling
- **Vector Databases** - ChromaDB for semantic search
- **Text Embeddings** - Sentence transformers for job matching
- **Multimodal LLMs** - Gemini vision for PDF processing
- **Prompt Engineering** - Structured prompts for job matching and cover letters
- **Chat Interfaces** - Chainlit for conversational AI
- **ETL Pipelines** - Data ingestion and embedding generation

## Business Problem

Match candidates with relevant job opportunities using AI:
- **Input**: Candidate resume (PDF) and job preferences
- **Output**: Ranked job matches with personalized cover letters
- **Approach**: RAG-based semantic search + LLM agent with tools

**Application Modes**:
1. **Vanilla ChatGPT** - General-purpose chat with conversation memory
2. **Jobs Finder Assistant** - Upload resume, get matched jobs via RAG
3. **Jobs Agent** - Advanced agent that finds jobs and generates cover letters

**Workflow**:
1. ETL pipeline embeds job listings into ChromaDB
2. User uploads resume → Gemini converts PDF to markdown
3. Resume summarizer extracts key skills
4. Vector search retrieves top 4 matching jobs
5. Agent generates personalized cover letters on request

See `assignment.md` for complete project instructions and implementation details.
