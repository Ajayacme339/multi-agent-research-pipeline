# Multi-Agent Research Pipeline

An automated research pipeline built with the [OpenAI Agents SDK](https://openai.github.io/openai-agents-python/). Give it a question and it goes end to end — search the web, analyze the findings, and write a polished executive report — with no manual steps.

Everything lives in [`multi_agent_workflows.ipynb`](multi_agent_workflows.ipynb).

## How it works

Three single-skill agents are chained by an async `manager_run(query)` function. They share one `SQLiteSession` so each step builds on a common memory of the run.

```
                 ┌─────────────┐   research   ┌──────────┐   analysis   ┌────────┐
  user query ──▶ │  Researcher │ ───────────▶ │  Analyst │ ───────────▶ │ Writer │ ──▶ ResearchReport
                 └─────────────┘              └──────────┘              └────────┘
                       │                                                     │
                  tavily_search                                        short_summary
                  (web search)                                         markdown_report (500+ words)
                                                                       follow_up_questions (3–5)
```

| Agent | Model | Tools | Output | Job |
|-------|-------|-------|--------|-----|
| **Researcher** | `gpt-5-mini` | `tavily_search` | `Report` | Gather real-time facts; return ≤ 5 bullet points |
| **Analyst** | `gpt-5-mini` | none | `Report` | Extract trends / risks / insights in 2 paragraphs |
| **Writer** | `gpt-5-mini` | none | `ResearchReport` | Produce a polished executive report |

Data flows through Pydantic models (`Report`, `ResearchReport`), so each agent's output feeds cleanly into the next.

## Setup

1. **Clone and enter the repo**

   ```bash
   git clone https://github.com/Ajayacme339/multi-agent-research-pipeline.git
   cd multi-agent-research-pipeline
   ```

2. **Create a virtual environment** (Python 3.13 recommended)

   ```bash
   python -m venv .venv
   # Windows:  .venv\Scripts\activate
   # macOS/Linux:  source .venv/bin/activate
   ```

3. **Install dependencies**

   ```bash
   pip install openai-agents python-dotenv requests ipykernel
   ```

4. **Add your API keys** — copy the template and fill it in:

   ```bash
   cp .env.example .env
   ```

   ```dotenv
   OPENAI_API_KEY=sk-...
   TAVILY_API_KEY=tvly-...
   ```

   Get keys from [OpenAI](https://platform.openai.com/api-keys) and [Tavily](https://tavily.com/).

## Usage

Open `multi_agent_workflows.ipynb`, select the Python 3.13 kernel, and run the cells top to bottom. To run the full pipeline on your own question:

```python
report = await manager_run("What is the public sentiment about <your topic>?")

print(report.short_summary)
for q in report.follow_up_questions:
    print("-", q)
# report.markdown_report holds the full write-up
```

## Project layout

| Path | What it is |
|------|-----------|
| `multi_agent_workflows.ipynb` | The full pipeline: tool, agents, `manager_run`, tests |
| `.env.example` | Template for the required API keys |
| `.agents/skills/openai-agents-sdk/` | Reference docs for the OpenAI Agents SDK |
| `prompt_*.md` | The step-by-step prompts used to build the notebook |

## Notes

- Requires network access and valid OpenAI + Tavily keys — each pipeline run makes real API calls (three agent runs plus web searches), which incur cost.
- `.env` is git-ignored; never commit your real keys.

## License

MIT
