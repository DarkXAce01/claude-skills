# claude-skills

Personal [Claude Code](https://code.claude.com) plugins.

## portfolio-dossier

Run `/portfolio-dossier:portfolio-dossier` inside any project. Claude researches the codebase and git history, captures real screenshots, terminal runs and an architecture diagram, asks a few questions, and writes everything to `~/portfolio-dossiers/<slug>/`, ready to turn into a portfolio page. Facts only, with a privacy pass that strips personal data before it finishes.

## Install

```bash
claude plugin marketplace add DarkXAce01/claude-skills
claude plugin install portfolio-dossier@claude-skills
```

Update later with `claude plugin marketplace update claude-skills`.
