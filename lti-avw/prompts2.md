# Prompt log — LTI documentation & GitHub Project (session 2)

## Initial prompt (verbatim)

with the context of the project in the files within the lti-avw folder (@lti-avw ) your task is to prepare the necessary documentation to start implementing LTI:
-Generate user stories using the following template: 
Act as a senior Product Owner with experience in agile methodologies.
Based on the following product description, generate 5 User Stories that meet the INVEST criteria. For each one include:

Descriptive title
Story in the format "As a [role], I want [action], so that [benefit]"
3 acceptance criteria in BDD format (Given/When/Then)
Complexity estimate (S/M/L)
Brief evaluation against INVEST

Product description:
"We are building an e-learning platform where instructors can create courses with video modules, quizzes, and certifications. Students can enroll, track their progress, and earn certificates upon completing a course."
After generating the stories, suggest a prioritization order for the MVP and justify your decision.

-Build the product backlog: assemble the backlog with the user stories, prioritizing them. 
-Choose the first user story and generate work tickets, detail them technically
-Estimate the effort of the work tickets using the methodology (Fibonacci, Planning Poker, T-shirt sizes) and units (hours, story points) of your choice.
-Document everything in a single .md file within the new repository that was just cloned (AI4DEVS-DESIGN2-2026-03-SENIOR). The file name is UserStories-AVW.md and place it in the folder lti-avw copied over from this current repo (AI4DEVS-DESIGN1-2026-03-SENIOR)
-additionally, create a github project to track user stories and tickets in the newly cloned repo
)

---

## Summary of the conversation

Work was aligned with **LTI (Lean Talent Intelligence)** and the design in `lti-avw` (including `LTI-AVW.md`), not the generic e-learning product description embedded in the template. Deliverable **`lti-avw/UserStories-AVW.md`** covers: five INVEST user stories, MVP prioritization, backlog table, first story (US-01) broken into tickets T-01–T-07 with technical detail, and effort estimates (Fibonacci story points, T-shirt, hours).

For **GitHub Project tracking**, you chose **Option B (GitHub CLI)**. Practical notes from that thread:

- **`gh` on Windows:** In some shells (e.g. Cursor), `gh` may not be on `PATH`; the CLI is often installed at `C:\Program Files\GitHub CLI\gh.exe`.
- **Projects API scopes:** `gh project` requires OAuth scopes **`project`** and **`read:project`**. Use `gh auth refresh -s project,read:project` if `project create` / `item-add` fails with missing scopes.
- **`gh project item-add` and “resource not found”:** The repository initially had **Issues disabled**, so no valid `/issues/<n>` URLs existed. After **enabling Issues** in repo settings, issue URLs resolve correctly. Placeholders like `<num>` must be replaced with real issue numbers.
- **Adding issues to a Project V2 in one step:** `gh issue create -R <owner/repo> -t "…" -b "…" -p "LTI AVW — MVP delivery"` attaches the new issue to the project by title (avoids manual `item-add` for each new issue).
- **Backlog created on GitHub:** User project **“LTI AVW — MVP delivery”** ([`andresviverosw` user project #1](https://github.com/users/andresviverosw/projects/1)) with **12 issues** #1–#12: US-01–US-05 and US-01 tickets T-01–T-07, bodies pointing back to `UserStories-AVW.md`.

**Documentation update:** Section **6** of `UserStories-AVW.md` was rewritten to record these outcomes (project link, scopes, issue index, CLI patterns, optional follow-ups) instead of the earlier note that automation was unavailable in the environment.

**This file:** Captures the **initial prompt** (verbatim above) and this **summary** for traceability.
