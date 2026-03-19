---
name: tailor-resume
description: "Tailor a resume to a job description — extracts keywords, rewrites summary, prioritises bullets, and drafts a cover letter"
version: "1.0"
author: NoxNox5
license: MIT

category: job-search
tags:
  - resume
  - cover-letter
  - job-search
  - career

models:
  recommended:
    - claude-sonnet-4-6
    - claude-opus-4-6
  compatible:
    - claude-haiku-4-5

capabilities:
  - resume_tailoring
  - cover_letter_generation
  - keyword_extraction

languages:
  - en
---

# Tailor Resume Skill

## Overview

Paste a job description and this skill will:
1. Extract the top keywords and requirements from the JD
2. Read your base resume from `data/base_resume.json`
3. Rewrite your professional summary (2 sentences) for this specific role
4. Tell you which bullets to lead with in each experience entry
5. Draft a concise, specific cover letter (3 paragraphs, ~250 words)

## How to Use

Run `/tailor-resume` then paste the job description when prompted. Optionally include the company name and hiring manager name for a personalised cover letter.

**Example prompts:**
- `/tailor-resume` *(then paste the full JD)*
- `/tailor-resume [paste JD here]`
- `/tailor-resume` → company: Stripe, hiring manager: Sarah Lee → [JD]

## Instructions for Claude

When this skill is invoked, do the following:

### Step 1 — Get the job description
If the user has already pasted a JD in their message, use it. Otherwise ask:
> "Paste the full job description below. Optionally add the company name and hiring manager name on the first line."

Parse out:
- `company_name` — from user input or infer from JD
- `job_title` — from JD heading or first line
- `hiring_manager` — from user input, or use "Hiring Team" if not provided
- `jd_text` — the full JD body

### Step 2 — Read the base resume
Read the file at: `~/Claude-Workspace/projects/job_tracker/data/base_resume.json`

If that path doesn't exist, look for `data/base_resume.json` relative to the current working directory. If neither exists, ask the user to provide their resume path.

### Step 3 — Analyse the JD
Extract:
- **Top 12 keywords** — specific skills, tools, methodologies mentioned in the JD. Include exact phrases where possible (e.g. "stakeholder management" not just "stakeholder").
- **Role type** — classify as one of: `business_analyst`, `data_analyst`, `operations_analyst`, `product_analyst`, `software_engineer`
- **Must-haves** — 3-5 hard requirements the candidate must demonstrate
- **Nice-to-haves** — 3-5 preferred but not essential

### Step 4 — Tailor the resume
Using the keywords and must-haves:

**Summary (2 sentences):**
- Sentence 1: lead with years of experience and the exact job title from the JD
- Sentence 2: name 2-3 specific tools or achievements that match the JD
- Never use: "leverage", "synergy", "circle back", "deep dive", "passionate about"
- Use contractions. Keep it under 50 words total.

**Experience bullet priorities** (for each role, list which 2-3 bullets to move to the top):
- Infoblox: pick the bullets that match JD keywords most closely
- INLOG / Truweight: only highlight if directly relevant; otherwise deprioritise

**Skills reorder:**
- List which skills to move to the front of each category to match JD

### Step 5 — Draft the cover letter
Exactly 3 paragraphs, 200–270 words. No greeting line — start straight into paragraph 1.

- **Paragraph 1 (2-3 sentences):** Why this specific role at this specific company. Reference something concrete from the JD — a product, a team structure, a stated challenge. Not generic enthusiasm.
- **Paragraph 2 (3-4 sentences):** Two or three achievements with specific numbers (60% dashboard improvement, 20% forecast accuracy, 10% SLA adherence, 83% ML accuracy). Name the companies. Connect directly to the JD's must-haves.
- **Paragraph 3 (2 sentences):** Forward-looking close. Confident, not desperate. No "I would be a great fit" or "I am excited to contribute."

End with:
```
Regards,
Subhankar Tripathi
Subbu.tripathi.dcu@gmail.com | +353-892783756
```

### Step 6 — Output format

Present the output in this exact structure:

---

## ✦ Role: [Job Title] at [Company]

### Keywords matched
`keyword1` `keyword2` `keyword3` *(list all 12 as inline code)*

### Must-haves coverage
| Requirement | Evidence |
|---|---|
| [must-have 1] | [which bullet/role covers it] |

### Tailored summary
> [2-sentence summary here]

### Bullet priorities
**Infoblox:** lead with → [bullet 1 opening words], [bullet 2 opening words]
**INLOG:** lead with → [bullet 1 opening words] *(or: deprioritise — less relevant for this role)*
**Truweight:** [same]

### Skills reorder
- Technical: move [X, Y] to front
- Analytical: move [X, Y] to front

### Cover letter
---
[Full cover letter text]

Regards,
Subhankar Tripathi
Subbu.tripathi.dcu@gmail.com | +353-892783756
---

## Notes for customisation

To adapt this skill for your own resume:
1. Replace the resume path in Step 2 with your own `base_resume.json`
2. Update the contact details in Step 5's sign-off
3. Replace the achievement numbers in Step 5 with your own metrics
4. Adjust the role classification list in Step 3 to match your target roles
