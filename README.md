<div align="center">
  <!-- <img src="logo.svg" width="90" alt="lx-0" /> -->

  <h1>skills</h1>

  <p><em>lx-0's PUBLIC plugin catalog for Claude Code and Cursor.</em></p>

  <p>
    A unified marketplace + monorepo of agent skills and bundled plugins.
  </p>

  <p>
    <a href="./LICENSE"><img alt="License" src="https://img.shields.io/badge/license-MIT-blue"></a>
    <img alt="Claude Code" src="https://img.shields.io/badge/Claude%20Code-marketplace-0A0A0A">
    <img alt="Cursor" src="https://img.shields.io/badge/Cursor-marketplace-0A0A0A">
    <img alt="visibility" src="https://img.shields.io/badge/visibility-public-22C55E">
  </p>
</div>

---

## Install

### Claude Code

```bash
/plugin marketplace add lx-0/skills
/plugin
```

Then install plugins individually:

```bash
/plugin install <plugin-name>@lx-0-public-plugins
```

### Cursor

Cursor reads the same marketplace catalog -- the manifest is mirrored at `./.cursor-plugin/marketplace.json`. See [Cursor plugin docs](https://cursor.com/docs/plugins) for the latest install flow.

### Local dev

```bash
git clone https://github.com/lx-0/skills
cd skills
node compile.mjs                       # build .compiled/ + symlinks
/plugin marketplace add ./             # add this repo as a local marketplace
```

No auth required -- this catalog is public.

---

## What's in the catalog

### External

| Plugin | Source | Purpose |
|---|---|---|
| llm-wiki | github `lx-0/llm-wiki` | Cross-project bridge to a local LLM-wiki -- read, diagnose, contribute, maintain, report engine bugs |
| sunoflow | github `lx-0/SunoFlow` | SunoFlow MCP skill -- AI music generation, lyrics, sound effects, stems, music videos, playlist mgmt |

### Adding more

- **Standalone skills** -- drop `SKILL.md` (+ optional `.plugin.json`) into `./skills/<category>/<slug>/`
- **Bundle plugins** -- create `./plugins/<name>/plugin.json` plus optional `skills/`
- **External plugins** (github-hosted) -- add an entry to the `plugins[]` array in `./marketplace.json`

Run `node compile.mjs` after any change. See [CONTRIBUTING.md](./CONTRIBUTING.md) for details.

---

## Compile pipeline

`compile.mjs` discovers `skills/**/SKILL.md`, generates per-skill plugin scaffolds in `.compiled/skill-plugins/`, and produces `.compiled/marketplace.json` from the top-level header (`./marketplace.json`) merged with auto-discovered bundles + standalone.

```bash
node clean.mjs    # wipe .compiled/ + root symlinks
node compile.mjs  # rebuild from sources
```

---

## License

MIT. See [LICENSE](./LICENSE). Listed plugins carry their own license. External plugins are fetched from their upstream repos and not redistributed.

---

Maintained by [lx-0](https://github.com/lx-0).
