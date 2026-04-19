# CreditIQ — Agentic Risk Intelligence Platform

**CreditIQ** is a next-generation credit risk assessment platform that bridges the gap between traditional machine learning and transparent, agentic AI. It transforms raw financial data into professional, auditable, and narrative risk reports using a custom **Plan-Execute-Reflect (PER)** framework.

---

## 🏗 System Architecture

The following diagram illustrates the relationship between the Streamlit interface, the Agentic Orchestrator, and the specialized tool ecosystem.

```mermaid
graph TD
    A[User Input] --> B[Streamlit UI]
    B --> C{Orchestrator}
    
    subgraph "Agentic Brain (agent_pipeline.py)"
        C --> D[Planner - Llama 8B]
        D --> E[Executor - Llama 70B/8B]
        E --> F[Reflector - Llama 8B]
        F --> G[Reporter - Llama 70B/8B]
    end
    
    subgraph "Tool Registry"
        E --> T1[ML Inference]
        E --> T2[Segment Scoring]
        E --> T3[Policy Engine]
        E --> T4[RAG Knowledge Base]
    end
    
    T4 --> DB[(ChromaDB)]
    G --> B
    B --> H[Professional Report]
```

---

## 🚀 Key Features

- **Dual-Mode Analysis**: Choose between "Lightning Prediction" (pure ML speed) and "Deep AI Analysis" (full agentic reasoning).
- **PER Framework**: A multi-agent orchestrator that **Plans**, **Executes**, **Reflects**, and **Reports**.
- **RAG-Powered Policy**: Integrated **ChromaDB** for real-time semantic search over credit rulebooks.
- **Ultra-Economy Resilience**: Automatic fallback logic that ensures analysis completion even during API rate limits.
- **Soft & Secure Reporting**: Financial-grade narrative generation with prompt-injection guardrails and jargon filtering.

---

## 🧠 The PER Pipeline Workflow

The Agentic Brain operates in four distinct phases to ensure transparency and logical consistency.

```mermaid
sequenceDiagram
    participant U as User/Streamlit
    participant P as Phase 1: Planner
    participant E as Phase 2: Executor
    participant R as Phase 3: Reflector
    participant RP as Phase 4: Reporter

    U->>P: Submit Applicant Data
    P->>P: Draft Analysis Strategy
    P->>E: JSON Plan & Target Tools
    
    loop Tool-calling Loop
        E->>E: Execute diagnostic tools
        E->>E: Update internal risk state
    end
    
    E->>R: Raw Execution Log
    R->>R: Audit consistency & logic
    R->>RP: Audited Decision Rationale
    
    RP->>RP: Draft Professional Narrative
    RP->>U: Final PDF-ready Report
```

---

## 🛡 Ultra-Economy Resilience

To handle restrictive Groq API rate limits (429 errors), CreditIQ implements a multi-layer resiliency strategy.

```mermaid
flowchart TD
    Start[Execute Agent Task] --> Strong[Attempt with Llama 70B]
    Strong -- Success --> End[Analysis Continues]
    Strong -- Error 429 / 400 --> Fallback[Switch to Llama 8B]
    Fallback --> Prune[Prune Context Length]
    Prune --> Retry[Retry Step]
    Retry --> End
```

| Feature | Description |
| :--- | :--- |
| **Hybrid Fallback** | Automatically switches from the large model to the small model if limits are reached. |
| **Context Pruning** | Intelligently removes old conversation history during the loop to keep token usage low. |
| **Multi-Model Routing** | Uses the cheaper 8B model for simple tasks (Planning/Auditing) to save "tokens per day." |

---

## 🛠 Tool Ecosystem

The Agent controls a specialized **Tool Registry** to perform deep diagnostics:

| Tool Name | Output | Role in Analysis |
| :--- | :--- | :--- |
| `preprocess_and_predict` | Decision, Prob, State | Core Machine Learning inference using a trained Decision Tree. |
| `score_applicant_segment` | Benchmarks, Score | Peer calculations (Income percentiles, DTI ratios). |
| `compute_risk_flags` | List of Flags, Severity | Hard-coded policy logic (e.g., minimum income or history). |
| `retrieve_credit_rules` | Semantic Policy Snippets | RAG-based search for relevant clauses from the credit policy. |
| `build_decision_rationale` | Structured JSON | Final summary that unites ML data with Qualitative policy findings. |

---

## 📁 Project Structure

- `app.py`: Streamlit frontend, state management, and plotting logic.
- `agent_pipeline.py`: The "Brain" of the system. Contains the PER logic, tool registry, and RAG configuration.
- `dt_model.pkl`: The current production ML model and preprocessing artifact.
- `requirements.txt`: Environment dependencies.
- `.streamlit/secrets.toml`: Local storage for the `GROQ_API_KEY`.

---

## ⚙️ Setup & Configuration

1. **Install Dependencies**: `pip install -r requirements.txt`
2. **Setup Secrets**: Add your key to `.streamlit/secrets.toml`.
3. **Run App**: `streamlit run app.py`

---
