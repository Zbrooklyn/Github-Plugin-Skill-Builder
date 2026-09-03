# Roadmap

## Product invariant

This project ships as a **ChatGPT plugin containing skills**, not as a standalone ChatGPT Skill.

Acceptance requires normal ChatGPT plugin usage when installed, for example through `@GitHub Plugin Skill Builder` or the ChatGPT plugin picker where supported. A standalone Skill install does not satisfy V0.

The V0 architecture is deliberately **skills-only and serverless**: the public GitHub repository is the plugin package host/source of truth. Do not add an MCP server merely to satisfy plugin packaging.

## V0 — Prove the GitHub-hosted skills-only plugin loop

Status: **in progress — GitHub root-package refactor complete; external ChatGPT import/invocation/sync proof remains**

Completed:

- Publish the repository publicly on GitHub.
- Make the repository root the plugin package, following the Superpowers-style layout.
- Add root `.claude-plugin/marketplace.json` with `"source": "./"`.
- Add root `.claude-plugin/plugin.json`.
- Move `creating-github-plugin-skills` to root `skills/`.
- Remove the obsolete nested `plugins/github-plugin-skill-builder/` package.
- Preserve the deterministic V0 invocation diagnostic.
- Add exact ChatGPT GitHub-marketplace installation and sync instructions.
- Lock the requirement that this installs as a plugin containing skills, not as a standalone Skill.
- Lock the requirement that V0 uses no MCP server, Server URL, app template, OAuth backend, database, or runtime hosting.

Remaining external acceptance tests:

- Use a ChatGPT workspace/account surface that exposes **Workspace settings → Plugins → Add → Import marketplace**.
- Import `https://github.com/Zbrooklyn/Github-Plugin-Skill-Builder` with Path blank.
- Install the imported **GitHub Plugin Skill Builder** plugin.
- Invoke it from a normal ChatGPT conversation through the plugin surface.
- Send `Run GitHub Plugin Skill Builder V0 test` and observe the exact diagnostic marker from the GitHub-hosted skill.
- Change the diagnostic marker in GitHub, select **Sync now**, and prove the changed behavior is observed in ChatGPT.

Current distribution constraint verified on 2026-09-03: OpenAI documents GitHub marketplace import as a workspace-admin import path. The personal Plus UI tested in this project exposes **Add plugin** as the custom MCP Server URL form instead of **Import marketplace**. That Server URL form cannot use a static GitHub repository URL; this is a product/distribution-surface limitation, not a repository-format failure.

## V1 — GitHub Repository Management Skill

Status: planned — priority next capability after V0 proof

Add a reusable GitHub repository-management skill **inside this plugin**, covering:

- create a new repository under the authenticated user's account or organization;
- choose public/private visibility intentionally;
- set repository name and description;
- initialize an empty repository safely;
- connect a local project and push its first commit;
- create/update repository files when a connector supports it;
- use the GitHub REST API when repository creation is not exposed by the current connector and an existing authenticated credential is safely available;
- never print, persist, or expose access tokens;
- verify the repository exists, has the intended visibility/default branch, and contains the expected files before claiming completion;
- distinguish what can be done from ChatGPT connectors versus what requires a local Claude Code/Codex runtime.

This requirement comes from a proven real workflow: Claude Code previously created `Zbrooklyn/claude-skills` through the GitHub API using the existing Git Credential Manager credential when `gh` was unavailable. The capability should be formalized instead of rediscovered ad hoc.

## Later — only after the core loop is proven

- automated manifest validation;
- CI checks for plugin structure and skill frontmatter;
- versioning/release conventions;
- public/catalog distribution investigation for personal ChatGPT installation;
- compatibility tests across ChatGPT surfaces;
- additional reusable plugin-building skills based on real failures and repeated needs.
