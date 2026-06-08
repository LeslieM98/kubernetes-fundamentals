# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

A set of hands-on Kubernetes training labs delivered through GitHub Codespaces. It is *not* an application — every lab is a self-contained directory of manifests that students apply against a local `kind` cluster.

## Environment

- Labs run inside the devcontainer image `quay.io/kubermatic-labs/training-ghcs-kubernetes-fundamentals-trainee-environment` (pinned in `.devcontainer/devcontainer.json`). The image's `postCreateCommand` runs `/setup_kind_cluster.sh` to provision a `my-cluster` kind cluster (1 control plane + 3 workers) plus `cloud-provider-kind` for `LoadBalancer` services.
- All lab READMEs assume the Codespaces mount path: `cd /workspaces/kubernetes-fundamentals/<lab>`. Don't rewrite these to relative paths.
- `make verify` runs `pre-checks.sh`, which checks the four expected docker containers are up and the cluster is reachable. Use this to confirm environment health before debugging a lab.

## Lab structure (important for any edit)

Each top-level numbered directory is one lab. Numbering groups topics: `01–18` core concepts, `20–23` scheduling, `30–34` network/auth/observability.

A lab typically contains:
- `README.md` — step-by-step student instructions (prose + bash code blocks).
- One or more `*.yaml` manifests — **many are intentionally broken**. The README tells the student to find and fix the bugs (look for phrases like "there are errors in the yaml files", "Find and fix the two issues", "There is an issue with this structure").
- `.solution/` — the corrected version of the broken YAML. **Always diff a broken file against its `.solution/` counterpart before deciding something is a real bug.** If it differs only on the intentional bug(s), leave it alone.

Labs with intentional bugs as of this writing: `03_commands-and-args`, `05_replicasets`, `09_configmaps`, `10_secrets`, `11_persistence-static`, `13_persistence-use-volume`.

## Hard rules

- **Off-limits directories**: `.99_todos/` (instructor drafts/notes) and `.secrets/` (credentials). Do not read, open, grep, or list these.
- **Do not bump pinned versions**: image tags like `nginx:1.19.2`, `busybox:1.32.0`, `curlimages/curl:7.72.0`, the ingress-nginx chart version `4.11.0`, the devcontainer image version, etc. These are pinned so trainings reproduce identically across sessions.
- **Do not "fix" intentional bugs** — see Lab structure above.
- **Do not change `LetsEncrypt` spelling** in lab READMEs (user has previously rejected the brand-correct edit).

## Conventions in lab READMEs

- Bash code blocks that span multiple terminals use `# [TERMINAL-2]` as a comment marker before commands meant for a second pane. Missing `#` makes the line execute as a command and error.
- `kubectl create -f` is preferred over `apply` for first creation; re-creation typically uses `kubectl replace -f X.yaml --force`. Calling `create` twice on the same manifest will fail with AlreadyExists.
- File paths in `cd` commands always use `/workspaces/kubernetes-fundamentals/<lab>/`.

## Linting

Two project skills live in `.claude/skills/`:

- `md-linter` — checks README prose for typos/grammar.
- `code-linter` — checks code blocks and YAML files for real bugs (compares against `.solution/` to ignore intentional ones).

Both follow the same scoping rule: if the working tree has unstaged changes, they restrict to the changed files; if a numeric prefix is passed (e.g. `12`), they resolve it to the matching `12_*` directory; otherwise they scan every top-level lab README. Both skip `.99_todos/` and `.secrets/`.
