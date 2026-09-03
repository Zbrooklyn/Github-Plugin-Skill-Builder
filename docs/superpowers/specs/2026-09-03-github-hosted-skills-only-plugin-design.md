# GitHub-Hosted Skills-Only Plugin Design

## Goal

Make the repository itself the complete source package for a ChatGPT plugin that contains skills, with no runtime server, MCP endpoint, database, OAuth backend, or other hosted application required.

## Product invariant

This ships as a **plugin containing skills**, not as a standalone ChatGPT Skill.

Success means an eligible ChatGPT workspace can import this GitHub repository as a plugin marketplace/package, install the resulting plugin, and invoke it from normal ChatGPT plugin surfaces. Installing only the underlying skill does not satisfy V0.

## Architecture

The repository root is the plugin package, matching the upstream Superpowers layout:

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
└── PROJECT_MEMORY.md
```

The marketplace entry uses `"source": "./"`, so the repository root is both the GitHub source of truth and the plugin package.

## Distribution model

OpenAI's GitHub marketplace importer is the supported ingestion path for this serverless package. The repository URL is the distribution identifier; no Server URL exists because there is no MCP server.

The current personal Plus `Add plugin` form that requests a Server URL is a different MCP-app flow and cannot be made to accept a static GitHub repository by changing plugin manifests. The package remains ready for any ChatGPT surface that exposes GitHub marketplace import or for later catalog distribution.

## Runtime boundaries

V0 intentionally contains no `mcp.json`, `.mcp.json`, server declaration, app template, or remote executable component. This preserves the skills-only plugin model and avoids unintentionally making the plugin Desktop-only.

## V0 behavior

The plugin contains one skill, `creating-github-plugin-skills`. It retains the deterministic diagnostic phrase `Run GitHub Plugin Skill Builder V0 test` so installation and invocation can be proven objectively.

## Acceptance criteria

1. `.claude-plugin/marketplace.json` exists at repository root and points to `"source": "./"`.
2. `.claude-plugin/plugin.json` exists at repository root.
3. `skills/creating-github-plugin-skills/SKILL.md` exists at repository root.
4. The old nested `plugins/github-plugin-skill-builder/` package is removed.
5. README and installation docs describe this as a GitHub-hosted skills-only plugin, not an MCP server or standalone Skill.
6. No MCP configuration file is present.
7. Repository remains public with default branch `main`.
8. An eligible ChatGPT GitHub-import surface can be given only `https://github.com/Zbrooklyn/Github-Plugin-Skill-Builder` with no subdirectory path.
