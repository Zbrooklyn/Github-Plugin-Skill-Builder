# GitHub-Hosted Skills-Only Plugin Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Refactor the repository so the GitHub repository root is the complete skills-only ChatGPT plugin package, following the Superpowers-style layout.

**Architecture:** Move the plugin manifest and skill from the nested `plugins/github-plugin-skill-builder/` package to the repository root, change the marketplace source to `./`, and update documentation to describe GitHub marketplace import as the distribution path. Keep V0 serverless: no MCP server or app configuration.

**Tech Stack:** GitHub repository, Claude-compatible plugin manifests, Markdown Agent Skills.

**Spec:** `docs/superpowers/specs/2026-09-03-github-hosted-skills-only-plugin-design.md`

## Global Constraints

- Ship as a **plugin containing skills**, never as a standalone ChatGPT Skill.
- Repository root is the plugin package.
- `.claude-plugin/marketplace.json` must use `"source": "./"`.
- Do not add `mcp.json`, `.mcp.json`, an MCP server URL, app template, OAuth backend, database, or runtime hosting.
- Preserve the exact V0 diagnostic prompt: `Run GitHub Plugin Skill Builder V0 test`.
- Repository URL remains `https://github.com/Zbrooklyn/Github-Plugin-Skill-Builder`.
- Repository remains public with default branch `main`.

---

### Task 1: Prove the current structure fails the target layout

**Files:**
- Expected but currently absent: `.claude-plugin/plugin.json`
- Expected but currently absent: `skills/creating-github-plugin-skills/SKILL.md`

**Interfaces:**
- Consumes: current repository default branch.
- Produces: fresh evidence that the target root paths do not yet exist.

- [x] **Step 1: Fetch `.claude-plugin/plugin.json` from `main`**

Expected: GitHub returns 404 before implementation.

- [x] **Step 2: Fetch `skills/creating-github-plugin-skills/SKILL.md` from `main`**

Expected: GitHub returns 404 before implementation.

---

### Task 2: Make the repository root the plugin package

**Files:**
- Create: `.claude-plugin/plugin.json`
- Modify: `.claude-plugin/marketplace.json`
- Create: `skills/creating-github-plugin-skills/SKILL.md`
- Delete: `plugins/github-plugin-skill-builder/.claude-plugin/plugin.json`
- Delete: `plugins/github-plugin-skill-builder/skills/creating-github-plugin-skills/SKILL.md`

**Interfaces:**
- Consumes: existing plugin metadata and skill content.
- Produces: a root package compatible with the approved Superpowers-style layout.

- [ ] **Step 1: Create root `.claude-plugin/plugin.json`**

Use:

```json
{
  "name": "github-plugin-skill-builder",
  "description": "GitHub-hosted skills-only plugin for creating, validating, and publishing reusable AI plugin skills.",
  "version": "0.1.0",
  "author": {
    "name": "Zbrooklyn"
  },
  "homepage": "https://github.com/Zbrooklyn/Github-Plugin-Skill-Builder",
  "repository": "https://github.com/Zbrooklyn/Github-Plugin-Skill-Builder",
  "license": "MIT",
  "keywords": [
    "skills",
    "plugins",
    "github",
    "chatgpt",
    "workflows"
  ]
}
```

- [ ] **Step 2: Update root marketplace manifest**

Use:

```json
{
  "name": "github-plugin-skill-builder",
  "description": "Development marketplace for the GitHub Plugin Skill Builder skills-only plugin.",
  "owner": {
    "name": "Zbrooklyn"
  },
  "plugins": [
    {
      "name": "github-plugin-skill-builder",
      "description": "GitHub-hosted skills-only plugin for creating, validating, and publishing reusable AI plugin skills.",
      "version": "0.1.0",
      "source": "./",
      "author": {
        "name": "Zbrooklyn"
      }
    }
  ]
}
```

- [ ] **Step 3: Create the root skill path**

Copy the existing skill content, but change its minimal structure example to:

```text
repo/
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
└── skills/
    └── skill-name/
        └── SKILL.md
```

Explain that the marketplace `source` is `./` when the repository root is the plugin package. Preserve the V0 diagnostic exactly.

- [ ] **Step 4: Read back all three root files**

Expected: all exist and contain the intended names, paths, and `source: "./"`.

- [ ] **Step 5: Delete the two old nested package files**

Expected: Git removes the now-empty nested directories automatically.

- [ ] **Step 6: Confirm both old nested paths return 404**

Expected: no duplicate plugin package remains.

---

### Task 3: Make installation and project intent unambiguous

**Files:**
- Modify: `README.md`
- Create: `INSTALL-CHATGPT.md`
- Modify: `ROADMAP.md`
- Modify: `PROJECT_MEMORY.md`

**Interfaces:**
- Consumes: root plugin architecture from Task 2.
- Produces: documentation that future sessions and users can follow without confusing marketplace import with MCP Server URL setup.

- [ ] **Step 1: Rewrite README structure and positioning**

README must state:

- this is a GitHub-hosted **skills-only plugin**;
- GitHub is the package host/source of truth;
- no runtime server is required;
- the repository root is the plugin package;
- the only distribution URL is `https://github.com/Zbrooklyn/Github-Plugin-Skill-Builder`;
- current ChatGPT installation requires a surface that exposes GitHub marketplace import.

- [ ] **Step 2: Add `INSTALL-CHATGPT.md`**

Document the supported path:

```text
Workspace settings → Plugins → Add → Import marketplace
Source: https://github.com/Zbrooklyn/Github-Plugin-Skill-Builder
Path: leave blank
Branch/tag/commit: leave blank to follow main
```

Also state that `Add plugin → Server URL` is the MCP-app creator and must not be given the GitHub repository URL.

- [ ] **Step 3: Update roadmap**

Mark the root-package refactor complete while leaving actual ChatGPT import/invocation/sync proof outstanding.

- [ ] **Step 4: Update project memory**

Record the serverless invariant: public GitHub repository is the plugin package host; no MCP server is part of V0; repo-only packaging cannot make an MCP Server URL field accept GitHub.

---

### Task 4: Verify the live GitHub repository

**Files:**
- Verify only; no planned new files.

**Interfaces:**
- Consumes: completed repository state.
- Produces: evidence required before claiming completion.

- [ ] **Step 1: Read the repository root tree**

Expected root includes `.claude-plugin`, `skills`, `README.md`, `INSTALL-CHATGPT.md`, `ROADMAP.md`, `PROJECT_MEMORY.md`, `LICENSE`, and `docs` and does not include the old `plugins` directory.

- [ ] **Step 2: Read `.claude-plugin/marketplace.json` and `.claude-plugin/plugin.json`**

Expected: valid JSON text, matching name/version, and marketplace `source` equals `./`.

- [ ] **Step 3: Read `skills/creating-github-plugin-skills/SKILL.md`**

Expected: valid `name` and `description` frontmatter; exact V0 diagnostic remains present.

- [ ] **Step 4: Inspect the recursive Git tree for MCP configuration**

Expected: no `mcp.json` or `.mcp.json` file.

- [ ] **Step 5: Read repository metadata**

Expected: visibility `public`, default branch `main`.

- [ ] **Step 6: Report the remaining external acceptance test**

The repository refactor is complete only if Steps 1–5 pass. V0 itself remains `in progress` until an eligible ChatGPT surface imports the GitHub repository, installs the plugin, invokes it in normal ChatGPT, and proves a later GitHub sync changes behavior.
