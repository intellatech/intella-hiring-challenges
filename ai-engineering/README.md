# Intella AI Engineer Assessment

**Project:** Scientific Papers RAG System

## Context

At Intella, we leverage AI to enhance satellite operations through intelligent document analysis, knowledge retrieval, and automated insights generation. A critical capability is building systems that can efficiently retrieve and synthesize information from large document collections.

Your task is to build a **Retrieval-Augmented Generation (RAG) system** that indexes scientific papers from arXiv and enables semantic search and conversational interaction with the document collection. This assessment evaluates your ability to:

- Design and implement RAG pipelines with modern LLM frameworks
- Work with vector databases and embedding models
- Build document ingestion and processing pipelines
- Create intuitive interfaces for AI-powered systems
- Make architectural decisions that balance performance with cost

**Example Workflow:**

1. Ingest papers from arXiv API (abstracts and metadata)
2. Process documents: chunk text, generate embeddings
3. Store embeddings in vector database with metadata
4. User queries: "What are the latest techniques for satellite image classification?"
5. System retrieves relevant chunks, generates contextual response

## Requirements

### 1. Data Collection & Ingestion

Implement a document ingestion pipeline that collects and processes scientific papers:

- **arXiv Integration**: Fetch papers from arXiv API by:
  - Topic/category search (e.g., `cs.AI`, `cs.CV`, `astro-ph`)
  - Keyword search
  - Date range filtering (optional)
- **Core Format**: Process paper **abstracts and metadata** from arXiv
  - This is the minimum requirement
  - Full PDF parsing is a bonus feature
- **Metadata Extraction**: Extract and store:
  - Title, authors, abstract
  - Publication date
  - Categories/tags
  - arXiv ID
- **Minimum Data**: Ingest at least **30-50 papers** for demonstration

### 2. Embedding & Vector Database

Design and implement the embedding and storage layer:

- **Embedding Model**: Use one suitable embedding model:
  - OpenAI `text-embedding-3-small` or `text-embedding-3-large`
  - Open-source alternatives: `sentence-transformers`
  - Or any other suitable embedding model
- **Chunking Strategy**: Implement text chunking:
  - Fixed-size chunks with overlap is acceptable
  - Configurable chunk size
- **Vector Database**: Choose and implement one of:
  - **LanceDB** (recommended - lightweight, no server needed)
  - **Chroma** (simple, in-memory option)
  - **Qdrant** (production-ready, requires server)
  - **pgvector** (PostgreSQL extension)
- **Collection Structure**:
  - Store embeddings with metadata
  - Enable similarity search with configurable top-k

### 3. CLI Query Tool

Implement a command-line interface in Python for interacting with the RAG system:

- **Semantic Search**: Query by natural language
  ```bash
  rag search "transformer architectures for vision"
  ```
- **Ingest Commands**: Add new documents from arXiv
  ```bash
  rag ingest --query "satellite" --limit 50
  ```
- **Database Stats**: View collection statistics
  ```bash
  rag stats
  ```
- **Configuration**: Support environment variables or config files

### 4. LLM Integration

Integrate a Large Language Model for response generation:

- **Provider Support**: Implement one provider:
  - **OpenAI** (GPT-4, GPT-3.5)
  - **Anthropic** (Claude 3)
  - **Ollama** (local models - good for cost-free development)
  - **LM Studio** (local models)
  - **OpenRouter** (multi-model gateway)
- **RAG Pipeline**: Implement retrieval-augmented generation:
  - Retrieve relevant chunks based on query
  - Construct context-aware prompts
  - Generate coherent responses with citations
- **Framework Integration** (optional, choose one if used):
  - **LangChain** / **LangGraph**
  - **Pydantic AI**
  - **LlamaIndex**
  - Custom implementation is perfectly acceptable
- **Response Quality**: Responses should:
  - Reference source documents
  - Synthesize information from retrieved context
  - Acknowledge when relevant info is unavailable

### 5. Code Quality Standards

Your code must demonstrate professional software engineering practices:

- **PEP 8**: Follow Python style guide (use `black` or `ruff` for formatting)
- **PEP 257**: Include docstrings for modules, classes, and key functions
- **Type Hints (PEP 484)**: Use type annotations throughout the codebase
- **Project Structure**: Organize code into logical modules (example structure):
  ```
  ai-engineering/
  ├── src/
  │   ├── ingestion/      # Document ingestion
  │   ├── embeddings/     # Embedding generation
  │   ├── vectordb/       # Vector database operations
  │   ├── rag/            # RAG pipeline
  │   └── cli/            # CLI application
  ├── tests/
  ├── configs/            # Configuration files
  └── ...
  ```
- **Ruff Configuration**: A pre-configured `pyproject.toml` with ruff settings is provided
  - Check compliance: `ruff check .`
  - Format your code: `ruff format .`

### 6. Documentation

Provide documentation for users and developers:

- **Project README.md** must include:
  - Project overview
  - Prerequisites (Python version, dependencies, API keys)
  - Installation instructions
  - Configuration guide (environment variables)
  - How to run the application
  - Usage examples with CLI commands

### 7. Testing

Implement basic test coverage:

- **Unit tests** for key components:
  - Chunking logic
  - Vector database operations
- Use `pytest`
- Mock external API calls (OpenAI, arXiv) in tests

### 8. Version Control Best Practices

- **Repository Setup**:
  - Fork the `intella-hiring-challenges` repository
  - Add the Intella evaluators as contributors
  - Work within your forked repository
  
- **Commit Strategy** (optional but recommended):
  - Write clear commit messages:
    - `feat: implement arXiv paper ingestion`
    - `feat: add vector database integration`
    - `docs: add CLI usage examples`

## Bonus Features (Optional)

Pick any of these to showcase additional skills. These are **not required** for a successful submission:

### PDF & Multi-Format Support

- [ ] **Full PDF Parsing**: Parse complete arXiv papers (not just abstracts)
  - Handle scientific PDF layouts
  - Extract text from sections
- [ ] **Multi-format Ingestion**: Support additional formats
  - Local PDF files
  - Markdown files
  - Plain text files

### Similar Papers Search

- [ ] **Find Similar Papers**: Given a paper ID, find semantically similar papers
  ```bash
  rag similar --paper-id 2301.12345
  ```

### Multiple LLM Providers

- [ ] **Provider Abstraction**: Support switching between providers
  - OpenAI, Anthropic, Ollama, etc.
  - Configuration-based provider selection

### Cluster Visualization

- [ ] **Embedding Visualization**: Create interactive visualizations
  - Use dimensionality reduction (t-SNE, UMAP, PCA)
  - Color clusters by topic/category
  - Interactive exploration with Plotly

### Streamlit GUI

- [ ] **Web Interface**: Build an interactive Streamlit application
  - Search interface with query input
  - Results display with metadata and snippets
  - Settings panel for configuration

### Chat Interface

- [ ] **Conversational RAG**: Implement chat functionality
  - Multi-turn conversation with context
  - Chat history management
  - Source attribution in responses

### Token & Performance Monitoring
- [ ] **Cost Tracking**: Monitor API usage and costs
  - Track token consumption per query
  - Display usage statistics
- [ ] **Performance Metrics**: Monitor system performance
  - Query latency tracking
  - Retrieval quality metrics

### Additional Bonus Features

- [ ] **Docker**: Add `Dockerfile` and `docker-compose.yml`
- [ ] **Caching**: Cache embeddings and LLM responses
- [ ] **Hybrid Search**: Combine semantic and keyword search (BM25)
- [ ] **Re-ranking**: Cross-encoder or LLM-based re-ranking
- [ ] **Async Processing**: Use async/await for I/O operations
- [ ] **Incremental Updates**: Add new documents without reprocessing existing ones

## Evaluation Criteria

Your submission will be evaluated across multiple dimensions:

| Area | What We Look For | Weight |
|------|------------------|--------|
| **RAG Implementation** | Effective retrieval, proper chunking, quality responses | ⭐⭐⭐⭐⭐ |
| **Architecture** | Clean separation of concerns, modular design | ⭐⭐⭐⭐⭐ |
| **Code Quality** | Readability, type safety, proper error handling | ⭐⭐⭐⭐⭐ |
| **LLM Integration** | Proper prompt engineering, working RAG pipeline | ⭐⭐⭐⭐ |
| **Documentation** | Clear README, usage examples | ⭐⭐⭐⭐ |
| **CLI Design** | Intuitive commands, helpful output | ⭐⭐⭐ |
| **Testing** | Basic test coverage for key components | ⭐⭐⭐ |
| **Bonus Features** | Any additional features implemented | ⭐⭐ |

### Key Evaluation Questions

We'll be asking ourselves:

1. **Does the RAG system work?** Can we query and get relevant, coherent responses?
2. **Is the architecture clean?** Separation between ingestion, retrieval, and generation?
3. **Is the code production-quality?** Type hints, error handling, readability?
4. **Can we run it easily?** Clear setup, minimal configuration friction?
5. **Is the CLI intuitive?** Well-designed commands with helpful output?

## Time Expectation

**Estimated time**: Maximum 8 hours

**Our advice**: Focus on **quality over quantity**. A working core RAG system with clean code is better than a feature-complete but buggy implementation.

### Priority Order

If time is limited, prioritize in this order:

1. Working arXiv ingestion (abstracts + metadata)
2. Embeddings stored in vector database
3. Basic semantic search via CLI
4. LLM-powered response generation
5. Documentation (README with setup instructions)
6. Basic tests
7. Bonus features

## Expected Deliverables

Your final submission should include:

### 1. Working RAG System

- Document ingestion from arXiv (abstracts + metadata)
- Vector database with searchable embeddings
- Working CLI tool for queries
- LLM-powered response generation

### 2. Source Code

- Organized project structure
- Type-annotated Python code
- Clean, readable code

### 3. Documentation

- **README.md** with:
  - Setup instructions (including API key configuration)
  - CLI usage examples
  - Brief architecture overview

### 4. Configuration

- Example `.env.example` file with required variables
- Clear documentation of configuration options

## Technical Recommendations

### Suggested Libraries

| Purpose | Recommended Libraries |
|---------|----------------------|
| CLI Framework | `typer`, `click`, `argparse` |
| LLM Framework | `langchain`, `pydantic-ai`, `llamaindex` (all optional) |
| Vector Database | `lancedb` (simplest), `chromadb`, `qdrant-client` |
| Embeddings | `openai`, `sentence-transformers` |
| HTTP Client | `httpx`, `requests` |
| Configuration | `pydantic-settings`, `python-dotenv` |

### arXiv API Resources

- **arXiv API**: https://arxiv.org/help/api
- **Python Wrapper**: `arxiv` package (`pip install arxiv`)
- **Rate Limits**: Be mindful of arXiv API rate limits (3 seconds between requests)
- **Tip**: The `arxiv` package returns abstracts directly - no PDF parsing needed for core requirements

## Submission Process

1. **Add reviewers as collaborators**
   - Go to Settings → Collaborators
   - Add the provided reviewer accounts

2. **Finalize your code**
   - Ensure core features work
   - Run a final test of the RAG pipeline
   - Clean up debug code

3. **Update documentation**
   - Verify README is complete
   - Test setup instructions

4. **Push to repository**
   - Commit final changes
   - Verify everything is visible on GitHub

5. **Notify us**
   - Reply to the email with your repository link

## Tips for Success

- **Start with arXiv abstracts**: The `arxiv` Python package gives you abstracts directly - use these first
- **Use LanceDB**: It's the simplest vector database to set up (just a local file)
- **Test with real queries**: Use realistic questions researchers would ask
- **Keep it simple**: A working simple solution beats a broken complex one
- **Use AI tools**: They're allowed and encouraged - but understand the code
- **Ask questions**: Make reasonable assumptions and document them

## FAQ

**Q: Do I need to parse full PDF papers?**  
A: No, working with abstracts and metadata from arXiv API is sufficient for core requirements. PDF parsing is a bonus.

**Q: Which vector database should I use?**  
A: LanceDB is easiest (no server, just `pip install lancedb`). Chroma is also simple.

**Q: Do I need to use LangChain or similar?**  
A: No, a custom implementation is perfectly acceptable. Use frameworks only if you're comfortable with them.

**Q: How many papers should I ingest?**  
A: 30-50 papers is sufficient for demonstration.

**Q: Can I use local models instead of OpenAI?**  
A: Yes! Ollama with open-source models is a great cost-free option.

**Q: Should I implement all bonus features?**  
A: No, focus on core requirements first. Pick 1-2 bonus features only if you have time.

**Q: What Python version should I target?**  
A: Python 3.10+ is recommended.

---

## Final Note

This assessment evaluates your ability to build a working AI-powered system. We're looking for engineers who can:

- Build reliable AI-powered systems
- Make pragmatic architectural decisions
- Write clean, maintainable code
- Deliver working software within time constraints

**Remember**: A well-designed, working system with clean code demonstrates more skill than a complex system that's buggy or incomplete.

Good luck! We're excited to see what you build. 🚀
