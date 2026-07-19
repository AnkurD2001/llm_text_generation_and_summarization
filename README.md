# LLM Text Generation and Summarization

## About the Project

This project demonstrates how to interact with a Large Language Model (LLM) using the OpenAI-compatible Python SDK. It showcases three fundamental Natural Language Processing (NLP) tasks:

- Text Generation
- Output Customization using model parameters
- Keyword Extraction (Text Summarization)

The notebook walks through configuring an API client, generating text from prompts, controlling the model's creativity using parameters, and extracting keywords from long passages using prompt engineering and few-shot learning.

---

# Project Overview

The notebook is organized into the following sections:

### 1. API Configuration
- Import required libraries.
- Store API credentials securely using environment variables.
- Initialize the OpenAI-compatible client.

### 2. Text Generation
Generate text from a user prompt using a chat completion model.

Example:

**Prompt**

```text
Once upon a time
```

**Output**

```text
...in a kingdom tucked between the folds of two shimmering mountains, there lived a clockmaker named Elias...
```

---

### 3. Customizing the Output

This section demonstrates how model parameters affect the generated response.

Parameters used:

- `max_tokens`
- `temperature`

Examples:

### Temperature = 0

Produces more deterministic and predictable output.

```python
generate_text(prompt, 50, 0)
```

Example Output

```text
Okay, the user just said "Once upon a time" and nothing else...
```

---

### Temperature = 1

Produces more creative responses.

```python
generate_text(prompt, 50, 1)
```

Example Output

```text
Model returned empty response
```

> **Note:** Depending on the selected LLM provider and model, highly creative settings may occasionally return empty responses or truncated outputs.

---

### 4. Text Summarization (Keyword Extraction)

Instead of generating free-form summaries, the model is instructed to extract the most important keywords from a block of text.

The implementation uses:

- System Prompt
- Few-shot Prompting
- Chat Completion API

Example Input

```text
Master Reef Guide Kirsty Whitman didn't need to tell me twice...
```

Example Output

```text
Master Reef Guide,
Kirsty Whitman,
snorkel mask,
manta ray,
male manta ray,
female manta ray,
mating behavior,
potential mate,
undersea ballet,
reef ecosystem.
```

---

# Technologies Used

- Python
- OpenAI Python SDK
- OpenAI-compatible API
- Prompt Engineering
- Few-shot Learning
- Environment Variables

---

# Project Workflow

```text
+------------------------------------------+
|        START: Initialize Project         |
+------------------------------------------+
                    |
                    v
+------------------------------------------+
| Cell 1 & 2: Import Libraries             |
| (OpenAI SDK, OS Module)                  |
+------------------------------------------+
                    |
                    v
+------------------------------------------+
| Cell 3: Configure API                    |
| - Store API Key                          |
| - Retrieve Environment Variable          |
| - Initialize OpenAI Client               |
+------------------------------------------+
                    |
                    v
+------------------------------------------+
| Cell 4: Generate Text                    |
| - User Prompt                            |
| - Chat Completion API                    |
| - Display Generated Text                 |
+------------------------------------------+
                    |
                    v
+------------------------------------------+
| Cell 5: Customize Output                 |
| - Adjust max_tokens                      |
| - Adjust temperature                     |
| - Compare Generated Results              |
+------------------------------------------+
                    |
                    v
+------------------------------------------+
| Cell 6: Text Summarization               |
| - System Prompt                          |
| - Few-shot Examples                      |
| - Extract Keywords                       |
+------------------------------------------+
                    |
                    v
+------------------------------------------+
|           OUTPUT: Keywords               |
|      or Generated Text Response          |
+------------------------------------------+
                    |
                    v
+------------------------------------------+
|             END OF PROJECT               |
+------------------------------------------+
```

---

# Notebook Structure

## Cell 1 — Import Libraries

**Explanation**

Imports the required libraries for communicating with the language model.

```python
from openai import OpenAI
import os
```

---

## Cell 2 — Configure Environment

**Explanation**

Stores the API key securely using an environment variable.

```python
os.environ["Your_llm_model_API_KEY"] = "<Your_API_Key>"
```

---

## Cell 3 — Initialize Client

**Explanation**

Retrieves the API key and initializes the OpenAI-compatible client.

```python
api_key = os.getenv("Your_llm_model_API_KEY")

client = OpenAI(
    base_url="https://Your_llm_model_API_KEY/api/",
    api_key=api_key
)
```

---

## Cell 4 — Text Generation

**Explanation**

Defines a function that sends a user prompt to the language model and returns generated text.

```python
def generate_text(prompt):
```

The function allows users to generate text from any prompt.

---

## Cell 5 — Customizing Output

**Explanation**

This version of the function exposes two configurable parameters:

- `max_tokens`
- `temperature`

```python
def generate_text(prompt, max_tokens, temperature):
```

This demonstrates how output length and creativity can be controlled.

---

## Cell 6 — Text Summarization

**Explanation**

Uses prompt engineering and few-shot examples to teach the model how to extract keywords from lengthy documents.

The workflow includes:

- System instruction
- Demonstration examples
- User input
- Keyword extraction

---

# Key Features

- Secure API configuration
- Text generation using chat completions
- Configurable creativity through temperature
- Adjustable response length
- Few-shot prompting
- Keyword extraction from long documents
- Prompt engineering techniques

---

# Sample Results

### Text Generation

**Prompt**

```text
Once upon a time
```

**Generated Output**

```text
...in a kingdom tucked between the folds of two shimmering mountains...
```

---

### Keyword Extraction

**Input**

Long article describing manta rays and reef exploration.

**Output**

```text
Master Reef Guide,
Kirsty Whitman,
snorkel mask,
manta ray,
male manta ray,
female manta ray,
mating behavior,
potential mate,
undersea ballet,
reef ecosystem.
```

---

# Conclusion

This project demonstrates the practical use of an OpenAI-compatible Large Language Model for multiple NLP tasks. It illustrates how prompt engineering and adjustable generation parameters influence model behavior, while also showcasing keyword extraction through few-shot learning. These examples provide a solid foundation for building more advanced AI-powered applications such as document analysis, summarization tools, chat assistants, and content generation systems.
