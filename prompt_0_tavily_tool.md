# Prompt 1: Define a Tavily Web Search Tool

Copy and paste the following into Claude Code:

```
Context: This module needs the Tavily API for web search. 

Instruction: First, add TAVILY_API_KEY to the existing .env file without overwriting existing keys. If you found an existing API Key, skip this step. Then create a new notebook called "multi_agent_workflows.ipynb" with a custom Tavily web search tool. Don't create any agents yet — just the tool function. Before choosing a model, search online to verify packages, docs and models. Use the exact model specified — do not substitute without confirming.

Input:
- API keys: OpenAI and Tavily from the existing .env file
- Tool parameters: search query and max_results (use TypedDict)
- API endpoint: "https://api.tavily.com/search"
- Default: 2 results

Output: A notebook with environment setup and a working tavily_search function tool ready to be used by agents. Set the notebook kernel to "venv" so it auto-selects the virtual environment kernel in VS Code.
```
