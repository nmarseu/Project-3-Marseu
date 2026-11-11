# Stack decision: n8n vs LangGraph

## The two decisions

**1. Industry / use case:** HR tech / career services. The Application Prep Agent turns a job posting link and a candidate's CV into a company and role brief, an honest fit analysis, CV improvement suggestions, a tailored cover letter and interview prep, for career services teams at bootcamps, universities and outplacement firms.

**2. Primary stack:** ☑ n8n ☐ LangGraph

## Why n8n fits this industry and problem

The workflow is trigger-driven and mostly linear: a form submission starts the run, and it moves through fetching the posting, researching the company, matching the CV and writing the report. Its value depends on plugging into tools career services teams already use, like forms and email, and n8n handles those natively. The branching is explicit and visible (fallback when a job page can't be read, the fit-score gate, the fact-check retry), so a non-technical career services team can understand and maintain it. The reasoning steps are well-defined (research, match, critique, write, check) rather than open-ended exploration, so LangGraph's fine-grained control over agent loops isn't needed for this MVP. n8n also got the MVP to a reliable end-to-end demo within the 5-day timeline.

## Trade-offs considered

| Criterion | n8n | LangGraph | Weight for this MVP |
|---|---|---|---|
| Time to demo | Visual nodes, built-in form, email and AI nodes | Python code for every step | High: 5-day timeline |
| Ops integration | Native form, email, Google, Slack, Airtable nodes | Needs custom integrations | High: buyers live in these tools |
| Maintainability by the buyer | Career services staff can read the canvas | Requires a Python developer | High: the buyer is non-technical |
| Branching logic | IF nodes, visible error outputs, loops | Fine-grained state and conditional edges | Medium: branching here is simple |
| Control over agent reasoning | Limited to prompts and fixed paths | Full control of a ReAct-style loop | Low: the steps are known in advance |
| Testing and versioning | JSON export, harder to unit-test | Standard Python testing | Medium |

## Where n8n reached its limits

- **Loops are awkward.** The fact-check retry needed a counter and a manual loop-back. In LangGraph this would be a conditional edge with state.
- **Prompt changes happen in the UI.** Long prompts lose formatting when pasted, and versioning relies on exporting the JSON.
- **No native unit tests.** Quality is checked by running sample cases.

## When LangGraph would become the better choice

- If the agent had to **decide which research to do** (for example, choosing between funding data, Glassdoor-style reviews or product pages depending on the company), a ReAct-style tool loop would fit better.
- If the product grew into a **multi-tenant SaaS** with automated tests, CI/CD and fine-grained cost control.

For the MVP, LangGraph is out of scope. A later version could keep n8n for triggers and delivery, and call a LangGraph service for the research and writing steps.
