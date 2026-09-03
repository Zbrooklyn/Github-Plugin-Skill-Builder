# Roadmap

## Product invariant

This project ships as a **ChatGPT plugin containing skills**, not as a standalone ChatGPT Skill.

Acceptance requires normal ChatGPT plugin usage when installed (for example via `@GitHub Plugin Skill Builder` or the ChatGPT plugin picker where supported). A standalone Skill install does not satisfy V0.

Do not add an MCP server merely to satisfy plugin packaging. The target is a skills-only plugin unless executable tools are genuinely required later.

## V0 — Prove GitHub-hosted plugin skills

Status: in progress — repository is published and valid; ChatGPT import is blocked on an eligible workspace surface

Completed:

- Publish this repository publicly on GitHub.
- Verify the marketplace manifest, plugin manifest, skill frontmatter, repository visibility, and default branch from GitHub.
- Lock the requirement that this must be installed as a plugin containing skills, not as a standalone Skill.

Remaining:

- Import the marketplace into an eligible ChatGPT workspace using `Workspace settings > Plugins > Add > Import marketplace`.
- Install the imported `GitHub Plugin Skill Builder` as a plugin.
- Prove it is invokable from a normal ChatGPT conversation through the plugin surface.
- Prove the `creating-github-plugin-skills` skill inside the plugin is discovered and usable.
- Change the skill in GitHub, select `Sync now`, and prove the changed behavior is observed.

Current ChatGPT constraint verified on 2026-09-03: OpenAI documents GitHub marketplace import as a workspace-admin capability. A personal Plus workspace may not expose the import control. The plugin is also not in the public Plugin Directory, so there is no catalog-install fallback yet.

## V1 — GitHub Repository Management Skill

Status: planned — priority next capability

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
- compatibility tests across ChatGPT surfaces;
- additional reusable plugin-building skills based on real failures and repeated needs.
