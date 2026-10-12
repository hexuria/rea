# REA — Devin plugin

Devin plugin bundle for [REA](https://github.com/morluto/rea): the
`reverse-engineer-anything` skill plus a declaration for the REA MCP server.

## Install

In the Devin web app: **Customize → Plugins → Add plugin → From repository**

- Repository: `hexuria/rea`
- Subdirectory: `plugins/rea`

CLI equivalent:

```sh
devin plugins install hexuria/rea#plugins/rea
```

Install this subdirectory, not the repository root. The repo-root `AGENTS.md`
is REA-development guidance, and a root-level install would inject it as an
always-on rule into every session where the plugin is enabled.

## What it loads

- Skill `reverse-engineer-anything`, invoked as `/rea:reverse-engineer-anything`.
- MCP server `rea`: `npx -y rea-agents@latest mcp` (stdio). It starts with each
  session where the plugin is enabled; the machine needs Node.js/npm on `PATH`
  and access to the npm registry. If the server cannot start, the skill's
  `npx -y rea-agents@latest` CLI fallback still applies.

## Contents and re-sync

`skills/reverse-engineer-anything/` is a verbatim copy of the authored source
at `.agents/skills/reverse-engineer-anything/` (without the build-time
`tool_count` and pinned package specifier the release pipeline adds). After
pulling upstream changes that touch the source skill, re-sync with:

```sh
cp -r .agents/skills/reverse-engineer-anything plugins/rea/skills/
```

The repository-internal skills (`rea-changelog-update`, `rea-tool-design`) are
intentionally not shipped: they target REA development, not REA users.
