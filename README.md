# Elite Taste for Claude Code

Paul Elite's design taste for your coding agent. It refines the UI your project already has (same components, same framework, same brand) and never swaps out your component library.

## Install

In Claude Code:

```
/plugin install elite-taste --marketplace paul-elite/elite-taste-plugin
```

The first time Claude uses Elite Taste, your browser opens so you can log in (or create a free account) and approve it. There's no API key to copy. The free plan includes principles, component guidance and project analysis; audits and refinement plans need Pro.

On Claude Code older than 2.1.275, add the marketplace first:

```
/plugin marketplace add paul-elite/elite-taste-plugin
/plugin install elite-taste@elite-taste
```

## Use

- Ask: *"Apply Elite's taste to this dashboard."* Claude audits the screen, shows you a plan, and edits only after you approve it.
- Run `/elite-taste:setup` in a project to choose the influence level, the brand colours and fonts to keep, density and motion. It writes `.elite-taste.json`, which is safe to commit.
- Sign in again or switch accounts: `/mcp`, choose **elite-taste**, then **Authenticate**. Disconnect it any time from Settings → Connected agents on the website.

## What's in this repo

| Path | What it is |
|---|---|
| `.claude-plugin/marketplace.json` | The marketplace that lists the plugin |
| `plugins/elite-taste/skills/elite-taste/SKILL.md` | How Claude works with Elite Taste: understand the project, plan, get approval, apply, re-audit |
| `plugins/elite-taste/skills/setup/SKILL.md` | `/elite-taste:setup` |
| `plugins/elite-taste/.mcp.json` | Connects to the hosted Elite Taste server; sign-in happens in your browser |

The design rules and the engine run on the hosted server, so this plugin stays small and updates to the taste reach you without reinstalling.

Cursor, Codex and other agents: see [elite-taste.vercel.app/docs](https://elite-taste.vercel.app/docs) or run `npx elite-taste init`.
