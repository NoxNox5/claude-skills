# claude-skills

A collection of Claude Code slash command skills for job searching, resume tailoring, and career workflows.

## Skills

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

## Adding more skills

Each skill lives in its own folder with a `SKILL.md` file. Copy the folder to `~/.claude/skills/` to install.

## License

MIT
