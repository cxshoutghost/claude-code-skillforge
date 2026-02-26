# Changelog

All notable changes to `skillforge` are documented here.
Follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format.

---

## [5.10.0] — 2026-02-26
### Added
- **Sample Upgrade Report** — New example (`examples/sample-upgrade-report.md`) showing the diagnostic audit output format with Pass/Warning/Fail items and change summary.
- **Sample Scan Report** — New example (`examples/sample-scan-report.md`) showing the health report table format across installed skills.
- **Upgrade Mode evaluation** — New test scenario (`evaluations/eval-upgrade-mode.json`) for testing the upgrade pipeline with a poorly structured skill.
- **Scan Mode evaluation** — New test scenario (`evaluations/eval-scan-mode.json`) for testing the scan pipeline.
- **CONTRIBUTING.md modes section** — Documents the three modes (Build, Upgrade, Scan) and how they interact.

### Changed
- **README pipeline section** — Now shows all three mode pipelines (Build, Upgrade, Scan) instead of just Build.
- **README examples section** — Split into Build Mode outputs and Upgrade & Scan Mode outputs.

---

## [5.9.0] — 2026-02-26
### Added
- **Skill Scanner (Scan Mode)** — Say "Scan my skills" and Skillforge reads all SKILL.md files in `~/.claude/skills/` and `~/.gemini/antigravity/skills/`, runs a quick audit on each, and outputs a health report table sorted by most issues first.
- **Scan Path (Steps S1–S3)** — Three-step scan pipeline: Discover Skills → Quick Audit → Health Report with actionable next steps.
- **Post-delivery nudge** — After every Build or Upgrade delivery, Skillforge now suggests scanning or upgrading other installed skills.

---

## [5.8.0] — 2026-02-26
### Added
- **Skill Upgrader (Upgrade Mode)** — Skillforge now supports a second mode: feed it any existing SKILL.md and it runs a full 27-item diagnostic audit, reports Pass/Warning/Fail per item, then auto-upgrades the skill to latest best practices while preserving original intent and domain logic.
- **Step 1.5: Mode Detection** — After syncing best practices, Skillforge now detects whether the user wants to build a new skill or upgrade an existing one, and branches accordingly.
- **Upgrade Path (Steps U1–U4)** — Four-step upgrade pipeline: Ingest → Diagnostic Audit (with checkpoint) → Upgrade & Fix → Deliver with change summary.

### Changed
- **Front matter description** — Updated to include upgrade-related triggers ("upgrade an existing skill", "audit a skill for compliance").

---

## [5.7.0] — 2026-02-26
### Added
- **New discovery source in Step 2.5** — Added [Awesome Claude Skills](https://github.com/ComposioHQ/awesome-claude-skills) (37K GitHub stars), expanding from 9 to 10 marketplace sources searched in parallel.
- **8 authoring patterns in Step 4** — Template pattern (strict vs flexible output formats), Examples pattern (input/output pairs), Conditional workflow pattern (decision-point branching), Checklist pattern (copyable progress tracking), Verifiable intermediates (plan-validate-execute), Defaults over options, MCP tool references (`ServerName:tool_name`), and Progressive Disclosure — all drawn from the official best practices.
- **Name field validation rules in Step 2** — Now teaches all 4 official constraints: max 64 characters, lowercase letters/numbers/hyphens only, no XML tags, cannot contain reserved words ("anthropic", "claude").
- **XML tag prohibition** — Added to Step 2 (name), Step 3 (description), and Step 6 (checklist).
- **MCP server support** — Step 2 (Tools) now includes MCP servers as an option. Step 4 teaches fully qualified `ServerName:tool_name` format.
- **Script quality guidance in Step 5** — "Solve, don't punt" (explicit error handling), no voodoo constants (document all configuration values), and dependency declaration (list packages with install commands).
- **Reference file guidance in Step 5** — Table of contents for files >100 lines, forward-slash-only paths.
- **3-section validation checklist in Step 6** — Restructured from a flat 11-item list to 3 sections: Core quality (16 items), Code & scripts (8 items), Post-delivery recommendations (3 items) — 27 items total, aligned with the official checklist structure.
- **Post-delivery testing recommendations** — Step 6 now recommends testing with Haiku/Sonnet/Opus, creating 3+ evaluation scenarios, and testing with real usage before sharing.
- **`evaluations/` directory** — 3 evaluation scenario files for testing Skillforge-generated skills: simple skill (no scripts), skill with scripts and dependencies, advanced skill (MCP tools + conditional workflow + checklist pattern).

### Changed
- **Step 4 (SOP Translation)** — Reorganized into base rules + "Authoring patterns" subsection for cleaner progressive disclosure.
- **Step 5 (Scaffold)** — Split into Scripts and References subsections for clarity.
- **Example: formatting-commits** — Added input/output example pairs demonstrating the Examples pattern from the official best practices.

---

## [5.6.0] — 2026-02-26
### Changed
- **Front matter compliance** — Removed non-standard fields (`license`, `metadata` block) from Skillforge's own front matter. Added `argument-hint` field. Only officially recognized fields are now used.
- **Step 2 (Intake)** — Gerund naming convention (e.g., `analyzing-seo-pages`) is now the recommended default per official best practices. Noun form accepted as fallback.
- **Step 3 (Front Matter)** — Explicitly lists all recognized fields and warns against custom fields. Removed `category` metadata guidance. Added `argument-hint` guidance.
- **Step 4 (SOP Translation)** — Added "degrees of freedom" guidance for matching instruction specificity to task fragility. Added feedback loop / validation pattern guidance. Added warning against time-sensitive information.
- **Step 5 (Scaffold)** — Added guidance to keep references one level deep from SKILL.md.
- **Step 6 (Validate)** — Expanded checklist from 8 to 11 items: added checks for non-standard front matter, time-sensitive info, consistent terminology, and reference depth.
- **Example skills** — Renamed to gerund form (`auditing-seo/`, `formatting-commits/`), moved into subdirectories, removed non-standard front matter (`license`, `metadata`), removed redundant `## Goal` sections, added validation step to SEO example.

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
- **Live Best Practices Sync** — Step 1 now fetches `https://code.claude.com/docs/en/skills` and `/hooks` at runtime to prevent hallucinating deprecated syntax.
### Changed
- Restructured the entire SOP into a strict 5-step imperative pipeline.

---

## [1.0.0] — 2026-02-24
### Initial Release
- Base meta-skill structure for generating `SKILL.md` files.
- 5-step pipeline: Intake → Front Matter Engineering → SOP Translation → Separation of Concerns → Scaffold Generation.
- Support for `context: fork`, `allowed-tools`, and `disable-model-invocation` advanced configurations.
