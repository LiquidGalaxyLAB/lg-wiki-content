---
title: "How to Contribute to LG Wiki"
contributor: "Dev T Gadani"
date: 2026-07-10T23:30:00.000+00:00
---

## Overview
Welcome! All contributions to LG Wiki are submitted as Markdown files via GitHub Pull Requests. Following these guidelines keeps the documentation unified, readable, and automatically indexed in the portal.

---

## Submission Workflow

### 1. Fork the Repository
Visit [LiquidGalaxyLAB/lg-wiki-content](https://github.com/LiquidGalaxyLAB/lg-wiki-content) and click **Fork** to create your copy.

### 2. Create a Branch
Branch off `main` with a clear, lowercase name like `add/kml-balloon-guide`. Never push directly to `main`.

### 3. Add your Markdown File
Create a new `.md` file inside the `content/` folder (e.g. `content/how-to-orbit.md`).

### 4. Add Images
Save images under `content/images/` and reference them relatively inside your Markdown:
```markdown
![Alt text](images/image-id.jpg)
```

### 5. Update index.json
Add an object entry to `index.json` at the repository root:
```json
{
  "pages": [
    ...
    {
      "id": "how-to-orbit",
      "title": "How to Orbit around a coordinate",
      "file": "how-to-orbit.md"
    }
  ]
}
```

### 6. Open a Pull Request
Push your branch and submit a PR against `main`. Maintainers will review and merge it.

---

## Repository Rules

### Rule 1: File Naming Conventions
Your filename becomes the URL slug. It must be entirely lowercase, using only hyphens as separators. Never use spaces, uppercase, or underscores.
*   **Correct:** `how-to-setup-slaves.md`
*   **Incorrect:** `How_To_Setup_Slaves.MD`

### Rule 2: Required Frontmatter Block
Every article must start with a YAML frontmatter block. Fill out this template:
```yaml
---
title: "Your Article Title"
contributor: "Your Full Name"
date: 2026-07-10T00:00:00.000+00:00
---
```
> [!WARNING]
> If your title contains a colon (e.g. `KML: A Beginner Guide`), wrap the title string in double quotes to prevent YAML parsing crashes.

### Rule 3: Content Structure & Headings
Use proper Markdown heading levels (`##`, `###`) so the "On This Page" TOC sidebar builds automatically. Never use `# h1` as it is reserved for the dynamically generated page title.
*   Do not use bold lines like `**Setup**` as headers. Use `## Setup` instead.

---

## Pre-Submission Checklist
*   [ ] YAML frontmatter contains title, contributor, and date.
*   [ ] Filename is lowercase and ends with `.md`.
*   [ ] File contains at least one `##` heading.
*   [ ] Images are in `content/images/` and referenced relatively.
*   [ ] No external/cloud image links (such as Appwrite or Blogger).
*   [ ] The page entry has been appended to `index.json`.
