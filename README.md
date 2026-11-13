# 3eAI Labs plugins for Claude Code

This marketplace holds one plugin, **aria-modeler**. It connects Claude Code to
[Aria Modeler](https://products.3eai-labs.com/3e-aria-modeler/), which turns a process you
describe into an executable workflow for UiPath, RPA Framework (Python), Flowable, CadenzaFlow
or CIB seven.

For example, ask Claude: *"Build a UiPath robot that reads the invoices in an Excel file and
emails a summary to the finance team."* Claude designs the steps, Aria checks each one against
its action catalog and generates the workflow files.

Catalog search is free. Generating and changing workflows needs an Aria subscription
(£9 per month) or a promo code. Support: support@3eai-labs.com

## Install

```text
/plugin install aria-modeler --marketplace 3eAI-Labs/aria-claude-plugin
```

On Claude Code older than 2.1.275, add the marketplace first:

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
| `plugins/aria-modeler/skills/aria-loop/SKILL.md` | How Claude searches the catalog, generates and fixes workflows, and reads the generator's warnings |
| `plugins/aria-modeler/README.md` | The plugin's own description: what it contains and what it sends where |

The plugin holds no secret: the OAuth client is public and uses PKCE, and your sign-in token is
kept by Claude Code.

## The live page

A live Aria page, where you see the project's workflows redrawn as Claude changes them and leave
notes for Claude, comes with a later Aria release. The production server does not offer it yet;
the skill uses it only when the server lists its tools.

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

## Terms

The Aria service runs under the Aria Terms of Service:
https://products.3eai-labs.com/3e-aria-modeler/?view=terms

Subscribing asks you to accept the current version in the checkout.

## Privacy

https://3eai-labs.com/en/privacy

## License

MIT, see [LICENSE](LICENSE). The license covers this repository; the Aria Modeler service it
connects to has its own terms.
