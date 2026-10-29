# 3eAI Labs plugins for Claude Code

This marketplace holds one plugin, **aria-modeler**. It connects Claude Code to
[Aria Modeler](https://products.3eai-labs.com/3e-aria-modeler/), which turns a process you
describe into an executable workflow for UiPath, Python Code, Flowable, CadenzaFlow or
CIB seven, and opens the live Aria page where you and Claude work on it together.

## Install

```text
/plugin marketplace add 3eAI-Labs/aria-claude-plugin
/plugin install aria-modeler@3eai-labs
```

A user-scope install serves the terminal, the Code tab of Claude Desktop and the IDE
extensions.

Then sign in: `/mcp` → `plugin:aria-modeler:aria-modeler` → **Authenticate**. Your browser
opens the Aria sign-in page and Claude Code receives the result on `localhost:8765`. Catalog
tools work before sign-in; generating and changing workflows needs your Aria subscription or
promo grant. Claude's own model designs the workflow, so no LLM API key is involved.

## What the plugin contains

| Path | Purpose |
|---|---|
| `plugins/aria-modeler/.mcp.json` | The Aria MCP server (`https://products.3eai-labs.com/3e-aria-modeler/mcp`) with the public OAuth client `aria-modeler-mcp-claude-code` and callback port 8765 |
| `plugins/aria-modeler/skills/aria-loop/SKILL.md` | How Claude searches the catalog, generates and fixes workflows, opens the live page and reads your notes |

The plugin holds no secret: the OAuth client is public and uses PKCE, and your sign-in token is
kept by Claude Code.

## The live page

When a project exists, Claude calls `open_workspace` and gives you a link to the Aria page.
The page shows every workflow of the project and redraws it each time Claude changes it. Select
a workflow or a step and leave a note; Claude reads your notes at the start of your next turn,
and the page marks them as read. The page cannot start a turn by itself.

## Already added Aria by hand?

If you registered the same server earlier with `claude mcp add ... aria-modeler`, remove that
entry after installing the plugin so Claude sees one Aria server:

```text
claude mcp remove aria-modeler --scope user
```

## Check before publishing

```bash
claude plugin validate .
claude plugin validate ./plugins/aria-modeler
```

## Privacy

https://3eai-labs.com/en/privacy

## License

MIT, see [LICENSE](LICENSE). The license covers this repository; the Aria Modeler service it
connects to has its own terms.
