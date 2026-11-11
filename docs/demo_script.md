# Demo script (6 minutes)

**Before you start:** workflow active, landing page open, form open in a second tab, Sofia's CV and achievement bank ready, inbox open. A backup report in the inbox in case the live run is slow.

| Time | Part | What to show | What to say |
|---|---|---|---|
| 0:00–0:45 | Problem and user | Landing page hero | Career coaches spend 1–2 hours preparing each application. AI tools are faster, but they invent experience. This agent does the research and drafts, and only uses facts it can prove. |
| 0:45–1:30 | Trigger | The form | Paste a job link, upload Sofia's CV, paste her extra achievements, pick English. Submit. From here, no human input. |
| 1:30–3:00 | Autonomy | n8n canvas while it runs | Walk left to right: reads CV and job, falls back to pasted text if the page is blocked, researches the company three ways, pulls guidelines from Pinecone, scores the fit. Point at the two decisions: the score gate (below 50 gets a short honest note) and the fact-check loop (unsupported claims trigger one rewrite). |
| 3:00–4:30 | The report | The email | At a glance block, fit analysis with strong/partial/gap, then the CV fix: "Helped automate several workflows" becomes "Automated 8 of 14 workflows, freeing ~60 hours a month". The number comes from her achievements, not the model. Cover letter opening, interview STAR stories, sources. |
| 4:30–5:15 | Stack decision | Canvas, one slide | Why n8n: trigger-driven, fits the tools coaches use, visible branching a non-technical team can maintain, fast to demo. When LangGraph would win: if the agent had to choose its own research path. |
| 5:15–6:00 | GTM sprints | `gtm_future_sprints.md` | Sprint 1: free pilot with a bootcamp, measure time saved. Sprint 2: case study to three paying customers, GDPR pack. Sprint 3: white-label partner with an outplacement firm. |

**If the live run fails:** show the backup report from the inbox and walk through the canvas from the last successful execution (Executions tab).

**Questions to prepare for:**
- How do you stop it inventing facts? Candidate facts only from CV and pasted achievements, nothing stored in RAG, fact-check loop, unverified claims flagged.
- Why not store candidate profiles? Privacy and GDPR for the MVP; saved profiles are part of Sprint 3.
- What does a run cost? A handful of `gpt-4o-mini` calls per report, a fraction of a cent to a few cents depending on input length (check your OpenAI usage page for the real number before the demo).
