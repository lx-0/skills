# AGENTS.md

Contributor guide for AI agents working on this repo. Humans: see [README.md](./README.md) and [CONTRIBUTING.md](./CONTRIBUTING.md).

## What this repo is

`skills` is lx-0's PUBLIC plugin catalog. Two kinds of source content:

- **Standalone skills** under `./skills/<category>/<slug>/SKILL.md` (+ optional `.plugin.json`)
- **Bundle plugins** under `./plugins/<name>/plugin.json` (canonical) with optional `skills/` subfolder

A single Node script (`compile.mjs`) discovers both and produces `.compiled/skill-plugins/` plus `.compiled/marketplace.json`. The marketplace is exposed at `./.claude-plugin/marketplace.json` and `./.cursor-plugin/marketplace.json` via symlinks.

## Hard rules (do not violate)

- **PUBLIC repo. No leaks.** Never write personal info, internal hostnames, private repo names, secrets, or refactor-history phrasing into user-facing fields (descriptions, READMEs, frontmatter).
- **Never edit `.compiled/`.** Always edit sources and run `node compile.mjs`. The generated tree is wiped on every build.
- **Never reintroduce `version` in `plugin.json`.** Rely on git SHA so updates propagate automatically.
- **Slug = parent folder name.** Don't rename folders without updating cross-references; collisions are skipped with a warning.

## Common tasks

| Task | Where to edit |
|---|---|
| Add a standalone skill | `skills/<category>/<slug>/SKILL.md` (+ optional `.plugin.json`), then `node compile.mjs` |
| Add a bundle | `plugins/<name>/plugin.json` (canonical), then `node compile.mjs` |
| Add an external plugin (github-hosted) | `marketplace.json` (top-level, `plugins[]` array), then `node compile.mjs` |
| Tweak top-level catalog metadata | `marketplace.json` (`name`, `description`, `owner`) |

## Build and verify

```bash
node clean.mjs          # wipe .compiled/ + root marketplace symlinks
node compile.mjs        # rebuild from sources
```

Verify after any source change:

```bash
node -e "console.log(JSON.parse(require('fs').readFileSync('.compiled/marketplace.json','utf8')).plugins.length, 'plugins')"
```

## Out of scope

- Plugins that require private infrastructure to function -- those belong in a private catalog, not here.
- Changing the marketplace `name` field (`lx-0-public-plugins`) -- it's the install target for every existing user.
- Auto-bumping versions -- versions are intentionally absent.
