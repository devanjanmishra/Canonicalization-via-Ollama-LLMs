# Canonicalization-via-Ollama-LLMs
This function uses Ollama's Qwen3 language model to analyze a restaurant review and extract structured sentiment insights. It outputs a JSON containing:

- rating (integer, 0–5): The overall sentiment score.

- pain_points (list): Key negative aspects mentioned (if any).

- positive_points (list): Key positive aspects mentioned (if any).


```mermaid
flowchart TD
    A[Start] --> B[Receive review input]
    B --> C[Ollama tool call]
    C --> D1[Review Score]
    C --> D2[Positive Points]
    C --> D3[Pain Points]

```
