# Roadmap

## V0 — Prove GitHub-hosted plugin skills

Status: in progress — repository is published and valid; ChatGPT import is blocked on an eligible workspace surface

Completed:

- Publish this repository publicly on GitHub.
- Verify the marketplace manifest, plugin manifest, skill frontmatter, repository visibility, and default branch from GitHub.

Remaining:

- Import the marketplace into an eligible ChatGPT workspace using `Workspace settings > Plugins > Add > Import marketplace`.
- Prove the `creating-github-plugin-skills` skill is discovered and usable.
- Change the skill in GitHub, select `Sync now`, and prove the changed behavior is observed.
- Prove the same marketplace/skill path in Claude Code.

Current ChatGPT constraint verified on 2026-09-03: OpenAI documents GitHub marketplace import as a workspace-admin capability, and Skills are currently documented for eligible Business, Enterprise, Healthcare, and Edu accounts. A personal Plus workspace may not expose the import control. The plugin is also not in the public Plugin Directory, so there is no catalog-install fallback yet.

## V1 — GitHub Repository Management Skill

Status: planned — priority next capability

Create a reusable skill for managing GitHub repositories end to end, including:

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
- compatibility tests across ChatGPT, Claude Code, and Codex;
- additional reusable plugin-building skills based on real failures and repeated needs.
