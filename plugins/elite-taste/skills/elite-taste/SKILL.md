---
name: elite-taste
description: Apply Paul Elite's design taste to the user's existing UI — generate new screens or refine existing ones without replacing their components, framework or brand. Use when the user asks to apply Elite / Paul Elite's taste, design judgment or principles, to "make this look designed", or to review/improve visual hierarchy, spacing, composition or polish of an interface.
---

# Elite Taste

**Your components. Paul's taste.** You change how the user's existing components are styled, composed and laid out. You never swap their component library, never add a UI framework, and never copy showroom code wholesale.

The design intelligence lives on the `elite-taste` MCP server. Fetch what you need, when you need it — don't load everything up front.

| MCP tool | Use it to |
|---|---|
| `analyze_project` | Detect framework, styling, component library, icons, token files |
| `get_design_constraints` | Get the measurable limits for this project (weights, scale, contrast, radii) and what to preserve |
| `get_layout_guidance` | Page-level rules for a page type (dashboard, settings, landing, library, mobile…) |
| `get_component_guidance` | Rules, patterns and anti-patterns for one component in a context |
| `get_visual_references` | Showroom examples that show the intent (look, don't copy) |
| `audit_interface` | Static audit of UI files → findings, scores, caveats |
| `suggest_refinements` | Ordered plan (tokens → components → screens) from an audit |
| `get_principles` | The whole philosophy, or one category |

If the server isn't connected or returns `unauthenticated`, the API key is missing or wrong. Plugin users: run `/plugin`, open **elite-taste**, choose **Configure** and paste a key from https://elite-taste.vercel.app/dashboard/keys. Everyone else: run `npx elite-taste init` and set `ELITE_TASTE_API_KEY`. If a tool returns `plan`, say which tool needs Pro and continue with what's available.

## Step 0 — Understand the project (always)

1. Read `.elite-taste.json` if it exists (influence, preserveBrand, brand colours/fonts, density, motion, accessibility, exclude). Pass it as `config` on every call.
2. Call `analyze_project` with `package.json` and the paths (plus contents, if small) of: tailwind config / global CSS / theme or token files / `components/ui/*` / the files the user mentioned.
3. Call `get_design_constraints`. These are your guard rails for the rest of the task.
4. Note what must not change: behaviour, data flow, props, routes, accessibility attributes, and (if `preserveBrand`) brand colours, logo and typefaces.

## Generation mode — "build this page with Elite's taste"

1. `get_layout_guidance` for the page type and target viewport.
2. `get_component_guidance` for each distinct component you'll compose (not for every instance).
3. Build with the project's own components and tokens. Where a token is missing, add it to the token file instead of hard-coding a value.
4. Run `audit_interface` on the files you wrote. Fix every `high` finding before you show the result.
5. Render it (dev server + screenshot, or ask the user to) and check it at mobile and desktop widths.

## Refinement mode — "refine / review this interface"

1. `suggest_refinements` with the relevant files (≤ 40, UI files only) and the user's goal.
2. **Show the plan and wait for approval.** Present it as a short numbered list: what changes, why (rule + rationale), risk. The user may drop steps.
3. Make sure changes are revertable: if the tree is dirty, ask before continuing; suggest a branch or `git stash`.
4. Apply one step at a time with your own file tools, tokens first. Keep diffs minimal: change classes, variants and tokens, not component structure, unless the plan says otherwise.
5. Re-run `audit_interface`. Report the score change and any remaining findings.
6. Render before/after screenshots. Only call a change a visual improvement after you've looked at the rendered result. If you couldn't render, say "not visually verified".
7. Tell the user how to revert (`git diff`, `git checkout -- <file>`, or drop the branch).

## How to talk about the rules

- Rules with `confidence: "unconfirmed"` come from Paul's shipped work and await his sign-off. Say "Paul's work tends to…", not "Paul's rule is…".
- Explain significant decisions in one line each, citing the rule id (e.g. `surfaces.flat-by-default`).
- When a preference conflicts with a project constraint, the project wins; mention the trade-off.
- Accessibility (`kind: universal`) always wins.

## Influence levels

- **strict** — apply every live rule; keep brand tokens, change nearly everything else.
- **balanced** (default) — must/should rules; existing components and tokens win ties.
- **flexible** — accessibility and must-rules only; everything else is a suggestion you list but don't apply.

## Don'ts

- Don't install a component library or rewrite components from the showroom.
- Don't add demo/fake data to make a screen look full — design the empty state (`content.real-content-only`).
- Don't claim "verified" for anything the static audit can't see.
- Don't touch files unrelated to the UI you were asked about.
