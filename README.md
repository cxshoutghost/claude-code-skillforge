<div align="center">

# Skillforge

### The skill that builds skills.

Generate perfectly structured Claude Code &amp; Antigravity `SKILL.md` files — with live doc sync, 9-marketplace discovery, and self-validation — in minutes.

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-5.4.0-green.svg)](CHANGELOG.md)
[![Claude Code](https://img.shields.io/badge/Claude_Code-compatible-blueviolet.svg)](https://code.claude.com)
[![Antigravity](https://img.shields.io/badge/Antigravity-compatible-orange.svg)](https://antigravity.google)

**Built by [Lijin Nair](https://lijinnair.com)** · [@lijinnair](https://github.com/lijinnair)

</div>

---

## Quick Start

```bash
# Clone into your Antigravity skills directory
git clone https://github.com/lijinnair/skillforge ~/.gemini/antigravity/skills/skillforge

# Or into native Claude Code
git clone https://github.com/lijinnair/skillforge ~/.claude/skills/skillforge
```

Then just say: **"I want to build a new skill"** or run **`/skillforge`**

---

## What It Does

Skillforge is a meta-skill — an AI agent that builds other AI agents. Give it a raw idea or messy workflow, and it outputs a deploy-ready `SKILL.md` file that follows every official best practice.

**The pipeline:**

| Step | What happens |
|---:|---|
| 1 | **Live Docs Sync** — Fetches latest rules from `code.claude.com` and `antigravity.google` |
| 2 | **Intake** — Collects your skill name, category, ecosystem, triggers, inputs, and outputs |
| 3 | **Discovery** — Searches 9 marketplaces in parallel to find existing similar skills |
| 4 | **Front Matter** — Engineers a spec-compliant, sub-1024-char metadata block |
| 5 | **SOP Translation** — Converts your workflow into an imperative execution pipeline |
| 6 | **Self-Validation** — Audits its own output against 8 rules before delivery |

## Why It Exists

Most AI skills are written like essays. Skillforge enforces **Progressive Disclosure** — the principle that every token in the context window must earn its place:

- Minimal footprint in the context window
- Deterministic logic offloaded to `scripts/`
- Examples and references loaded only when needed
- Strict imperative pipelines, not conversational prose

The result: skills that are faster, more reliable, and cheaper to run.

## Features

- **Dual ecosystem** — Generates skills for Claude Code or Antigravity
- **Live doc sync** — Always builds against the latest official spec
- **9-source discovery** — Searches Smithery, SkillsMP, SkillsLLM, SkillHub, Composio, AI Templates, GitHub Topics, and more before building from scratch
- **Graceful fallback** — If docs are unreachable, surfaces cached version and asks before proceeding
- **Self-validating** — 8-point checklist catches errors before you see the output
- **Token-optimized** — The skill itself practices what it preaches (< 100 lines, ~1,100 tokens)

## Repository Structure

```
skillforge/
├── SKILL.md            ← The core SOP (v5.4.0)
├── README.md           ← You are here
├── CHANGELOG.md        ← Full version history
├── CONTRIBUTING.md     ← How to contribute
├── LICENSE             ← MIT
├── skill.json          ← Marketplace metadata
└── examples/
    ├── seo-page-auditor.SKILL.md
    └── git-commit-formatter.SKILL.md
```

## Examples

Skillforge generates skills like these:

- **[SEO Page Auditor](examples/seo-page-auditor.SKILL.md)** — Audits any URL for title tags, meta descriptions, heading structure, and content quality
- **[Git Commit Formatter](examples/git-commit-formatter.SKILL.md)** — Generates Conventional Commits messages from staged diffs

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). All contributions welcome.

## Author

**[Lijin Nair](https://lijinnair.com)** — AI Systems Builder &amp; Prompt Architect

- GitHub: [@lijinnair](https://github.com/lijinnair)
- Web: [lijinnair.com](https://lijinnair.com)

---

<div align="center">

If Skillforge saved you time, **[star the repo](https://github.com/lijinnair/skillforge)** — it helps others find it.

</div>
