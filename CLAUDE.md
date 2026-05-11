# CLAUDE.md — tj-claude-skills

This repo holds custom Claude Code skill files (`.md`) and a GitHub Pages site
(`docs/index.html`) that lets anyone browse and copy them.

---

## Adding a new skill

When the user creates a new skill, you must update **three places** in this repo:

### 1. Create the skill file

Save the skill as `<skill-name>.md` at the repo root. The file must have YAML
frontmatter with at least `name` and `description`.

### 2. Add a card to `docs/index.html`

Copy the existing skill card block (marked with a comment) and paste it above
the `<!-- ADD NEW SKILL CARDS ABOVE THIS LINE -->` comment. Fill in:

- `data-skill` on the `<button>` — must exactly match the key you add in step 3
- `.skill-name` text — the slash-command name (without the `/`)
- `.tag` elements — 2–4 short tags describing the skill's domain
- `.skill-desc` text — 2–3 sentence plain-English summary
- `href` on the View raw link — GitHub URL to the raw `.md` file

```html
<div class="skill-card">
  <div class="card-top">
    <div class="card-meta">
      <div class="skill-name">your-skill-name</div>
      <div class="skill-tags">
        <span class="tag">tag one</span>
        <span class="tag">tag two</span>
      </div>
    </div>
  </div>
  <p class="skill-desc">
    Plain-English description of what this skill does and when to use it.
  </p>
  <div class="card-actions">
    <button class="copy-btn" data-skill="your-skill-name">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><rect x="9" y="9" width="13" height="13" rx="2"/><path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"/></svg>
      Copy skill
    </button>
    <a class="view-link" href="https://github.com/tjensen8/tj-claude-skills/blob/main/your-skill-name.md" target="_blank">View raw →</a>
  </div>
</div>
```

### 3. Add the skill content to the `SKILLS` object in `docs/index.html`

At the bottom of `docs/index.html`, inside the `SKILLS` object, add an entry
above the `// ADD NEW SKILL CONTENT ENTRIES ABOVE THIS LINE` comment:

```js
"your-skill-name": `<full raw markdown content of the .md file here>`,
```

The key must exactly match the `data-skill` attribute on the card's copy button.
The value is the complete raw text of the `.md` file, as a JS template literal.
Escape any backticks inside with `\``.

### 4. Update the README

Add a row to the Skills table in `README.md`:

```md
| [your-skill-name](your-skill-name.md) | One-line description |
```

### 5. Commit

Stage all changed files and commit with a message like:
```
Add <skill-name> skill
```

---

## Enabling GitHub Pages (first-time setup)

Go to the repo on GitHub → Settings → Pages → Source: **Deploy from a branch**,
branch: `main`, folder: `/docs`. The site will be live at
`https://tjensen8.github.io/tj-claude-skills/`.
