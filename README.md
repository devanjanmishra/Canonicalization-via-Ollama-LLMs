# 🧠 Text Quantization,NER,Standardization Pipeline

This repository implements a multi-step pipeline for understanding and structuring raw text (reviews, in this case). The goal is to move from **raw text** to **structured insights** through sentiment analysis, keyphrase extraction, and label standardization.
The entire workflow is carried out using Qwen3 LLM via Ollama, enabling tool call, ensuring structured output at the end.  
The workflow is implemented on Open Source _"yelp-restaurant-reviews"_ data, but can be extended to convert any raw text to ***quantified*** ***standardized*** ***structured*** output.  

---

## 📋 Pipeline Overview

The processing pipeline operates in **three main stages**:

### 1️⃣ [Basic Sentiment Analysis](./Basic_Sentiment_Analysis/sentiment_quantification.ipynb)
**Goal**: Rate the entire review on a scale from 0 (very negative) to 5 (very positive).

#### Theoretical Context:
- **Sentiment Analysis**: Assigning an overall polarity score to a review.
- Common techniques include zero-shot classification, review embedding, or trained sentiment classifiers.

---

### 2️⃣ [Quantitative Named Entity Recognition (NER)](./Quantitative_Named_Entity_Recognition/Named_Entity_Recogntion_Sentiment.ipynb)
**Goal**: Extract opinionated phrases like _"slow service"_ or _"great food"_, and identify references to specific entities (e.g., _"ice cream"_, _"burger"_).

#### Theoretical Context:
- **Keyphrase Extraction / Aspect Extraction**: Pulling out meaningful aspects from text.
- **Aspect-Based Sentiment Analysis (ABSA)**: Attaching sentiment to specific targets like _"food"_, _"service"_.
- **Opinion Mining**: Identifying subjective expressions.
- **Named Entity Recognition (NER)**: Capturing references to named items (e.g., dishes, products).

---

### 3️⃣ [Standardization / Canonicalization](./Standardization_Canonicalization/Standardization_of_Quantified_Results.ipynb)
**Goal**: Map diverse phrasings (e.g., _"the service was slow"_ vs _"slow service"_) to a single standardized label.

#### Theoretical Context:
- **Text Normalization / Canonicalization**: Reducing linguistic variance across extracted phrases.
- **Synonym Resolution / Clustering**: Grouping semantically similar expressions under unified tags.


## 📋 Pipeline Flow

```mermaid
flowchart TD
    A[Start] --> B[Receive Review Input]
    B --> C[Ollama Tool Call: Quantification & NER]
    C --> Pos[Positive Points]
    C --> Neg[Pain Points]

    Pos --> PosDishes[Positive Dishes]
    Pos --> PosOther[Other Positive Points]
    Neg --> NegDishes[Negative Dishes]
    Neg --> NegOther[Other Negative Points]

    PosOther --> CollectPos[Collect All Positive Points]
    NegOther --> CollectNeg[Collect All Negative Points]

    CollectPos --> SPos[Ollama Tool Call: Label Standardization - Positive]
    CollectNeg --> SNeg[Ollama Tool Call: Label Standardization - Negative]

    SPos --> StdPos[Standardized Positive Points]
    StdPos --> MapPos[Reduced/Standarized Positive Points]
    CollectPos --> MapPos
    MapPos --> CatPos[Categorized Positive Points]

    SNeg --> StdNeg[Standardized Negative Points]
    StdNeg --> MapNeg[Reduced/Standarized Negative Points]
    CollectNeg --> MapNeg
    MapNeg --> CatNeg[Categorized Negative Points]

    %% Dotted box: NER phase
    subgraph NER [ Named Entity Recognition ]
        style NER stroke-dasharray: 5
        Pos
        Neg
        PosDishes
        PosOther
        NegDishes
        NegOther
    end

    %% Encircle Standardization & Categorization process
    subgraph Standardization [ Point Standardization & Categorization ]
        style Standardization stroke: #999,stroke-width:2px
        PosOther
        NegOther
        CollectPos
        CollectNeg
        SPos
        SNeg
        StdPos
        StdNeg
        MapPos
        MapNeg
        CatPos
        CatNeg
    end

    %% Apply class to important nodes
    class C,SPos,SNeg highlight;

    %% Define highlight class with dark grey background and white text
    classDef highlight fill:#333,stroke:#fff,stroke-width:2px,color:#fff,font-weight:bold;

```

## Sample Output:
A **structured JSON** representation of the review, including:
```json
{
  "rating": 4,
  "positive_points": ["delicious food", "friendly staff"],
  "pain_points": ["slow service"],
  "categories": {
    "food": ["delicious food"],
    "service": ["slow service"]
  }
}
```
![Sample Output ](./sample_word_cloud.jpg)