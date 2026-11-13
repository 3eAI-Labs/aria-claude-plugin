# Aria Modeler

Describe a business process to Claude and get an executable workflow for UiPath, RPA
Framework (Python), Flowable, CadenzaFlow or CIB seven. Claude designs the process with its own
model; [Aria Modeler](https://products.3eai-labs.com/3e-aria-modeler/) checks every step against
its action catalog and generates the workflow files. Aria calls no language model on this path,
so you need no LLM API key.

A live Aria page, where you see the project's workflows redrawn as Claude changes them and leave
notes for Claude, comes with a later Aria release. The production server does not offer it yet;
the skill uses it only when the server lists its tools.

## Install in Claude Code

```text
/plugin install aria-modeler --marketplace 3eAI-Labs/aria-claude-plugin
```

This adds the `3eai-labs` marketplace and installs the plugin in one step (Claude Code 2.1.275 or
later).

## What you need

- An Aria account. Catalog search works before you sign in; generating and changing workflows
  needs an Aria subscription (£9 per month) or a promo code.
- In Claude Code, sign in once: `/mcp` → `plugin:aria-modeler:aria-modeler` → **Authenticate**.
  Your browser opens the Aria sign-in page and Claude Code receives the result on
  `localhost:8765`.

## What the plugin contains

- **One remote MCP server**, `https://products.3eai-labs.com/3e-aria-modeler/mcp`, operated by
  3eAI Labs Ltd. It uses the public OAuth client `aria-modeler-mcp-claude-code` with PKCE.
- **One skill**, `aria-loop`, which tells Claude how to search the catalog, generate and fix
  workflows and read the generator's warnings; once the server offers the live page, also how to
  open it and read your notes.

The plugin has no hooks, no commands, no local programs and no secrets.

## What is sent where

Everything goes to the Aria MCP server above, and only when Claude calls one of its tools:

- the process definitions, workflow names and step parameters Claude writes for you;
- once the live Aria page is available, the notes and the selection you make on it;
- your Aria sign-in token, which Claude Code keeps and sends with each call.

Aria stores your projects, workflows and notes in your Aria account. Aria refuses content that
looks like a credential, so never put passwords or keys in a process description or a note.
When Claude opens the live page, the skill may ask it to run your system's browser opener
(`xdg-open`, `open` or `start`) with the page link, and only for a link on
`https://products.3eai-labs.com/3e-aria-modeler/`; any other link is shown, not opened.

Privacy policy: https://3eai-labs.com/en/privacy

Support: support@3eai-labs.com

## License

MIT. The license covers this plugin; the Aria Modeler service has its own terms.
