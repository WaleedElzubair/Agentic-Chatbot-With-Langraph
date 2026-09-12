# Agentic Chatbot with LangGraph

An interactive conversational AI application built with Streamlit, LangGraph, LangChain, and DeepSeek. The bot accepts messages through a web interface, sends the conversation to the DeepSeek chat model, and streams the response back to the user in real time.

## Overview

This project demonstrates how to build a stateful chatbot with a graph-based workflow. LangGraph manages the message state and execution flow, while Streamlit provides the user interface and displays the conversation.

The current workflow is intentionally simple and reliable:

```text
User message -> LangGraph state -> DeepSeek model -> Streamed response
```

Although the project is described as an agentic chatbot, the current implementation uses one model node. The graph structure makes it possible to add tools, routing, memory backends, validation, or additional agent nodes later.

## Features

- Interactive browser-based chat interface
- Real-time streaming of assistant responses
- Conversation message state managed by LangGraph
- In-memory checkpoints for the active application session
- DeepSeek `deepseek-chat` model integration
- Environment-based API key configuration with `python-dotenv`
- Simple graph architecture that can be extended with additional nodes and tools

## Technologies Used

| Technology | Purpose |
| --- | --- |
| Python | Application runtime |
| Streamlit | Web-based chat interface |
| LangGraph | Workflow and state management |
| LangChain Core | Standard message objects and model integration |
| ChatDeepSeek | Connection to the DeepSeek chat model |
| python-dotenv | Loading environment variables from `.env` |
| MemorySaver | In-memory graph checkpoints |

## Project Structure

```text
.
├── app.py                 # Streamlit interface and response streaming
├── chat_bot_backend.py    # LangGraph workflow and DeepSeek model setup
├── requirements.txt       # Python dependencies
├── README.md              # Project documentation
└── LICENSE                # License information
```

## Requirements

- Python 3.10 or newer
- A DeepSeek API key
- Internet access for model requests

## Installation

1. Open a terminal in the project directory.

2. Create a virtual environment:

	```powershell
	python -m venv .venv
	```

3. Activate the environment.

	**Windows PowerShell**

	```powershell
	.\.venv\Scripts\Activate.ps1
	```

	**macOS/Linux**

	```bash
	source .venv/bin/activate
	```

4. Install the dependencies:

	```bash
	pip install -r requirements.txt
	```

## Configuration

Create a file named `.env` in the project root and add your DeepSeek API key:

```env
DEEPSEEK_API_KEY=your_api_key
```

Replace `your_api_key` with a valid key. Keep the `.env` file private and do not commit it to source control.

## Run the Application

Start the Streamlit server from the project directory:

```bash
streamlit run app.py
```

Open the local URL shown in the terminal, then enter a message in the chat input.

## How the Bot Works

1. The user submits a message in the Streamlit interface.
2. The message is converted into a LangChain `HumanMessage`.
3. The message is passed to the compiled LangGraph workflow.
4. The `chat_node` sends the conversation state to DeepSeek.
5. The assistant response is streamed to the interface and added to the displayed message history.

The graph currently contains one node and two edges:

```text
START -> chat_node -> END
```

`MemorySaver` stores graph checkpoints in memory while the process is running. The current configuration uses a single thread ID, so the application is intended for local or single-session use.

## Limitations

- Conversation checkpoints are not persisted after the application stops.
- The current workflow contains one model node and does not use external tools.
- The default thread ID is shared by the running application.
- A valid DeepSeek API key and network connection are required.

For production use, consider adding persistent storage, user-specific thread IDs, authentication, error handling, and rate-limit protection.

## Troubleshooting

### API key errors

Verify that `.env` exists in the project root and contains `DEEPSEEK_API_KEY`. Restart the Streamlit process after changing the file.

### Import errors

Confirm that the virtual environment is active, then reinstall the dependencies:

```bash
pip install -r requirements.txt
```

### Port already in use

Start Streamlit on another port:

```bash
streamlit run app.py --server.port 8502
```

## License

See [LICENSE](LICENSE) for the applicable license terms.
# Agentic Chatbot with LangGraph

A Streamlit chat application powered by LangGraph and DeepSeek. Messages are processed through a simple graph workflow and streamed to the browser as the response is generated.

## Features

- Streamlit chat interface
- Streaming DeepSeek responses
- LangGraph message state management
- In-memory conversation checkpoints
- Environment-based API key configuration

## How It Works

`app.py` provides the user interface and streams responses from the compiled graph. `chat_bot_backend.py` defines the graph and sends the conversation messages to the DeepSeek chat model.

The graph contains one processing node:

```text
START -> chat_node -> END
```

`MemorySaver` keeps checkpoints in memory while the application is running. Conversation data is lost when the application restarts.

## Prerequisites

- Python 3.10 or newer
- A DeepSeek API key

## Setup

From the project directory, create and activate a virtual environment:

	**Windows PowerShell**

	```powershell
	python -m venv .venv
	.\.venv\Scripts\Activate.ps1
	```

	**macOS/Linux**

	```bash
	python3 -m venv .venv
	source .venv/bin/activate
	```

Install the project dependencies:

	```bash
	pip install -r requirements.txt
	```

## Configuration

Create a `.env` file in the project root and add your DeepSeek API key:

```env
DEEPSEEK_API_KEY=
```

The backend loads this value with `python-dotenv`. Do not commit `.env` or expose your API key in source control.

## Running the Application

Start the Streamlit application from the project root:

```bash
streamlit run app.py
```

Open the local URL printed by Streamlit, then send a message through the chat input.

## Project Structure

```text
.
├── app.py                 # Streamlit user interface
├── chat_bot_backend.py    # LangGraph workflow and DeepSeek integration
├── requirements.txt       # Python dependencies
├── README.md              # Project documentation
└── LICENSE                # License information
```

## Troubleshooting

### Missing API key

Confirm that `.env` exists in the project root and contains `DEEPSEEK_API_KEY`. Restart Streamlit after changing environment variables.

### Dependency errors

Ensure the virtual environment is active and reinstall the dependencies:

```bash
pip install -r requirements.txt
```

### Port in use

Run Streamlit on another port:

```bash
streamlit run app.py --server.port 8502
```

## License

See [LICENSE](LICENSE) for license details.

