# Prompt 1: Build the Researcher and Analyst Agents

Copy and paste the following into Claude Code:

```
Context: 
I want to build an automated research pipeline that can take any topic, search the web for real-time information, and then analyze the findings for key trends and insights — all without manual work. A single agent can't do this well because researching and analyzing are different skills. I need specialized agents that each do one thing well.

Instruction: in the existing "multi_agent_workflows.ipynb" notebook, I want you to solve this problem by building two specialized agents. The Researcher searches the web and collects facts. The Analyst receives those facts and extracts trends, risks, and insights. Use Pydantic models so data flows cleanly between them. Before choosing a model, search online to verify the latest available OpenAI models. Use the exact model specified — do not substitute without confirming.

Input:
- Agent 1: "Researcher" — uses tavily_search, returns max 5 bullet points. Output type: Pydantic BaseModel with "summary" field.
- Agent 2: "Analyst" — no tools, receives research notes and extracts key trends/risks/insights in 2 paragraphs. Same output type.
- Model: gpt-5-mini (both agents)
- Test query: "Why is Labubu so popular and what are the rarest Labubu collectibles?"

Output: A notebook with environment setup, tavily_search tool, both agents defined, and the Researcher tested with the query. Set the notebook kernel to "venv" so it auto-selects the virtual environment kernel in VS Code.
```
