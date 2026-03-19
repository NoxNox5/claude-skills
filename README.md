# claude-skills

A collection of Claude Code slash command skills for job searching, resume tailoring, and prompt engineering.

## Skills

---

### `/prompter`
Transform any rough natural-language idea into a production-grade system prompt — structured, model-aware, and optimised for how Claude actually works best.

**Install:**
```bash
cp -r prompter ~/.claude/skills/prompter
```

**Use in Claude Code:**
```
/prompter [describe what you want a prompt to do]
```

**What it does:**

Works in three phases:
1. **Classify** (Haiku-tier thinking) — identifies task type, complexity level, agent identity, and any gaps in your rough prompt
2. **Architect** (Opus-tier thinking) — designs the full system prompt using Claude 4.x best practices: XML tags, context-before-task ordering, positive constraints, exact output format, few-shot examples for complex tasks, Think-Act-Think-Act loops for agentic workflows
3. **Refine** (Sonnet-tier thinking) — runs a checklist pass to remove hedge words, ambiguity, and filler

**What you get back:**
- Complexity assessment (`Simple / Medium / Complex / Agentic`)
- Model recommendation table (Opus / Sonnet / Haiku + when to use adaptive thinking)
- Complete system prompt with XML-tagged sections
- User prompt template with `{{PLACEHOLDER}}` variables
- Usage notes: strengths, failure modes, variations

**Design principles baked in:**
- XML structure (`<role>`, `<context>`, `<task>`, `<constraints>`, `<output_format>`, `<examples>`)
- Context always placed before task (up to 30% performance improvement on data-rich inputs)
- Positive-framed constraints only
- Few-shot examples for Complex and Agentic prompts
- Verification checkpoints for agentic workflows
- Model routing: Opus for reasoning, Sonnet for execution, Haiku for speed/volume

---

### `/tailor-resume`
Paste a job description → get back JD keyword analysis, a tailored 2-sentence summary, bullet priorities per experience entry, and a 3-paragraph cover letter.

**Install:**
```bash
cp -r tailor-resume ~/.claude/skills/tailor-resume
```

**Use in Claude Code:**
```
/tailor-resume [paste job description]
```

**What you get:**
- Top 12 keywords extracted from the JD
- Must-haves coverage table (JD requirement → which of your bullets covers it)
- Tailored professional summary (2 sentences, role-specific)
- Bullet reorder priorities for each experience entry
- Full cover letter (3 paragraphs, ~250 words, specific numbers and company names)

**Customise for your own resume:**
Edit `tailor-resume/SKILL.md` — update the resume path, contact details, and achievement metrics in the instructions.

---

## Installing all skills

```bash
# Clone the repo
git clone https://github.com/NoxNox5/claude-skills.git

# Install all skills at once
cp -r claude-skills/prompter ~/.claude/skills/prompter
cp -r claude-skills/tailor-resume ~/.claude/skills/tailor-resume
```

Then use them in Claude Code:
```
/prompter
/tailor-resume
```

---

## Adding more skills

Each skill lives in its own folder with a `SKILL.md` file. Copy the folder to `~/.claude/skills/` to install.

Skill file structure:
```
~/.claude/skills/
└── skill-name/
    └── SKILL.md    ← YAML frontmatter + markdown instructions
```

## License

MIT
