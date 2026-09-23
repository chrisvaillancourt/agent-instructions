# agent-instructions

A proposal-first skill for maintaining repository agent instructions: **keep, disclose, enforce, or delete**. Informed by Matt Pocock's guidance; independently maintained, not affiliated with or endorsed by him.

Use it to audit existing `AGENTS.md` / `CLAUDE.md` guidance or decide whether a new repository needs any. It preserves useful constraints rather than generating an architecture dump or optimizing for a line count.

## Install

Requires Node.js and pnpm or npm for the `skills` CLI. Examples use pnpm by default, with npm/npx alternatives below. The skill itself has no executable dependencies. Review the [skill](skills/agent-instructions/SKILL.md) before installing; skills run with the permissions of their host agent.

```sh
# Inspect available skills without installing.
pnpm dlx skills@latest add chrisvaillancourt/agent-instructions --list

# Interactive installation: choose your harnesses and scope.
pnpm dlx skills@latest add chrisvaillancourt/agent-instructions --skill agent-instructions

# Project installation for OMP's .agents discovery and Claude Code.
pnpm dlx skills@latest add chrisvaillancourt/agent-instructions --skill agent-instructions --agent universal claude-code

# User-wide installation for OMP and Claude Code.
pnpm dlx skills@latest add chrisvaillancourt/agent-instructions --skill agent-instructions --global --agent universal claude-code
```

For npm users, replace `pnpm dlx` with `npx`; the remaining arguments are identical:

```sh
npx skills@latest add chrisvaillancourt/agent-instructions --skill agent-instructions
```

If you use Socket Firewall, prefix package execution with `sfw`, for example `sfw pnpm dlx skills@latest add ...` or `sfw npx skills@latest add ...`. Use your normal dependency approval policy. `@latest` is convenient but mutable; the tested version is recorded in [validation](docs/validation.md).

### OMP user-wide installation

The checked CLI has no dedicated `omp` agent target; `pi` means Pi, not OMP. Project-scoped `--agent universal` writes `.agents/skills/`, which OMP discovers.

For user-wide OMP and Claude Code access, use the global command above. If you already have the `skills` CLI installed, you can use `skills` in place of `pnpm dlx skills@latest`. The skill has been reported available in OMP after this installation without adding `skills.customDirectories`; no extra configuration is required when OMP already discovers it.

Only if OMP does not discover the installed skill, inspect the CLI's reported destination and OMP's active skill search locations. If the installed container is outside those locations, add it to `skills.customDirectories`, preserving existing entries, or link only this skill into your active OMP agent directory's `skills/` folder. Do not assume the universal global destination is `~/.agents/skills`: CLI versions can use `~/.config/agents/skills`. Do not overwrite an existing skill or change configuration blindly. See [harness notes](skills/agent-instructions/references/harnesses.md).

No global harness settings or installations are changed by cloning this repository.

## Use

OMP, with skill commands enabled:

```text
/skill:agent-instructions Audit this repository. Propose changes only.
```

Claude Code:

```text
/agent-instructions Audit this repository. Propose changes only.
```

After reviewing the proposal:

```text
Apply the proposed repository instruction-file changes. Leave the unresolved policy choices unchanged.
```

Invoking the skill defaults to **read-only proposal mode**. Explicit authorization is required for edits; commit/push, installations, hooks, permission changes, and publication are separate actions. On harnesses that ignore `disable-model-invocation`, automatic invocation is not mechanically prevented. Verify your harness's controls or load the file manually outside automatic discovery.

The skill is self-contained. An installed `writing-for-agents` skill can provide additional writing guidance, but is optional. No `/init` override is installed.

## Maintain and update

- [Principles](docs/principles.md): design decisions and tradeoffs.
- [Sources](docs/sources.md): articles, videos, research, evidence limits, and upstream monitoring links.
- [Maintenance](docs/maintenance.md): model/harness refresh procedure, behavioral scenarios, review, and publication checks.
- [Validation](docs/validation.md): what has actually been exercised, with limitations.

Update installed skills through your CLI's supported update workflow (`pnpm dlx skills@latest update`, or `npx skills@latest update` for npm users; consult its help for scope and selection), then verify the active harness loads the new version. A repository update does not prove that existing sessions have refreshed their context.

## License

[MIT](LICENSE) for this repository's original content. External articles, videos, and linked documentation retain their own licenses.
