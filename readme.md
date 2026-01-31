graph TB
    subgraph "PRESENTATION LAYER"
        UI1[Streamlit Web UI<br/>Interactive Dashboard]
        UI2[CLI Interface<br/>orchestrator.py]
    end

    subgraph "ORCHESTRATION LAYER"
        ORCH[Pipeline Orchestrator<br/>8-Step Sequential Execution]
    end

    subgraph "PROCESSING LAYER"
        ANALYZE[1. Analyzer<br/>File Scan & AST]
        CONVERT[2. Converter<br/>AI + Cache]
        GENERATE[3. Generator<br/>File Org]
        PYTEST[4. Python Tests<br/>Validation]
        GOTEST[5. Go Tests<br/>WSL Exec]
        COMPARE[6. Comparator<br/>Match Check]
        DECIDE[7. Decision<br/>Pass/Fail]
        REPORT[8. Reporter<br/>JSON Report]
    end

    subgraph "DATA LAYER"
        REDIS[(Redis Cache<br/>Conversions)]
        FS[(File System<br/>modern/ Output)]
        LOGS[(Logs<br/>Audit Trail)]
    end

    subgraph "EXTERNAL SERVICES"
        GROQ[Groq API<br/>LLM Service]
        WSL[WSL<br/>Go Runtime]
    end

    UI1 --> ORCH
    UI2 --> ORCH
    
    ORCH --> ANALYZE
    ANALYZE --> CONVERT
    CONVERT --> GENERATE
    GENERATE --> PYTEST
    PYTEST --> GOTEST
    GOTEST --> COMPARE
    COMPARE --> DECIDE
    DECIDE --> REPORT
    
    CONVERT <--> REDIS
    CONVERT <--> GROQ
    GENERATE --> FS
    GOTEST <--> WSL
    ORCH --> LOGS
    REPORT --> FS

    classDef uiLayer fill:#3b82f6,stroke:#1e40af,color:#fff,stroke-width:3px
    classDef orchLayer fill:#8b5cf6,stroke:#6d28d9,color:#fff,stroke-width:3px
    classDef processLayer fill:#10b981,stroke:#059669,color:#fff,stroke-width:2px
    classDef dataLayer fill:#f59e0b,stroke:#d97706,color:#fff,stroke-width:2px
    classDef externalLayer fill:#ef4444,stroke:#dc2626,color:#fff,stroke-width:2px

    class UI1,UI2 uiLayer
    class ORCH orchLayer
    class ANALYZE,CONVERT,GENERATE,PYTEST,GOTEST,COMPARE,DECIDE,REPORT processLayer
    class REDIS,FS,LOGS dataLayer
    class GROQ,WSL externalLayer
