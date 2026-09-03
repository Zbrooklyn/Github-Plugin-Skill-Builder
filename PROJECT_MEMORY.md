# Project Memory

## Serverless plugin package invariant — 2026-09-03

The public repository `Zbrooklyn/Github-Plugin-Skill-Builder` is itself the **complete plugin package host/source of truth** for V0.

The target is a **GitHub-hosted skills-only ChatGPT plugin**: manifests, `SKILL.md` files, Markdown documentation, and supporting resources live in GitHub and are ingested by a compatible ChatGPT GitHub-plugin importer. There is no runtime server in V0.

Canonical root package layout:

```text
Github-Plugin-Skill-Builder/
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
└── skills/
    └── creating-github-plugin-skills/
        └── SKILL.md
```

The marketplace entry uses `"source": "./"`, matching the root-package pattern used by upstream Superpowers.

Do not reintroduce the obsolete nested `plugins/github-plugin-skill-builder/` package unless a future platform requirement explicitly demands it.

Do not add `mcp.json`, `.mcp.json`, a Server URL, an MCP runtime, OAuth backend, database, Worker, or other hosting merely to make the package count as a plugin. OpenAI currently documents that plugins may contain only skills. V0 intentionally tests that path.

The ChatGPT **Add plugin → Server URL** form is a separate MCP/app-creation flow. A static GitHub repository is not an MCP protocol endpoint, and no plugin-manifest edit can make the repository URL valid in that field. The supported GitHub package-ingestion path currently documented by OpenAI is **Workspace settings → Plugins → Add → Import marketplace**.

Therefore:

- repository-format success and personal-Plus installation availability are separate questions;
- if a workspace lacks **Import marketplace**, do not misdiagnose that as a manifest failure;
- V0 is not complete until the repository is imported as a **plugin**, invoked in a normal ChatGPT conversation, and a later GitHub change is observed after marketplace sync.

## Distribution invariant — 2026-09-03

This project must ship as a **ChatGPT plugin that contains skills**, not as a standalone ChatGPT Skill.

Reason: the product requirement is normal ChatGPT chat usage through the plugin surface, for example `@GitHub Plugin Skill Builder` or the ChatGPT plugin picker where supported. A standalone Skill is a different product surface and must not be substituted for this goal.

The intended architecture is:

`GitHub repository → plugin marketplace/manifest → plugin containing skills → installed ChatGPT plugin → normal ChatGPT conversation`

A skills-only plugin is still a plugin. Once an eligible plugin is installed, OpenAI currently documents invoking plugins in ChatGPT through an `@` mention or the plugin picker/`+` menu where supported.

## Standing decision — 2026-09-03

The roadmap must include a reusable **GitHub Repository Management Skill**.

Purpose: prevent future AI sessions from getting blocked when a new repository is required but the currently connected GitHub surface does not expose repository creation.

The skill should cover repository creation and related setup/verification, prefer native connected actions when available, and fall back only in local runtimes where a safely authenticated GitHub API credential already exists. Credentials must never be printed or stored in project files.

Evidence already established: Claude Code previously created `Zbrooklyn/claude-skills` via the GitHub API using the existing Git Credential Manager credential when the `gh` CLI was not installed.

This is a roadmap commitment, not part of V0 implementation. V0 remains intentionally minimal until the GitHub-hosted plugin loop is proven.

## V0 ChatGPT distribution finding — 2026-09-03

The target is the **Superpowers-style plugin model**: a GitHub-hosted plugin package containing reusable skills that can be invoked from normal ChatGPT conversations when the plugin is installed. Do not replace this goal with a standalone MCP server or a one-off uploaded skill.

Important distinction established from current OpenAI documentation and the Superpowers repositories:

- `obra/superpowers` is the upstream public GitHub project and uses a root `.claude-plugin/plugin.json`, root `.claude-plugin/marketplace.json` with `"source": "./"`, and root `skills/` tree.
- OpenAI also maintains curated plugin distribution surfaces; a public GitHub repository by itself does not automatically become installable in every personal ChatGPT workspace.
- OpenAI's documented direct GitHub marketplace import flow is `Workspace settings > Plugins > Add > Import marketplace` and is an administrator/workspace feature.
- The personal Plus UI tested on 2026-09-03 exposes `Add plugin` as the custom MCP app form with Server URL/authentication fields, not the GitHub marketplace importer.
- Therefore the repository/manifests can be valid while the personal Plus workspace still lacks a direct arbitrary-GitHub-plugin installation path.

For a Superpowers-equivalent experience in personal ChatGPT, the remaining distribution problem is getting the plugin onto an installable ChatGPT plugin surface/catalog or testing from a workspace that exposes GitHub marketplace import. Do not change the serverless package architecture to work around a missing importer unless new platform evidence requires it.
