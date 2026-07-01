# Corepass Code plugin template

Build and publish Corepass Code (`harness`) marketplace plugins from a single repo.
The layout mirrors [Cursor's plugin-template](https://github.com/cursor/plugin-template);
manifests live under `.corepass-plugin/` and also load from `.claude-plugin/` /
`.cursor-plugin/` for cross-ecosystem compatibility.

Two starter plugins are included:

- **starter-simple**: rules and skills only
- **starter-advanced**: rules, skills, agents, commands, hooks, MCP, and scripts

## Getting started

1. Push this repo to your own git host.
2. `.corepass-plugin/marketplace.json`: set marketplace `name`, `owner`, `metadata`,
   and one entry per plugin (`name`, `source`, `description`, optional `category` /
   `featured` for the storefront).
3. `plugins/*/.corepass-plugin/plugin.json`: set `name` (lowercase kebab-case),
   `displayName`, `author`, `description`, `keywords`, `license`, `version`, `logo`.
4. Replace the placeholder rules, skills, agents, commands, hooks, scripts, and logos.

Add more plugins: see [`docs/add-a-plugin.md`](docs/add-a-plugin.md).

## Install it

```bash
harness marketplace add <this repo url> --name my-marketplace
harness plugin install starter-advanced@my-marketplace
```

Or in the desktop app: Plugins → Marketplace sources → Add, then Browse
(search + category groups) → Install, and Manage to enable/disable.

## What loads in Corepass Code

The harness registers **skills/** (`<name>/SKILL.md`), **agents/** (`*.md`),
**tools/** (`*.py`), plus manifest-declared MCP servers and hooks. `rules/` and
`commands/` are part of the Cursor layout and are carried for portability, but do
not map to a Corepass Code registry yet — they are ignored on load.

## Layout

```
.corepass-plugin/marketplace.json        # storefront index
docs/add-a-plugin.md
scripts/validate-template.mjs            # node scripts/validate-template.mjs
plugins/
  starter-simple/
    .corepass-plugin/plugin.json         # runtime manifest (author {} / logo tolerated)
    rules/coding-standards.mdc
    skills/code-reviewer/SKILL.md
    assets/logo.svg
    README.md
  starter-advanced/
    .corepass-plugin/plugin.json
    rules/*.mdc
    skills/code-reviewer/SKILL.md
    agents/security-reviewer.md
    commands/deploy-staging.md
    hooks/hooks.json
    scripts/*.sh
    mcp.json
    assets/logo.svg
    README.md
```

## Submission checklist

- Each plugin has a valid `.corepass-plugin/plugin.json`.
- Plugin names are unique, lowercase, and kebab-case.
- `.corepass-plugin/marketplace.json` entries map to real plugin folders.
- Frontmatter metadata is present in rule, skill, agent, and command files.
- Logos are committed and referenced with relative paths.
- `node scripts/validate-template.mjs` passes.
