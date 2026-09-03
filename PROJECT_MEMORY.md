# Project Memory

## Standing decision — 2026-09-03

The roadmap must include a reusable **GitHub Repository Management Skill**.

Purpose: prevent future AI sessions from getting blocked when a new repository is required but the currently connected GitHub surface does not expose repository creation.

The skill should cover repository creation and related setup/verification, prefer native connected actions when available, and fall back only in local runtimes where a safely authenticated GitHub API credential already exists. Credentials must never be printed or stored in project files.

Evidence already established: Claude Code previously created `Zbrooklyn/claude-skills` via the GitHub API using the existing Git Credential Manager credential when the `gh` CLI was not installed.

This is a roadmap commitment, not part of V0 implementation. V0 remains intentionally minimal until the GitHub-hosted plugin loop is proven.
