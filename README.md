# LLM Text Generation and Summarization

## About the Project

This project demonstrates how to interact with a Large Language Model (LLM) using an OpenAI-compatible Python SDK.

The project covers three important Natural Language Processing (NLP) tasks:

- **Text Generation**
- **Output Customization using LLM Parameters**
- **Text Summarization through Keyword Extraction**

The notebook demonstrates how prompt engineering, temperature control, and few-shot prompting can influence the behavior of an LLM.

---

# Project Overview

The project follows the complete lifecycle of an LLM application:

1. Configure the API connection.
2. Send prompts to an LLM.
3. Generate text responses.
4. Control creativity and response length.
5. Extract important keywords from documents using few-shot prompting.

---

# Technologies Used

- Python
- OpenAI Python SDK
- OpenAI-Compatible API
- Large Language Models (LLMs)
- Prompt Engineering
- Few-Shot Learning
- Natural Language Processing (NLP)
- Environment Variables

---

# Project Workflow

```
+------------------------------------------+
|          START: Initialize Project       |
+------------------------------------------+
                    |
                    v
+------------------------------------------+
| Step 1: Import Required Libraries        |
| - OpenAI SDK                             |
| - OS Module                              |
+------------------------------------------+
                    |
                    v
+------------------------------------------+
| Step 2: Configure API                    |
| - Store API Key                          |
| - Retrieve API Key                       |
| - Initialize LLM Client                  |
+------------------------------------------+
                    |
                    v
+------------------------------------------+
| Step 3: Text Generation                  |
| - Provide User Prompt                    |
| - Send Request to LLM                    |
| - Generate Response                      |
+------------------------------------------+
                    |
                    v
+------------------------------------------+
| Step 4: Customize Output                 |
| - Change max_tokens                      |
| - Adjust temperature                     |
| - Compare Different Outputs              |
+------------------------------------------+
                    |
                    v
+------------------------------------------+
| Step 5: Text Summarization               |
| - System Instructions                    |
| - Few-shot Examples                      |
| - Extract Keywords                       |
+------------------------------------------+
                    |
                    v
+------------------------------------------+
|              FINAL OUTPUT                |
| Generated Text / Extracted Keywords      |
+------------------------------------------+
                    |
                    v
+------------------------------------------+
|             END OF PROJECT               |
+------------------------------------------+
```

---

# API Configuration

## Import Libraries

The project starts by importing the required libraries.

```python
from openai import OpenAI
import os
```

---

## Configure API Key

The API key is stored using environment variables instead of directly writing credentials inside the code.

```python
os.environ["Your_llm_model_API_KEY"] = "<Your_API_Key>"
```

Retrieve the API key:

```python
api_key = os.getenv("Your_llm_model_API_KEY")
```

Initialize the client:

```python
client = OpenAI(
    base_url="https://Your_llm_model_API_KEY/api/",
    api_key=api_key
)
```

---

# 1. Text Generation

## Description

The text generation function sends a user prompt to the LLM and returns the generated response.

## Function

```python
def generate_text(prompt):

    response = client.chat.completions.create(
        model="Your_llm_model",

        messages=[
            {
                "role": "user",
                "content": prompt
            }
        ],

        max_tokens=100,
        temperature=0.7
    )

    content = response.choices[0].message.content

    if content:
        return content.strip()

    return "No response generated"
```

---

## Example

Input:

```python
prompt = "Once upon a time"

generated_text = generate_text(prompt)

print(generated_text)
```

Output:

```text
...in a kingdom tucked between the folds of two shimmering mountains,
there lived a clockmaker named Elias who didn't build clocks to tell the time.
Instead, he built clocks that captured moments.
```

---

# 2. Customizing the Output

## Description

LLM responses can be controlled by modifying generation parameters.

The two important parameters are:

### max_tokens

Controls the maximum length of the response.

### temperature

Controls creativity:

- Lower temperature → More predictable output
- Higher temperature → More creative output

---

## Function

```python
def generate_text(prompt, max_tokens, temperature):

    response = client.chat.completions.create(

        model="Your_llm_model",

        messages=[
            {
                "role": "user",
                "content": prompt
            }
        ],

        max_tokens=max_tokens,
        temperature=temperature
    )


    content = response.choices[0].message.content

    if content:
        return content.strip()

    return "Model returned empty response"
```

---

## Testing Different Temperatures

### Temperature = 0

```python
generate_text(prompt, 50, 0)
```

Example:

```text
Okay, the user just said "Once upon a time" and nothing else.
```

---

### Temperature = 1

```python
generate_text(prompt, 50, 1)
```

Example:

```text
Model returned empty response
```

Different LLM providers may produce different results depending on model configuration.

---

# 3. Text Summarization (Keyword Extraction)

## Description

This project uses the LLM to extract important keywords from a long text passage.

The model receives:

- System instruction
- Few-shot examples
- User text

This teaches the model the expected output format.

---

## Function

```python
def text_summarizer(prompt):

    response = client.chat.completions.create(

        model="Your_llm_model",

        messages=[

            {
                "role": "system",
                "content":
                "You will be provided with a block of text, "
                "and your task is to extract a list of keywords from it."
            },


            {
                "role": "user",
                "content": prompt
            }

        ],

        temperature=0.5,
        max_tokens=256
    )


    return response.choices[0].message.content.strip()
```

---

## Example

Input:

```text
Master Reef Guide Kirsty Whitman didn't need to tell me twice.
Peering down through my snorkel mask...
```

Output:

```text
Master Reef Guide,
Kirsty Whitman,
snorkel mask,
manta ray,
male manta ray,
female manta ray,
mating behavior,
potential mate,
snorkelling safari,
undersea ballet,
reef ecosystem.
```

---

# Prompt Engineering Approach

This project uses:

## System Prompt

Defines the task.

Example:

```text
Extract important keywords from the provided text.
```

---

## Few-Shot Prompting

Examples are provided to show the model the expected response format.

Example:

Input:

```text
Article text
```

Expected output:

```text
keyword1, keyword2, keyword3
```

The model learns the required format before processing new input.

---

# Repository Structure

```
LLM-Text-Generation-and-Summarization/

│
├── LLM_Text_Generation_and_Summarization.ipynb
│
├── README.md
│
├── requirements.txt
│
└── .gitignore
```

# Sample Results

## Generated Text

Prompt:

```text
Once upon a time
```

Generated:

```text
...in a kingdom tucked between two shimmering mountains,
there lived a clockmaker named Elias...
```

---

## Extracted Keywords

Input:

```text
Article describing manta rays and marine exploration.
```

Output:

```text
Kirsty Whitman,
manta ray,
snorkel mask,
mating behavior,
potential mate,
undersea ballet,
reef ecosystem.
```

---

# Conclusion

This project demonstrates how Large Language Models can be used for different NLP applications.

By controlling prompts and generation parameters, the same LLM can perform creative text generation and structured information extraction.

The project provides a foundation for building advanced AI applications such as:

- Document summarization systems
- AI assistants
- Content generation tools
- Knowledge extraction pipelines
- Retrieval-Augmented Generation (RAG) applications
