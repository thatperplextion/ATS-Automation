
# AI Job-Seeker Assistant (n8n Workflow)

This repo contains an n8n workflow that:

* Collects a resume + job description via **Form Submit Trigger**
* Extracts and cleans resume & job‑description text
* Optionally scrapes GitHub / portfolio data
* Calculates simple, rule‑based **ATS / overall quality score**
* Does a rule‑based **skills–gap analysis**
* Builds a simple HTML report + converts it to PDF
* Emails the report to the candidate
* Stores a summary row in a Notion database:

  * `Name`
  * `Date Analyzed`
  * `email`
  * `Overall Quality` (number)
  * `Skills Gap Count` (number)
  * `GitHub URL`
  * `Drive Link` (optional if you add a Google Drive node)

## Files

* `ai-job-workflow.json` – import this into n8n (**Import from file**).
* `.gitignore` – basic Node / editor ignores.

## Notion database setup

Create a **Notion database** with these properties (exact names + types):

| Property name     | Type   |
|-------------------|--------|
| Name              | Title  |
| Date Analyzed     | Date   |
| Drive Link        | URL    |
| email             | Email  |
| Overall Quality   | Number |
| Skills Gap Count  | Number |
| GitHub URL        | URL    |
| LinkedIn URL      | URL    |

Share the database with your Notion integration, then put the **database id**
into the Notion node in n8n (or pick it from the dropdown).

The workflow already maps:

* `Name` ← Full Name from the form
* `email` ← Email Address from the form
* `Date Analyzed` ← current date (Asia/Kolkata)
* `GitHub URL` ← GitHub Profile URL from the form
* `Overall Quality` ← `overall_quality_score` from `Rule-based ATS & Keyword Matcher`
* `Skills Gap Count` ← `skills_gap.length` from `Rule-based Skills Gap Analysis`

## How to use

1. Import `ai-job-workflow.json` into n8n.
2. Configure credentials (OpenAI or your LLM, Gmail, etc – depending on what you use).
3. Edit the **Form Submit Trigger** fields if you want to rename them.
4. Open the **Save Summary to Notion** node and point it at your Notion database.
5. Activate the workflow and submit the public form URL to test.

You can now push this repo to GitHub from VS Code.

