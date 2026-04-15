# my-codex-skills (test1)

This is a global skill system for Codex focused on **web development, UI quality, and safe code changes**.

It combines:
- external skills (pulled from GitHub)
- local global rules (defined below)

---

# 🧠 GLOBAL RULES (ALWAYS APPLY)

## 📌 Mandatory Rule For Codex

- Before starting any task, Codex must read this README and follow all rules in it.
- These rules are mandatory for all project work and must be respected at all times.
- Codex always ориентируется на правила этого README, читает их и соблюдает их всегда.

## 🛡 Safety Rules

- Do not make broad or sweeping changes unless clearly necessary.
- Prefer minimal, targeted edits.
- Only modify files directly related to the task.
- Do not rewrite unrelated components, configs, or styles.

- Do not delete existing code or files unless explicitly required.
- Do not perform destructive or irreversible actions.

- Do not add, remove, or update dependencies unless explicitly asked.
- Do not modify config files, environment settings, or build setup unless required.

---

## 🏗 Code & Architecture Rules

- Before editing, inspect the codebase and understand structure, patterns, and dependencies.
- Follow existing architecture and conventions.

- Do not create new files, hooks, utilities, or abstractions unless truly necessary.
- Prefer reusing existing components and patterns.

- Prefer simple and maintainable solutions over complex or over-engineered ones.

- Do not replace working logic with mock data, placeholders, or fake implementations.

---

## 🎨 UI & Frontend Rules

- Build clean, intentional, and well-composed interfaces.
- Avoid generic AI-looking layouts and repetitive sections.

- Always consider responsive design (desktop, tablet, mobile).

- Maintain clear visual hierarchy:
  spacing, typography, grouping, contrast.

- Avoid overdesign:
  no unnecessary gradients, glassmorphism, or random effects.

- Use motion carefully:
  animations should improve clarity, not distract.

- Design should prioritize content, not decoration.

---

## ⚙️ Behavior Rules

- Do not assume things without checking code.
- If something is unclear — make a safe assumption and proceed conservatively.

- For larger changes, prefer step-by-step improvements instead of full rewrites.

- Preserve working functionality over making code “cleaner”.

---

## 🧾 Output Rules

- After making changes, briefly explain:
  - what was changed
  - which files were affected
  - why it was done

- Do not add excessive comments in code.
- Only comment non-obvious logic.

---

# 🧩 SKILLS (INSTALLED SEPARATELY)

This setup uses external skills:

- impeccable → UI generation, audit, polish
- taste-skill → design taste & frontend quality
- design-motion-principles → motion & animation audit

Install via:

npx skills add pbakaus/impeccable
npx skills add Leonxinx/taste-skill

---

# ⚡ HOW TO USE

Typical workflow:

1. Generate UI:
→ use impeccable craft

2. Improve UI:
→ use /polish or /critique

3. Check UX:
→ use /audit

4. Improve animations:
→ ask for motion audit

---

# 🧠 PHILOSOPHY

- Do less, but better
- Respect existing code
- Avoid unnecessary complexity
- Build clean and intentional UI
- Think before changing anything
