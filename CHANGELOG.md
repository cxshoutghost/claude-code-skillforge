# Changelog

All notable changes to `skillforge` are documented here.
Follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format.

---

## [5.5.0] — 2026-02-25
### Added
- **Step 0: Self-Update Check** — Skillforge now checks for newer versions on GitHub before every run. If an update is available, it displays a one-line notice with the `git pull` command. Non-blocking — does not interrupt the workflow.
- **VERSION file** — New root-level file containing the current version string, used by the update check mechanism.
### Changed
- This pattern will be baked into every skill Skillforge generates, making all Skillforge-built skills self-update-aware.

---

## [5.4.0] — 2026-02-25
### Changed
- **Token optimization pass** — SKILL.md reduced from ~1,300 to ~1,100 tokens per invocation (~15% reduction).
- Removed redundant Goal section (duplicated front matter description).
- Replaced marketplace table with numbered list (saved ~80 tokens of formatting overhead).
- Merged "Expected Output Format" into Step 6, eliminating a standalone section.
- Removed "Reference Best Practices" section (rules already in self-validation checklist).
- Compressed phrasing across all steps while preserving every instruction.
### Added
- `website` metadata field in SKILL.md front matter.
- Enhanced README.md with badges, quick-start section, and viral-optimized layout.
- Expanded skill.json keywords for marketplace discoverability.

---

## [5.3.0] — 2026-02-25
### Added
- **Execution Rules section** — New top-level rules enforcing parallel fetching, auto-read (no approval needed for non-destructive operations), and explicit checkpoint-only pauses.
### Changed
- **Step 1** now explicitly instructs concurrent fetching of all 5 URLs in parallel.
- **Step 2.5** now explicitly instructs concurrent searching of all 9 marketplaces in parallel.

---

## [5.2.0] — 2026-02-24
### Added
- **2 new marketplaces added to Step 2.5 discovery sources:**
  - [Composio](https://composio.dev) — AI agent tool & integration marketplace
  - [AI Templates](https://www.aitmpl.com/skills) — Curated AI skill and prompt templates

---

## [5.1.0] — 2026-02-24
### Added
- **Step 2.5: Skill Discovery Check** — Before building any skill from scratch, Skillforge now silently searches 7 known marketplaces and directories for existing similar skills:
  1. [Smithery](https://smithery.ai) — 100K+ skills registry for Claude Code
  2. [SkillsMP](https://skillsmp.com) — 87K+ community-indexed agent skills
  3. [SkillsLLM](https://skillsllm.com) — AI skills for Claude Code, Codex CLI, and ChatGPT
  4. [SkillHub](https://skill-marketplace.com) — Unified marketplace aggregating top GitHub skills
  5. [Antigravity Skill Vault](https://github.com/search?q=topic:antigravity-skill) — GitHub topic search
  6. [Awesome Skills (sickn33)](https://github.com/sickn33/antigravity-awesome-skills) — 900+ curated skills catalog
  7. [GitHub topic search](https://github.com/search?q=topic:claude-code-skill) — Community skills by topic
- If a match is found, a **Discovery Report** is presented to the user, who can choose to customise an existing skill or build a new one from scratch.

---

## [5.0.0] — 2026-02-24
### Added
- **Step 6: Self-Validation Checklist** — Claude now internally audits its own generated skill against 8 rules (front matter size, line count, trigger phrases, etc.) before delivering output, and fixes any failures automatically.
- **Fallback Checkpoint** — If any documentation URL is unreachable, the skill now gracefully displays the cached knowledge version and last-updated date, then prompts the user to choose to continue or retry instead of silently failing.
- **Skill Category Tagging** — Step 2 now collects a skill category (`dev`, `seo`, `marketing`, `document`, `data`, `ops`) and injects it as a `category` metadata field in the Front Matter.
- **`user-invocable` guidance** — Step 3 now explicitly teaches when to set `user-invocable: true`, `disable-model-invocation: true`, or omit both.
- **`examples/` directory** — Added two fully worked sample output skills:
  - `seo-page-auditor.SKILL.md` — Category: `seo`
  - `git-commit-formatter.SKILL.md` — Category: `dev`

---

## [4.0.0] — 2026-02-24
### Added
- **Antigravity home docs** — Added `https://antigravity.google/docs/home` to the mandatory documentation sync list.
- **Root Claude Code docs** — Added `https://code.claude.com/docs/en/` (root) to Step 1 alongside `/skills` and `/hooks`.
### Changed
- Step 1 is now an explicit **Interactive Checkpoint** that fully blocks progression until the user confirms the synced best practices.

---

## [3.0.0] — 2026-02-24
### Added
- **Dual Ecosystem Support** — The builder now explicitly asks whether the skill is for native Claude Code (`~/.claude/skills`) or the Antigravity system (`~/.gemini/antigravity/skills`) and outputs the correct `mkdir` path accordingly.
- **Antigravity docs sync** — Added `https://antigravity.google/docs/skills` to the mandatory documentation sync step.
- Added `README.md` with full What/Why/When/Where/How documentation.

---

## [2.0.0] — 2026-02-24
### Added
- **Live Documentation Sync** — Step 1 now fetches `https://code.claude.com/docs/en/skills` and `/hooks` at runtime to prevent hallucinating deprecated syntax.
### Changed
- Restructured the entire SOP into a strict 5-step imperative pipeline.

---

## [1.0.0] — 2026-02-24
### Initial Release
- Base meta-skill structure for generating `SKILL.md` files.
- 5-step pipeline: Intake → Front Matter Engineering → SOP Translation → Separation of Concerns → Scaffold Generation.
- Support for `context: fork`, `allowed-tools`, and `disable-model-invocation` advanced configurations.
