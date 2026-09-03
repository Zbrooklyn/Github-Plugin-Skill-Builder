# GitHub Plugin Skill Builder

A minimal reference project for creating reusable AI skills that live in GitHub and can be distributed as plugins to ChatGPT and Claude Code.

The first version intentionally contains one meta-skill: **creating-github-plugin-skills**. Its job is to document the process we will use to create future GitHub-hosted plugin skills correctly.

## Why this project exists

Instead of copying skill instructions between AI products, the goal is to keep the maintained version in GitHub and let supported products import or sync that source.

This repository uses a Claude-compatible marketplace because OpenAI currently supports `.claude-plugin/marketplace.json` as a GitHub marketplace import format, while the same marketplace structure is usable by Claude Code.

## Structure

```text
github-plugin-skill-builder/
├── .claude-plugin/
│   └── marketplace.json
└── plugins/
    └── github-plugin-skill-builder/
        ├── .claude-plugin/
        │   └── plugin.json
        └── skills/
            └── creating-github-plugin-skills/
                └── SKILL.md
```

The actual repository root is `github-plugin-skill-builder/`; the tree above shows the files beneath it.

## What V0 proves

V0 is deliberately small. It is meant to prove five things before the project grows:

1. GitHub can be the source of truth.
2. The marketplace and plugin manifests are accepted.
3. The skill is discovered when its trigger applies.
4. The skill's instructions are usable in practice.
5. A later GitHub change can be synced and observed.

## ChatGPT

OpenAI currently allows workspace administrators to import plugin marketplaces from public or private GitHub repositories.

1. Open **Workspace settings → Plugins**.
2. Select **Add → Import marketplace**.
3. Enter the repository URL: `https://github.com/Zbrooklyn/Github-Plugin-Skill-Builder`.
4. Leave Path empty because the marketplace manifest is at the repository root.
5. Choose the default branch for ongoing updates, or pin a tag/commit when you want fixed behavior.
6. Import the marketplace and review the resulting plugin before making it available.

Availability depends on the ChatGPT plan, workspace, role, and rollout. Personal ChatGPT accounts do not necessarily expose workspace marketplace import controls.

## Claude Code

After the repository is public, add the marketplace and install the plugin:

```text
/plugin marketplace add Zbrooklyn/Github-Plugin-Skill-Builder
/plugin install github-plugin-skill-builder@github-plugin-skill-builder
```

## Creating the next skill

Once this plugin is installed, ask the AI to create a GitHub-hosted plugin skill. The `creating-github-plugin-skills` skill should provide the baseline structure, authoring rules, validation checklist, and publishing approach.

The project should then improve itself only from evidence gathered while creating and testing real skills.

## Roadmap

The next planned reusable capability is a **GitHub Repository Management Skill**. It will formalize repository creation, initialization, connected/local fallback behavior, credential safety, and read-back verification so future plugin projects do not depend on manual repository setup. See [`ROADMAP.md`](ROADMAP.md) and [`PROJECT_MEMORY.md`](PROJECT_MEMORY.md).

## V0 boundaries

Not included yet:

- MCP servers
- connected apps
- hooks
- code generators
- CI/CD
- automated publishing
- multiple plugins

Those should only be introduced after the minimal GitHub → plugin → skill loop is proven.

## Sources of truth

Before changing the format, verify current platform documentation. The plugin ecosystem is evolving and repository documentation should not be treated as permanently correct.

- OpenAI Help: Plugins in ChatGPT and Codex
- OpenAI Help: Importing and syncing plugin marketplaces from GitHub
- OpenAI's `openai-developers-for-claude` repository as a public marketplace/plugin structure example

## License

MIT
