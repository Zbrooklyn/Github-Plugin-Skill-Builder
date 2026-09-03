# Roadmap

## V0 — Prove GitHub-hosted plugin skills

Status: in progress

- Publish this repository publicly on GitHub.
- Connect/import it into supported ChatGPT and Claude Code plugin surfaces.
- Prove the `creating-github-plugin-skills` skill is discovered and usable.
- Change the skill in GitHub, sync it, and prove the changed behavior is observed.

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
