# Multi-Provider GenAI CLI Chatbot

A lightweight, Python-based command-line chatbot that allows users to interact with multiple Large Language Model (LLM) providers through a single interface.

The application supports **OpenAI, Google Gemini, and Ollama**, allowing users to switch between cloud-based AI models and locally hosted language models through simple environment-based configuration.

## Overview

This project demonstrates how to integrate different Generative AI providers into a single Python application.

Users can select their preferred LLM provider, enter prompts through the terminal, and receive AI-generated responses directly in the command line.

### Architecture

```text
             User
               |
               v
         Python CLI
               |
               v
        Provider Selection
               |
       +-------+-------+
       |       |       |
       v       v       v
    OpenAI   Gemini  Ollama
    (Cloud)  (Cloud)  (Local)
       |       |       |
       +-------+-------+
               |
               v
       AI-Generated Response
               |
               v
            Terminal
```

## Features

- **Multi-Provider Support:** Integrates OpenAI, Google Gemini, and Ollama.
- **Provider Selection:** Choose an LLM provider through environment configuration without modifying the Python source code.
- **Custom System Prompt:** Configure the assistant's behavior using a customizable system prompt.
- **Secure API Key Management:** Uses environment variables and `python-dotenv` to keep API credentials outside the source code.
- **Local LLM Integration:** Supports locally running models through the Ollama HTTP API.
- **Interactive CLI:** Communicate with AI models directly through the terminal.
- **Command Support:** Includes `/help` and `/exit` commands.
- **Error Handling:** Provides helpful setup messages and handles request failures.

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| OpenAI API | Cloud-based LLM integration |
| Google Gemini API | Cloud-based LLM integration |
| Ollama | Local LLM integration |
| Requests | HTTP communication with Ollama |
| python-dotenv | Environment variable management |

## Project Structure

```text
multi-provider-genai-chatbot/
│
├── chatbot.py          # Main application and CLI interface
├── config.py           # Loads configuration from .env
├── providers.py        # Integrations for OpenAI, Gemini and Ollama
│
├── .env.example        # Environment configuration template
├── .gitignore          # Excludes sensitive and unnecessary files
├── requirements.txt    # Python dependencies
└── README.md           # Project documentation
```

## Getting Started

Follow these steps to set up and run the project locally.

### Prerequisites

- Python 3.9 or later
- pip (Python package installer)
- An API key for OpenAI or Google Gemini, or
- Ollama installed locally if you want to use a local LLM.

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/multi-provider-genai-chatbot.git
```

Navigate to the project directory:

```bash
cd multi-provider-genai-chatbot
```

### 2. Create a Virtual Environment

```bash
python -m venv .venv
```

Activate the virtual environment.

**Windows (PowerShell):**

```powershell
.venv\Scripts\Activate.ps1
```

**macOS / Linux:**

```bash
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a `.env` file by copying the provided example.

**Windows (PowerShell):**

```powershell
copy .env.example .env
```

**macOS / Linux:**

```bash
cp .env.example .env
```

Open the `.env` file and configure your preferred provider.

Choose **one provider** by setting `LLM_PROVIDER`.

## Provider Configuration

### Option 1: OpenAI

To use OpenAI:

1. Create an API key through the OpenAI Platform.
2. Add your API key and preferred model name to `.env`.

```env
LLM_PROVIDER=openai

OPENAI_API_KEY=your-api-key
OPENAI_MODEL=gpt-4o-mini

SYSTEM_PROMPT=You are a helpful AI assistant.
```

Use a model name that is currently available to your account.

### Option 2: Google Gemini

To use Google Gemini:

1. Generate an API key through Google AI Studio.
2. Add your credentials to `.env`.

```env
LLM_PROVIDER=gemini

GEMINI_API_KEY=your-api-key
GEMINI_MODEL=gemini-2.0-flash

SYSTEM_PROMPT=You are a helpful AI assistant.
```

Use a currently available Gemini model.

### Option 3: Ollama (Local LLM)

Ollama allows you to run language models locally on your computer without requiring a cloud API key.

**Step 1:** Install Ollama.

**Step 2:** Start Ollama and download a model.

For example:

```bash
ollama pull llama3.2
```

**Step 3:** Configure `.env`.

```env
LLM_PROVIDER=ollama

OLLAMA_BASE_URL=http://localhost:11434
OLLAMA_MODEL=llama3.2

SYSTEM_PROMPT=You are a helpful AI assistant.
```

Make sure Ollama is running before starting the chatbot.

The selected model must already be downloaded on your computer.

## Running the Application

Once the configuration is complete, run:

```bash
python chatbot.py
```

The chatbot will display the selected provider and model before starting the interactive session.

## Example Interaction

```text
========================================
      Simple GenAI CLI Chatbot
========================================

Provider: openai
Model: gpt-4o-mini
Type /help for commands.

You: Hello!

Assistant: Hello! How can I help you today?

You: Explain Python in simple words.

Assistant: Python is a programming language
that is easy to read and learn...

You: /help

Commands:
  /help   Show this help
  /exit   Quit the chatbot (you can also type: exit)

You: /exit

Goodbye!
```

*Note: The actual responses depend on the selected provider and model.*

## Configuration Reference

| Variable | Description |
|---|---|
| `LLM_PROVIDER` | Selects the provider: `openai`, `gemini`, or `ollama` |
| `SYSTEM_PROMPT` | Defines the assistant's behavior |
| `OPENAI_API_KEY` | OpenAI API credential |
| `OPENAI_MODEL` | OpenAI model name |
| `GEMINI_API_KEY` | Google Gemini API credential |
| `GEMINI_MODEL` | Gemini model name |
| `OLLAMA_BASE_URL` | Ollama server address |
| `OLLAMA_MODEL` | Locally installed Ollama model |

Only the credentials and model configuration for your selected provider are required.

## Error Handling & Troubleshooting

**1. API key is missing**

Example:

```text
Error: OPENAI_API_KEY is missing.
```

Make sure you have created the `.env` file and entered the correct API key.

**2. Invalid provider**

Example:

```text
LLM_PROVIDER is '...'
```

Set `LLM_PROVIDER` to one of the supported values:

- `openai`
- `gemini`
- `ollama`

**3. Model name is missing or invalid**

Check the corresponding model variable in `.env` and ensure that the model is available to your account or installed locally.

**4. Could not connect to Ollama**

Make sure Ollama is installed and running.

The default server address is:

```text
http://localhost:11434
```

**5. ModuleNotFoundError**

Install the required dependencies again:

```bash
pip install -r requirements.txt
```

Also ensure that your virtual environment is activated.

## Current Limitations

This is a learning-oriented project rather than a production-ready application.

Current limitations include:

- No conversation history or persistent memory between messages.
- No streaming responses.
- No tool calling or agent functionality.
- Only one provider can be selected at a time through configuration.
- API usage may incur charges depending on the selected cloud provider.

## Future Enhancements

Potential improvements for future versions:

- Conversation history and contextual memory.
- Streaming AI responses.
- Interactive provider switching.
- Support for additional LLM providers.
- Tool calling and function integration.
- Retrieval-Augmented Generation (RAG).
- Improved logging and structured error handling.

## Learning Outcomes

Through this project, I explored:

- Integrating Large Language Models using Python.
- Working with multiple AI provider APIs.
- Understanding cloud-based and locally hosted LLMs.
- Managing API credentials securely using environment variables.
- Sending prompts and processing AI-generated responses.
- Building an interactive command-line application.
- Organizing Python applications using modular programming.

## Security

- Never commit your actual `.env` file.
- Keep API keys private.
- Use `.env.example` as a configuration template.
- Avoid hardcoding credentials in source files.

---

**Built with Python and Generative AI.**