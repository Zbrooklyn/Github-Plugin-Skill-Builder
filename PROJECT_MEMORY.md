# Project Memory

## Standing decision — 2026-09-03

The roadmap must include a reusable **GitHub Repository Management Skill**.

Purpose: prevent future AI sessions from getting blocked when a new repository is required but the currently connected GitHub surface does not expose repository creation.

The skill should cover repository creation and related setup/verification, prefer native connected actions when available, and fall back only in local runtimes where a safely authenticated GitHub API credential already exists. Credentials must never be printed or stored in project files.

Evidence already established: Claude Code previously created `Zbrooklyn/claude-skills` via the GitHub API using the existing Git Credential Manager credential when the `gh` CLI was not installed.

This is a roadmap commitment, not part of V0 implementation. V0 remains intentionally minimal until the GitHub-hosted plugin loop is proven.

## V0 ChatGPT distribution finding — 2026-09-03

The target is the **Superpowers-style plugin model**: a GitHub-hosted plugin package containing reusable skills that can be invoked from normal ChatGPT conversations when the plugin is installed. Do not replace this goal with a standalone MCP server or a one-off uploaded skill.

Important distinction established from current OpenAI documentation and the Superpowers repositories:

- `obra/superpowers` is the upstream public GitHub project.
- OpenAI also maintains a curated packaged copy under `openai/plugins/plugins/superpowers`.
- A public GitHub repository by itself does **not** automatically become installable in a personal ChatGPT workspace.
- OpenAI's documented direct GitHub marketplace import flow is `Workspace settings > Plugins > Add > Import marketplace` and is an administrator/workspace feature.
- The personal Plus UI tested on 2026-09-03 exposes `Add plugin` as the custom MCP app form (Server URL + authentication), not the GitHub marketplace importer.
- Therefore the repository/manifests can be valid while the personal Plus workspace still lacks a direct arbitrary-GitHub-plugin installation path.

For a Superpowers-equivalent experience in personal ChatGPT, the missing distribution step is getting the plugin into an installable ChatGPT plugin catalog/surface, or testing from a workspace that exposes GitHub marketplace import. Do not misdiagnose this as a manifest or repository failure.
