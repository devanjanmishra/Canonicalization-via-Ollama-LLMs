# Keyphrase Extraction / Aspect Extraction
Keyphrase Extraction / Aspect Extraction : Extracting phrases like “slow service” or “great food” from text.
Formal names:
- Aspect-Based Sentiment Analysis (ABSA): Assigning sentiment to specific aspects (e.g., “food”, “service”).
- Opinion Mining: Finding subjective expressions in text.
- Named Entity Recognition (NER) (if it's targeting named items like “ice cream” or “burger”)

```mermaid
flowchart TD
    A[Start] --> B[Receive review input]
    B --> C[Ollama Tool Call : Quantification & NER]
    C --> D1[Review Score]
    C --> D2[Positive Points]
    C --> D3[Pain Points]
    D2 --> E21[Positive Dishes]
    D2 --> E22[Positive Points except Dishes]
    D3 --> E31[Negative Dishes]
    D3 --> E32[Negative Points except Dishes]

    %% Add dotted box
    subgraph Sentiment Analysis [ Named Entity Recognition NER]
        style Sentiment Analysis stroke-dasharray: 5
        D2
        D3
        E21
        E22
        E31
        E32
    %% Apply class to important nodes
    class C, highlight;

    %% Define highlight class with dark grey background and white text
    classDef highlight fill:#333,stroke:#fff,stroke-width:2px,color:#fff,font-weight:bold;
    end
```
