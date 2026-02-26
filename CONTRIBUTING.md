# Contributing to Skillforge

Thank you for your interest in contributing! This project is a meta-skill for generating optimized Claude Code and Antigravity skills. All contributions are welcome.

---

## 📋 How to Contribute

### 1. Reporting Issues
If you find a bug or something that doesn't work as expected:
- Open a **GitHub Issue** with a clear title and description.
- Include your Claude Code version and which ecosystem you are using (native Claude or Antigravity).
- If the docs URLs in Step 1 are returning unexpected content, please include the URL and what you received.

### 2. Suggesting Improvements
- Open a **GitHub Issue** tagged with `enhancement`.
- Describe the use case that is currently not handled.
- If relevant, include a sample skill that would benefit from the improvement.

### 3. Submitting Pull Requests
1. **Fork** this repository.
2. Create a new branch: `git checkout -b feature/your-improvement-name`
3. Make your changes following the guidelines below.
4. Open a **Pull Request** with a clear description of what changed and why.

---

## ✅ Contribution Guidelines

### Editing `SKILL.md`
- Keep the file **under 500 lines**.
- Keep the **Front Matter under 1024 characters**.
- All SOP steps must begin with an **imperative command verb**.
- Do NOT remove the **(CHECKPOINT)** gates or the **Self-Validation Checklist** — these are core safety features.
- Bump the version in the `VERSION` file, the `version` field in `skill.json`, and the inline version in `SKILL.md` Step 0. Add a corresponding entry to `CHANGELOG.md`.

### Working with Modes
Skillforge has three modes: **Build**, **Upgrade**, and **Scan**. When making changes:
- **Build Mode** (Steps 2–6): The primary skill generation pipeline.
- **Upgrade Mode** (Steps U1–U4): The diagnostic audit and auto-upgrade pipeline.
- **Scan Mode** (Steps S1–S3): The installed skills health check pipeline.
- Changes to the validation checklist in Step 6 also affect Upgrade Mode (Step U2 reuses it).

### Adding Examples
- New examples go in the `examples/` directory.
- Use a subdirectory per example: `examples/[skill-name]/SKILL.md`.
- The example must be a real, working skill (not a placeholder).
- Use only officially recognized front matter fields (no custom fields like `generated-by`).

### Updating Documentation
- Keep `README.md` concise — the 5-section format (What/Why/When/Where/How) should be preserved.
- Update `CHANGELOG.md` for every meaningful change using [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format.

---

## 🧠 Philosophy
This project follows the **Progressive Disclosure** principle — less is more. When in doubt, link to external docs rather than embedding them. Every line added to `SKILL.md` has a cost in tokens, so make it count.

---

## 📝 License
By contributing, you agree that your contributions will be licensed under the MIT License.
