# Sentiment & Basic Quantification
This function uses Ollama's Qwen3 language model to analyze a restaurant review and extract structured sentiment insights. It outputs a JSON containing:

- rating (integer, 0–5): The overall sentiment score.

- pain_points (list): Key negative aspects mentioned (if any).

- positive_points (list): Key positive aspects mentioned (if any).


```mermaid
flowchart TD
    A[Start] --> B[Receive review input]
    B --> C[Ollama Tool Call: Sentiment & Basic Quantification]
    C --> D1[Review Score]
    C --> D2[Positive Points]
    C --> D3[Pain Points]

    %% Apply class to important nodes
    class C, highlight;

    %% Define highlight class with dark grey background and white text
    classDef highlight fill:#333,stroke:#fff,stroke-width:2px,color:#fff,font-weight:bold;

```
