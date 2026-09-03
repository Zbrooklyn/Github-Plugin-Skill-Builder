# GitHub Plugin Skill Builder

A public GitHub-hosted **skills-only plugin** for ChatGPT-compatible plugin workflows.

The repository itself is the plugin package and source of truth. There is no runtime server, MCP endpoint, OAuth backend, database, or other hosting layer in V0.

Informally, this is the **serverless plugin** pattern: GitHub hosts the manifests, skills, Markdown instructions, and supporting documentation that a compatible plugin importer ingests.

## What this project is proving

The experiment is deliberately narrow:

> Can one public GitHub repository be the complete source package for a ChatGPT plugin containing reusable skills, without operating a traditional plugin/MCP server?

The intended flow is:

```text
Public GitHub repository
        ↓
plugin marketplace + plugin manifest
        ↓
skills/ + Markdown documentation
        ↓
ChatGPT GitHub plugin importer
        ↓
installed plugin
        ↓
normal ChatGPT plugin usage
```

This must be installed as a **plugin containing skills**, not as a standalone ChatGPT Skill.

## Repository structure

The repository root is the plugin package, following the same root-package pattern used by Superpowers:

```text
Github-Plugin-Skill-Builder/
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
├── skills/
│   └── creating-github-plugin-skills/
│       └── SKILL.md
├── INSTALL-CHATGPT.md
├── README.md
├── ROADMAP.md
├── PROJECT_MEMORY.md
└── LICENSE
```

The marketplace entry uses:

```json
"source": "./"
```

That means the repository root itself is the plugin source.

## ChatGPT installation

On a ChatGPT workspace that exposes GitHub marketplace import:

1. Open **Workspace settings → Plugins**.
2. Select **Add → Import marketplace**.
3. Use this repository as Source:

```text
https://github.com/Zbrooklyn/Github-Plugin-Skill-Builder
```

4. Leave **Path** blank.
5. Leave **Branch/tag/commit** blank to follow the default `main` branch, or pin a revision when fixed behavior is desired.
6. Import the marketplace, open **GitHub Plugin Skill Builder**, and install/enable the plugin for the intended role.

See [`INSTALL-CHATGPT.md`](INSTALL-CHATGPT.md) for the exact test procedure.

### Important: the MCP "Server URL" form is different

If **Add plugin** opens a form asking for **Server URL**, authentication, OAuth, or custom headers, that is the MCP/app creation path. Do **not** paste this GitHub repository URL into that field.

A static GitHub repository is not an MCP protocol endpoint, and no manifest change can make a repository URL behave like one. This project intentionally avoids an MCP server because V0 is a skills-only plugin.

OpenAI currently documents GitHub repositories through the separate **Import marketplace** flow. Availability of that flow depends on account/workspace/role/rollout.

## V0 skill

The first plugin skill is:

```text
creating-github-plugin-skills
```

It documents the minimal GitHub-hosted plugin structure, skill-authoring rules, validation checks, and publishing approach we will use when building future plugins.

For objective installation testing, the skill contains this exact diagnostic prompt:

```text
Run GitHub Plugin Skill Builder V0 test
```

A correctly loaded skill must begin its answer with:

```text
GitHub Plugin Skill Builder V0 — skill active
```

## Why there is no MCP server

A plugin can package skills without connecting an external app. V0 therefore has no `mcp.json`, `.mcp.json`, Server URL, or executable backend.

This is intentional. Adding MCP configuration just to make the repository "feel" like a plugin would change the architecture and can limit where an imported plugin runs.

If a future skill genuinely needs executable external actions, that capability can be added deliberately as a later layer. It is not required for the GitHub-hosted skills-only experiment.

## GitHub is the source of truth

The maintained content lives here. The target update loop is:

```text
edit GitHub → merge → plugin marketplace sync → changed behavior in ChatGPT
```

V0 is not considered proven until we observe that full loop from an eligible ChatGPT plugin surface.

## V0 status

Repository packaging:

- public GitHub source: complete
- root marketplace manifest: complete
- root plugin manifest: complete
- root `skills/` package: complete
- no runtime/MCP server: confirmed by design
- deterministic invocation diagnostic: complete

External proof still required:

- import this repository into a ChatGPT workspace that exposes GitHub marketplace import;
- install it as a plugin;
- invoke it from a normal ChatGPT conversation;
- verify the V0 diagnostic;
- change the GitHub skill, run marketplace sync, and observe the changed behavior.

## Next capability

After V0 is proven, the priority next skill is a **GitHub Repository Management Skill** inside this plugin. It will formalize safe repository creation, initialization, credential handling, connected/local execution differences, and read-back verification.

See [`ROADMAP.md`](ROADMAP.md) and [`PROJECT_MEMORY.md`](PROJECT_MEMORY.md).

## Compatibility

The package uses the Claude-compatible plugin marketplace format because OpenAI's GitHub marketplace importer currently supports `.claude-plugin/marketplace.json` and `.claude-plugin/plugin.json`. The root layout also mirrors the upstream Superpowers packaging pattern.

Before changing manifest fields or installation instructions, verify the current platform documentation because the plugin ecosystem is evolving.

## References

- OpenAI Help — Importing and syncing plugin marketplaces from GitHub: https://help.openai.com/en/articles/20001504
- OpenAI Help — Plugins in ChatGPT and Codex: https://help.openai.com/en/articles/20001256
- Superpowers upstream repository: https://github.com/obra/superpowers

## License

MIT
