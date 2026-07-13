# Prompt 2: Add the Writer Agent & Build the Full Pipeline

Copy and paste the following into Claude Code:

```
Context: We have "multi_agent_workflows.ipynb" with a Researcher and Analyst agent. The Researcher can find information and the Analyst can extract insights — but there's no one to write a polished report from the findings.

Problem: Right now, a human would need to take the Analyst's output and manually write it up into a professional report. I want the pipeline to go end-to-end: from a user's question all the way to a finished executive report with a summary, detailed analysis, and follow-up questions — fully automated, no manual steps.

Instruction: Add a Writer agent that produces a polished research report, and an async manager_run(user_query) function that chains all three agents: Researcher → Analyst → Writer. Use SQLiteSession so all agents share memory. Display the final report output. Before choosing a model, search online to verify the latest available OpenAI models. Use the exact model specified — do not substitute without confirming.

Input:
- Writer agent: "Writer", gpt-5-mini, outputs a Pydantic model with short_summary (2-3 sentences), markdown_report (500+ words), follow_up_questions (list of 3-5)
- Pipeline: Researcher gets query → Analyst gets research summary → Writer gets query + research + analysis
- Test query: "What is the public sentiment and expert reviews about the Tesla Cybertruck?"

Output: Updated notebook with the Writer agent, a manager_run() pipeline function, and test results showing summary, full report, and follow-up questions.
```
