---
name: setup
description: Create or update .elite-taste.json for this project (influence level, brand colours and fonts to keep, density, motion, accessibility target). Use when the user wants to configure Elite Taste for a project.
disable-model-invocation: true
---

# Set up Elite Taste for this project

Write `.elite-taste.json` at the project root. Every Elite Taste tool call passes it as `config`.

1. If `.elite-taste.json` already exists, read it and show the current values.
2. Look for the brand before asking: the theme or token file, the Tailwind config, global CSS, and the logo. Propose the brand colours (as hex) and typefaces you find.
3. Ask the user, in one short message, to confirm or change:
   - **Influence**: `balanced` (default), `strict` (apply every rule) or `flexible` (accessibility and must-rules only)
   - **Brand to keep**: the colours and fonts you found, and whether to preserve them (`preserveBrand`, default true)
   - **Density**: `comfortable`, `balanced` or `compact`
   - **Motion**: `none`, `subtle` or `expressive`
   - **Accessibility**: `AA` (default) or `AAA`
4. Write the file in this shape, keeping any `exclude` list that was already there:

```json
{
  "$schema": "https://elite-taste.vercel.app/schema/project-config.json",
  "profile": "paul-elite",
  "influence": "balanced",
  "preserveBrand": true,
  "brand": { "colors": ["#0d6b57"], "fonts": ["Geist"], "notes": "" },
  "density": "balanced",
  "motion": "subtle",
  "accessibility": "AA",
  "exclude": []
}
```

5. Call `get_design_constraints` with the new config and summarise the limits it returns in a few lines, so the user sees what the settings mean.

The file holds no secrets, so it's safe to commit.
