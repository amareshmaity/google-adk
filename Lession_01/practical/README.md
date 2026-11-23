# Google Agent Development Kit (ADK) – Setup and Basic Commands

## 1. Create a Project Folder

Create a folder for your project and open it in VS Code.

```bash
mkdir google-adk-project
cd google-adk-project
code .
```

## 2. Create a Virtual Environment

```bash
python3 -m venv .venv
```

## 3. Activate the Virtual Environment

**Linux / macOS:**

```bash
source .venv/bin/activate
```

**Windows (PowerShell):**

```powershell
.venv\Scripts\Activate.ps1
```

## 4. Install Google ADK

```bash
pip install google-adk
```

## 5. Verify ADK Installation

Check the installed Google ADK version:

```bash
adk --version
```

## 6. Create an Agent Project


Use the following command to create a new agent project:

```bash
adk create demo_bot
```

This generates the initial project structure for your agent.

## 7. Get a Gemini API Key

1. Visit [Google AI Studio](https://aistudio.google.com/).
2. Sign in with your Google account.
3. Generate a Gemini API key.
4. Add the API key to the project's `.env` file.

Example:

```env
GOOGLE_API_KEY=your_gemini_api_key
```

**Important:** Never commit your `.env` file or expose your API key on GitHub.

## 8. Run the Agent

Run the agent directly from the terminal:

```bash
adk run demo_bot
```

## 9. Run the Web Interface

Launch the ADK web interface:

```bash
adk web
```

This provides a browser-based interface for interacting with and testing your agents.

## 10. Run the API Server

Start the ADK API server:

```bash
adk api_server
```

This allows you to interact with your agent through an API.

## 11. Run Google ADK with Other Models

Google ADK supports integration with other model providers through LiteLLM.

### Step 1: Install LiteLLM

```bash
pip install litellm
```

### Step 2: Configure the Model

Import `LiteLlm` and configure your agent to use an OpenAI model.

```python
from google.adk.models.lite_llm import LiteLlm

model = LiteLlm(model="openai/gpt-4o")
```

Alternatively, configure the model directly inside your agent:

```python
from google.adk.agents import Agent
from google.adk.models.lite_llm import LiteLlm

root_agent = Agent(
    name="campusx_bot",
    model=LiteLlm(model="openai/gpt-4o"),
    instruction="You are a helpful AI assistant."
)
```

### Step 3: Get an OpenAI API Key

1. Visit [OpenAI Platform](https://platform.openai.com/api-keys).
2. Generate an API key.
3. Add it to your `.env` file.

```env
OPENAI_API_KEY=your_openai_api_key
```

## 12. Configure Model Parameters

You can customize the model's generation behavior using `GenerateContentConfig`.

### Example

```python
from google.genai import types

generate_content_config = types.GenerateContentConfig(
    temperature=0.3,
    max_output_tokens=800
)
```

### Important Parameters

| Parameter           | Description                                                                               |
| ------------------- | ----------------------------------------------------------------------------------------- |
| `temperature`       | Controls randomness in generated responses. Lower values produce more consistent outputs. |
| `max_output_tokens` | Sets the maximum number of tokens the model can generate in a response.                   |

**Temperature guide:**

- `0.0–0.3`: More consistent and predictable responses.
- `0.4–0.7`: Balanced creativity and consistency.
- `0.8–1.0`: More creative and diverse responses.

### Using Configuration in an Agent

```python
from google.adk.agents import Agent
from google.genai import types

root_agent = Agent(
    name="campusx_bot",
    model="gemini-2.5-flash",
    instruction="You are a helpful AI assistant.",
    generate_content_config=types.GenerateContentConfig(
        temperature=0.3,
        max_output_tokens=800
    )
)
```

---

## 13. Quick Revision – Commands

| Task                       | Command                     |
| -------------------------- | --------------------------- |
| Create virtual environment | `python3 -m venv .venv`     |
| Activate (Linux/macOS)     | `source .venv/bin/activate` |
| Install Google ADK         | `pip install google-adk`    |
| Check ADK version          | `adk --version`             |
| Create agent               | `adk create campusx_bot`    |
| Run agent                  | `adk run campusx_bot`       |
| Start web interface        | `adk web`                   |
| Start API server           | `adk api_server`            |
| Install LiteLLM            | `pip install litellm`       |

## 14. Official Learning Resources

- [Google ADK Documentation](https://google.github.io/adk-docs/)
- [Google ADK Python Documentation](https://google.github.io/adk-docs/get-started/)
- [Google AI Studio](https://aistudio.google.com/)
- [OpenAI API Keys](https://platform.openai.com/api-keys)
- [LiteLLM Documentation](https://docs.litellm.ai/)
