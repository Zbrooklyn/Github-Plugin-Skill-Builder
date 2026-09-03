# Install in ChatGPT

This repository is packaged as a **GitHub-hosted skills-only plugin**. It does not run an MCP server and does not have a Server URL.

## Supported GitHub marketplace import path

On a ChatGPT workspace that exposes GitHub marketplace import:

1. Open **Workspace settings → Plugins**.
2. Select **Add → Import marketplace**.
3. In **Source**, paste:

```text
https://github.com/Zbrooklyn/Github-Plugin-Skill-Builder
```

4. Leave **Path** blank.
5. Leave **Branch/tag/commit** blank to follow the repository's default `main` branch. Pin a tag or commit only when fixed behavior is desired.
6. Select **Import marketplace** and authorize GitHub if prompted.
7. Review the import result.
8. Open **GitHub Plugin Skill Builder** and set its installation policy so the plugin is installed/available for the intended role.

The repository root contains both supported Claude-compatible manifests:

```text
.claude-plugin/marketplace.json
.claude-plugin/plugin.json
```

The marketplace points to the repository root with:

```json
"source": "./"
```

No subdirectory path is required.

## Do not use the MCP Server URL form

If **Add plugin** opens a form containing fields such as:

```text
Server URL
Authentication
OAuth Client ID
OAuth Client Secret
Custom Headers
```

that is the custom MCP/app creation flow. It expects a live MCP protocol endpoint.

Do **not** paste this repository URL into Server URL:

```text
https://github.com/Zbrooklyn/Github-Plugin-Skill-Builder
```

A public GitHub repository can host the plugin package and skill content, but it is not itself an MCP network endpoint.

If your ChatGPT account exposes only the Server URL form and not **Import marketplace**, the current account/workspace does not provide the GitHub-import path required by this serverless package. That is a distribution-surface limitation, not a repository-format failure.

## V0 invocation test

After the plugin is installed, open a normal ChatGPT conversation with the plugin enabled/selected and send exactly:

```text
Run GitHub Plugin Skill Builder V0 test
```

Success requires the answer to begin exactly:

```text
GitHub Plugin Skill Builder V0 — skill active
```

That string lives inside the GitHub-hosted `SKILL.md`, making the test distinguishable from generic model behavior.

## V0 sync test

After the first invocation succeeds:

1. Change the diagnostic marker in `skills/creating-github-plugin-skills/SKILL.md` from `V0` to a clearly different temporary marker, such as `V0-SYNC-2`.
2. Commit the change to the branch used by the imported marketplace.
3. In ChatGPT, open **Workspace settings → Plugins → Marketplaces**.
4. Open this marketplace and select **Sync now**.
5. Invoke the diagnostic again.
6. Confirm ChatGPT returns the new marker.
7. Restore the canonical V0 marker unless the version change is intentionally retained.

This proves the complete path:

```text
GitHub change → marketplace sync → changed plugin skill behavior in ChatGPT
```

## V0 acceptance

V0 is complete only when all of the following are true:

- the GitHub repository imports as a plugin package;
- the resulting **plugin**, not merely a standalone Skill, is installed;
- it can be used from a normal ChatGPT conversation on the supported surface;
- the deterministic diagnostic is observed;
- a GitHub edit followed by marketplace sync changes the observed behavior;
- no MCP server is required for any of those steps.
