# claude-skills

A collection of Claude Code slash command skills.

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

## Installing a skill

```bash
git clone https://github.com/NoxNox5/claude-skills.git
cp -r claude-skills/prompter ~/.claude/skills/prompter
```

Then use in Claude Code:
```
/prompter
```

## Adding more skills

Each skill lives in its own folder with a `SKILL.md` file. Copy the folder to `~/.claude/skills/` to install.

```
~/.claude/skills/
└── skill-name/
    └── SKILL.md
```

## License

MIT
