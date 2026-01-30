# Langflow to Python ADK Conversion

Production-ready Python implementation of the Langflow workflow design (LEOAZR_M74854_M74854.json).

## Overview for agent code.

This package converts a Langflow graph (nodes + edges) into an executable LangGraph workflow using modern libraries:
- `langchain-core` and `langchain-openai` for LLM integration
- `langgraph` for agentic workflow orchestration
- `pydantic` v2 for configuration and state management

## Workflow Design

The workflow implements a Multi-Purpose Agent with database query capabilities:

1. **ChatInput** - Captures user input
2. **Prompt Template** - Formats comprehensive system prompt for multi-scenario handling
3. **Azure OpenAI Model** - LLM processing with Azure deployment
4. **MCP Tools** - Model Context Protocol tools (placeholder in phase-1)
5. **Agent** - ReAct agent with tool integration
6. **ChatOutput** - Final response formatting

## Project Structure

```
essedum-pipeline-agent/
├── src/
│   ├── __init__.py              # Package initialization
│   ├── workflow_state.py        # Pydantic state model
│   ├── config.py                # Configuration with Azure/OpenAI support
│   ├── nodes.py                 # Node implementations
│   ├── graph_builder.py         # LangGraph workflow builder
│   └── main.py                  # CLI entry point
├── requirements.txt             # Dependencies
├── LEOAZR_M74854_M74854.json   # Original Langflow design
└── .env                         # Environment configuration (create this)
```

## Setup

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Configure Environment

Create a `.env` file in the project root:

```env
# Azure OpenAI (recommended)
AZURE_OPENAI_API_KEY=your-azure-api-key
AZURE_OPENAI_ENDPOINT=https://your-resource.openai.azure.com/
AZURE_OPENAI_DEPLOYMENT=your-deployment-name
AZURE_API_VERSION=2024-06-01

# OR OpenAI (fallback)
OPENAI_API_KEY=your-openai-api-key

# Optional settings
MODEL_NAME=gpt-4
TEMPERATURE=0.7
LOG_LEVEL=INFO
```

### 3. Run the Workflow

```bash
python src/main.py
```

With debug logging:

```bash
python src/main.py --debug
```

With custom design file:

```bash
python src/main.py --design-file path/to/design.json
```

## Usage

The CLI starts an interactive session:

```
Enter your question: What is machine learning?
Assistant: [AI response...]

Enter your question: SELECT * FROM users WHERE role='admin';
Assistant: [Database query results...]

Enter your question: quit
```

## Phase-1 Limitations

- **No conditional branching**: If routers/conditions exist in the design, only the first path is executed
- **MCP Tools**: Placeholder implementation; full MCP server integration pending
- **Linear workflow**: All nodes execute in sequence based on edge order

## Node Functions

Generated node functions from Langflow design:

- `node_chatinput_vip4f` - User input capture
- `node_prompt_template_t2vsf` - Prompt formatting with multi-scenario logic
- `node_mcp_ufeql` - MCP tools integration (stub)
- `node_azureopenaimodel_6aodl` - Azure OpenAI LLM invocation
- `node_agent_zgq5d` - ReAct agent with tool execution
- `node_chatoutput_avpjo` - Final output formatting

## Error Handling

All nodes implement comprehensive error handling:
- Graceful fallbacks for missing inputs
- ASCII-only logging (Windows-safe)
- State propagation with error tracking
- Non-crashing workflow execution

## Development

### Running Tests

```bash
python -m pytest tests/
```

### Logging

Set `LOG_LEVEL=DEBUG` in `.env` for detailed execution traces.

### Extending

To add custom nodes:
1. Create node function in `src/nodes.py`
2. Register in `node_function_map` in `src/graph_builder.py`
3. Update `WorkflowState` if new fields are needed

## License

Production-ready conversion for enterprise deployment.
