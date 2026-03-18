# 📊 Agentic-Analyst

> **An intelligent Data Analyst Agent that accepts natural language questions, writes & executes SQL, visualizes results, and narrates insights — complete with autonomous self-correction capabilities.**

---

## 📖 Overview

**Agentic-Analyst** acts as an autonomous data analyst team member. When provided with a natural language question about a database, it intelligently inspects the schema, generates the appropriate SQL query, and safely executes it. 

If the query fails, the agent enters a **self-correction loop**, re-prompting itself with the error message to fix the syntax or logic until it succeeds. Upon a successful execution, the module passes the resulting dataframe to a plotting sub-agent to generate rich visualizations and produces a natural language narration of the key findings.

## 🛠️ Tech Stack

- **LLMs:** Claude / GPT-4o
- **Framework:** LangChain & autonomous pipelines
- **Databases:** PostgreSQL, SQLite
- **Data Processing:** Pandas
- **Visualization:** Matplotlib, Plotly
- **Frontend / UI:** Streamlit

## ✨ Core Features & How It Works

1. **Schema-Aware Generation:** The agent dynamically inspects the database schema (tables, columns, types) before attempting to construct an answer.
2. **Self-Correction Loop:** Generates SQL, executes it in a sandboxed/safe manner, catches errors, and iteratively fixes its own queries based on the database driver feedback.
3. **Multi-Modal Output:** Combines raw tabular data (SQL results), visual data (plots/charts), and textual summaries (insight narrations) in a single cohesive answer.

---

## 📂 Project Structure

```text
agents/                 # Core logic for specialized sub-agents
│   ├── question_parser.py   # Intent extraction and routing
│   ├── sql_agent.py         # SQL generation and self-correction
│   ├── plotter.py           # DataFrame visualization agent
│   └── narrator.py          # Insight generation and explanation
│
tools/                  # Interfaces to external systems
│   ├── db_connector/        # DB Clients (Postgres, SQLite)
│   ├── sql_executor.py      # Safe SQL execution
│   └── plotting/            # Matplotlib and Plotly adapters
│
workflows/              # Multi-agent coordination and state machines
│   ├── analyst_workflow.py  # Main pipeline: parse -> sql -> plot -> narrate
│   └── followup_workflow.py # Handling clarifications and drill-downs
│
app/                    # Application APIs and UI interfaces
│   ├── api/v1/              # Endpoint routing (e.g., FastAPI)
│   └── web/                 # Streamlit dashboard interface
│
data/                   # Local stores for samples and tests
│   ├── sample_schemas/      
│   └── test_queries/        
│
outputs/                # Generated reports and execution logs
│   └── runs/                
│
tests/                  # Unit and integration tests
config/                 # Environment configurations (dev, staging, prod)
```

## 🚀 Getting Started

### 1. Prerequisites
- Python 3.9+
- PostgreSQL or SQLite
- LLM API Keys (e.g., `OPENAI_API_KEY` or `ANTHROPIC_API_KEY`)

### 2. Installation
```bash
# Clone the repository
git clone https://github.com/your-username/Agentic-Analyst.git
cd Agentic-Analyst

# Install dependencies
pip install -r requirements.txt
```

### 3. Usage
Run the Streamlit application to start interacting with your new AI Data Analyst:
```bash
streamlit run app/web/app.py
```
*(Alternatively, you can test specific agents or API routes individually during development).*

---

## 🎯 Stretch Goals & Future Roadmap

- [ ] **Anomaly Detection Alerts:** Proactively monitor configured databases and send alerts for anomalous metric trends.
- [ ] **Scheduled Report Delivery:** Automatically generate, narrate, and email multi-modal reports on a set schedule (daily/weekly).
- [ ] **Drill-down Follow-up Questions:** Enable users to seamlessly ask follow-up questions that maintain deep context of previous SQL results.
