---
name: creating-github-plugin-skills
description: Use when creating, documenting, validating, or publishing a GitHub-hosted plugin skill intended for ChatGPT, Claude Code, or both.
---

# Creating GitHub Plugin Skills

## Purpose

Use one GitHub repository as the maintained source for reusable AI skills that can be distributed through a plugin. Prefer the smallest valid structure and add tools, apps, MCP servers, hooks, or automation only when the skill actually needs them.

## Before Creating Anything

1. Define the job the skill should help with and the situations that should trigger it.
2. Decide whether the target is ChatGPT, Claude Code, or both.
3. Check the current official platform documentation before choosing manifest fields or installation steps. Plugin formats can change.
4. For a shared ChatGPT + Claude Code repository, prefer a Claude-compatible marketplace unless a platform-specific capability requires a separate format.

## Minimal Shared Structure

```text
repo/
├── .claude-plugin/
│   └── marketplace.json
└── plugins/
    └── plugin-name/
        ├── .claude-plugin/
        │   └── plugin.json
        └── skills/
            └── skill-name/
                └── SKILL.md
```

Keep the marketplace entry's `source` pointed at the plugin directory. Keep plugin names consistent between directory names and manifests.

## Writing SKILL.md

Every skill starts with YAML frontmatter containing `name` and `description`.

- Use a lowercase hyphenated name.
- Write the description as a trigger: start with `Use when...` and describe when the skill should load, not the workflow it performs.
- Put the actual workflow in the body.
- Keep the skill concise and searchable.
- Document judgment that an agent needs; mechanize purely mechanical rules when practical.

## Validation Before Publishing

Verify all of the following:

- Every JSON manifest parses successfully.
- Every marketplace `source` path exists.
- Plugin and folder names agree.
- Every skill has valid `name` and `description` frontmatter.
- Installation instructions match current official documentation.
- The repository contains no credentials, tokens, private data, or machine-specific paths.
- The plugin remains skills-only unless another capability is intentionally required.

For ChatGPT web compatibility, be cautious about adding MCP configuration: imported plugins that declare MCP servers can be labeled Desktop only.

## Publishing and Updating

Publish the repository to GitHub only after validation. For ChatGPT workspace import, use the repository URL and the supported manifest at the selected path. For Claude Code, add the repository as a plugin marketplace and install the plugin from that marketplace.

Treat the GitHub repository as the source of truth. Review changes before merging because synced marketplaces can pull later repository updates into installed plugins.

## V0 Rule

When creating a first version, build one useful skill and prove installation, discovery, invocation, and update behavior before adding more infrastructure.
