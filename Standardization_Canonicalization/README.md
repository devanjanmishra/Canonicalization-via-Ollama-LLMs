# Standardization / Canonicalization
Mapping diverse phrasings like “slow service” and “the service was slow” to a single standardized label.
Formal names:
- Text Normalization
- Canonicalization
- Synonym Resolution / Clustering


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
    StdPos --> MapPos[Map to All Positive Points]
    CollectPos --> MapPos
    MapPos --> CatPos[Categorized Positive Points]

    SNeg --> StdNeg[Standardized Negative Points]
    StdNeg --> MapNeg[Map to All Negative Points]
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