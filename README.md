# LangChain Tutorial - Setup and Configuration

This repository contains comprehensive tutorials on LangChain Agents and a BonBon FAQ Chatbot assignment.

## Prerequisites

- Python 3.11+
- Azure OpenAI account with API credentials
- Conda or virtual environment manager

## Installation

### 1. Create and Activate Environment

Using Conda:
```bash
conda create -n langchain-training python=3.11
conda activate langchain-training
```

Or using venv:
```bash
python -m venv langchain-training
source langchain-training/bin/activate  # On macOS/Linux
# or
langchain-training\Scripts\activate  # On Windows
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure Azure OpenAI Credentials

1. Copy the example environment file:
   ```bash
   cp .env.example .env
   ```

2. Open `.env` and update with your Azure OpenAI credentials:
   ```
   AZURE_OPENAI_ENDPOINT=https://your-resource-name.openai.azure.com/
   AZURE_OPENAI_KEY=your-api-key-here
   AZURE_OPENAI_API_VERSION=2024-02-15-preview
   AZURE_OPENAI_DEPLOYMENT_NAME=gpt-4  # Your chat model deployment
   AZURE_OPENAI_EMBEDDING_DEPLOYMENT=text-embedding-3-small  # Your embedding model deployment
   ```

3. **Important:** Make sure your Azure OpenAI resource has both:
   - A chat model deployed (e.g., gpt-4, gpt-35-turbo)
   - An embedding model deployed (e.g., text-embedding-3-small, text-embedding-ada-002)

## Project Structure

```
├── notebooks/
│   ├── Agent.ipynb              # Comprehensive LangChain Agents tutorial
│   ├── LangChainTutorial.ipynb  # Basic LangChain tutorial
│   ├── VectorEmbeddings.ipynb   # Vector embeddings tutorial
│   ├── AzureAISearch.ipynb      # Azure AI Search integration
│   └── demo.ipynb               # Demo notebook
├── BonBon_Assignment/
│   ├── assignment.ipynb         # BonBon FAQ chatbot assignment
│   └── data/
│       └── BonBon FAQ.pdf       # FAQ document for assignment
├── requirements.txt             # Python dependencies
├── .env.example                 # Example environment configuration
└── README.md                    # This file
```

## Running the Notebooks

### Agent Tutorial (notebooks/Agent.ipynb)

This notebook provides a comprehensive guide to LangChain Agents, covering:
- Basic agent setup with Azure OpenAI
- Custom tools creation using `@tool` decorator
- Built-in tools (Wikipedia, DuckDuckGo search)
- ReAct agents with custom prompts
- Agent memory using LangGraph's MemorySaver
- Research assistant example
- Best practices and use cases

**To run:**
1. Open `notebooks/Agent.ipynb` in VS Code
2. Select the `langchain-training` kernel
3. Run cells sequentially
4. All 21 code cells should execute successfully

### BonBon Assignment (BonBon_Assignment/assignment.ipynb)

This assignment implements an IT support chatbot using the BonBon FAQ document.

**Assignment Components:**
1. **Document Indexing** - Loads, splits, embeds, and stores FAQ document in Chroma vector database
2. **Conversational Chatbot** - ReAct agent with:
   - Knowledge base search tool (retrieves from vector database)
   - Internet search tool (uses DuckDuckGo as fallback)
   - Conversation memory (maintains context across messages)
   - Source citation (includes page numbers from FAQ)

**To run:**
1. Ensure `.env` is configured with your Azure credentials
2. Open `BonBon_Assignment/assignment.ipynb`
3. Select the `langchain-training` kernel
4. Run all cells sequentially
5. Test with the provided test cases

## Troubleshooting

### Common Issues

1. **ModuleNotFoundError**
   - Solution: Ensure all packages are installed: `pip install -r requirements.txt`
   - Make sure you're using the correct environment

2. **Azure OpenAI 404 Error (DeploymentNotFound)**
   - Solution: Verify your deployment names in `.env` match your actual Azure deployments
   - Check that both chat and embedding models are deployed in your Azure resource
   - Wait 5 minutes if you just created the deployment

3. **ImportError for langchain modules**
   - Solution: The notebooks use LangChain 1.1.3+ with LangGraph architecture
   - Old tutorials may use deprecated imports like `AgentExecutor` or `create_openai_functions_agent`
   - Modern approach: Use `create_react_agent` from `langgraph.prebuilt`

4. **DuckDuckGo Search Errors**
   - Solution: The notebooks include graceful error handling
   - If `ddgs` package is missing, it will show a warning but continue
   - Install with: `pip install ddgs>=6.0.0`

5. **Memory/Checkpoint Issues**
   - Solution: Use `MemorySaver` from `langgraph.checkpoint.memory`
   - Old approach using `ConversationBufferMemory` is deprecated
   - Message format: `{"messages": [("human", "text")]}`

## Package Versions

Key packages (see requirements.txt for complete list):
- langchain >= 0.3.0
- langchain-openai >= 0.2.0
- langchain-community >= 0.3.0
- langgraph >= 0.2.0
- chromadb >= 0.4.0
- pypdf >= 3.17.0

## Additional Resources

- [LangChain Documentation](https://python.langchain.com/)
- [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)
- [Azure OpenAI Service](https://azure.microsoft.com/en-us/products/ai-services/openai-service)

## Support

If you encounter issues:
1. Check that `.env` is properly configured
2. Verify Azure deployments exist and are accessible
3. Ensure all dependencies are installed
4. Check Python version (3.11+ recommended)

## License

This project is for educational purposes.
