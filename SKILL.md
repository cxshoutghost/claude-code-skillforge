---
name: skillforge
description: Generates highly optimized Agent Skills for both native Claude Code and the Antigravity system, according to official best practices and the "Progressive Disclosure" strategy. Use when the user wants to build a new skill, turn a workflow into a skill, optimize an existing prompt, or structure agent instructions for either ecosystem.
license: MIT
metadata:
  author: Lijin Nair
  github: https://github.com/lijinnair
  website: https://lijinnair.com
  version: "5.5.0"
---

# Skillforge SOP

## Execution Rules
- Fetch all URLs and search all marketplaces **in parallel** using concurrent tool calls.
- `read_url_content`, `search_web`, `view_content_chunk` are non-destructive — execute without user approval.
- Only pause at steps marked **(CHECKPOINT)**.

## Step 0: Update Check
Fetch `https://raw.githubusercontent.com/lijinnair/skillforge/main/VERSION` silently. Compare the remote version with the local version (`5.5.0`). If remote is newer, display: *"Skillforge v[remote] is available (you have v[local]). Run `git -C [skill-path] pull` to update."* where `[skill-path]` is the detected install location. Then proceed normally — do not block execution.

## Step 1: Sync Live Docs (CHECKPOINT)
Fetch live documentation before any user interaction.

1. **Fetch ALL 5 URLs in parallel:**
   - `https://code.claude.com/docs/en/`
   - `https://code.claude.com/docs/en/skills`
   - `https://code.claude.com/docs/en/hooks`
   - `https://antigravity.google/docs/home`
   - `https://antigravity.google/docs/skills`
2. **All succeed:** Synthesize best practices, present summary. Say: *"Here are the latest best practices. Proceed?"* Wait for confirmation.
3. **Any fail:** State which URLs failed. Display cached knowledge version and date. Say: *"I can proceed using built-in knowledge (Version: [X], Last Updated: [Date]). Continue or retry?"* Do not proceed until the user chooses.

## Step 2: Intake & Scoping
Collect from the user:
- **Name:** kebab-case (e.g., `my-skill-name`)
- **Category:** `dev` | `marketing` | `seo` | `document` | `data` | `ops`
- **Ecosystem:** Claude Code (`~/.claude/skills`) or Antigravity (`~/.gemini/antigravity/skills`)
- **Triggers:** Activation words or phrases
- **Inputs:** Context, files, or arguments needed at runtime
- **Output:** Expected deliverable
- **Tools:** Bash, URL fetch, file read, or `context: fork`?

## Step 2.5: Discovery Check
Search **ALL 9 sources in parallel** before building from scratch:

1. Smithery — `https://smithery.ai/skills?q=[skill-name]`
2. SkillsMP — `https://skillsmp.com/search?q=[skill-name]`
3. SkillsLLM — `https://skillsllm.com/search?q=[skill-name]`
4. SkillHub — `https://skill-marketplace.com/search?q=[skill-name]`
5. Antigravity Skill Vault — `https://github.com/search?q=[skill-name]+topic:antigravity-skill`
6. Awesome Skills — `https://github.com/sickn33/antigravity-awesome-skills` CATALOG.md
7. GitHub Topics — `https://github.com/search?q=[skill-name]+topic:claude-code-skill`
8. Composio — `https://composio.dev/search?q=[skill-name]`
9. AI Templates — `https://www.aitmpl.com/skills?q=[skill-name]`

**Results:**
- **No match:** Proceed to Step 3.
- **Match found (CHECKPOINT):** Present Discovery Report (name, source, stars, description). Ask: *(A) Customise existing, or (B) Build new?* Wait for choice.
- **Sources failed:** Note unreachable sources in the report. Use whatever succeeded. If ALL 9 fail, proceed to Step 3.

## Step 3: Front Matter Engineering
Design front matter (`< 1024 chars`) per the docs synced in Step 1:
- **Description:** Start with 3rd-person verb ("Analyzes...", "Generates..."). Include 3–5 trigger phrases.
- **Category:** Add `category: [value]` metadata field.
- **Invocation:** `disable-model-invocation: true` for destructive actions. `user-invocable: true` for explicit-only. Omit both for auto-discover.
- **Advanced:** Add `context: fork` and `allowed-tools` only if required.

## Step 4: SOP Translation
Convert the workflow into numbered imperative steps.
- Each step starts with a command verb ("Extract...", "Analyze...", "Compile...").
- Use `$ARGUMENTS` and backtick substitution (e.g., `!\`gh pr diff\``) for runtime context.
- **Progressive Disclosure:** Do not embed data only needed for one path — link to it or load it conditionally.

## Step 5: Scaffold Generation
Output the `mkdir` command for the chosen ecosystem:
- Claude: `mkdir -p ~/.claude/skills/[skill-name]`
- Antigravity: `mkdir -p ~/.gemini/antigravity/skills/[skill-name]`

Offload deterministic logic to `scripts/` if applicable. Follow with the complete `SKILL.md` code block.

## Step 6: Validate & Deliver
Run this checklist internally — fix any failures before delivering output.

- [ ] Front matter < 1024 characters
- [ ] Body < 500 lines
- [ ] Description starts with 3rd-person verb
- [ ] Description has 3+ trigger phrases
- [ ] `category` metadata present
- [ ] Invocation flags set correctly
- [ ] All steps begin with imperative verb
- [ ] Correct `mkdir` path for chosen ecosystem

**Deliver:** Sync status → checklist results → `mkdir` command → full `SKILL.md` code block.

Consult `examples/` for reference outputs.
