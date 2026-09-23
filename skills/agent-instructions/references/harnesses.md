# Harness-dependent behavior

Checked 2026-09-23. These are compatibility notes, not universal loading rules. Recheck the active version before relying on them. Installation transfers files; it does not prove a harness loaded or obeyed them.

## OMP

Inspected OMP 18.2.9 documentation and bundled source:

- `/skill:agent-instructions` explicitly invokes this skill when `skills.enableSkillCommands` is enabled.
- `disable-model-invocation: true` is normalized to hidden model discovery. It does not make the file inaccessible: explicit invocation and `skill://agent-instructions` remain available. This is not an access-control boundary.
- `.agents/skills/<name>/SKILL.md` is discovered at project scope. Native user skills live in `~/.omp/agent/skills/`; named profiles can use a different agent directory.
- Standalone ancestor `AGENTS.md` files can accumulate across depths, but same-depth context files are subject to provider precedence. Native `.omp/AGENTS.md` discovery uses the nearest non-empty `.omp` directory; it is not a universal additive hierarchy.
- `@path` in context files expands inline. Use ordinary Markdown links with conditions for on-demand reading.
- Native `RULES.md` is sticky content, not a place to hide long guidance. User/project rules with the same name can shadow each other.

Sources: [skills documentation](https://github.com/can1357/oh-my-pi/blob/main/docs/skills.md), [context files](https://github.com/can1357/oh-my-pi/blob/main/docs/context-files.md), [slash commands](https://github.com/can1357/oh-my-pi/blob/main/docs/slash-command-internals.md). These links track upstream; the observations above are version-specific. In OMP, the installed equivalents are available through `omp://`.

## Claude Code

[Official skills documentation](https://code.claude.com/docs/en/skills) documents `/agent-instructions` and `disable-model-invocation: true` for explicit-only invocation. Skills and legacy custom commands share a command surface. This repository uses a skill, without duplicating it as a command.

Check [memory documentation](https://code.claude.com/docs/en/memory) before changing `CLAUDE.md` imports or nested guidance. Do not assume the OMP `AGENTS.md` loading rules apply.

## Other harnesses

The [Agent Skills specification](https://agentskills.io/specification) defines the package format, not universal invocation control. `disable-model-invocation` is a harness extension. A harness may ignore it; the skill body still requires an explicit user request, but prose is not mechanical enforcement.

Check official documentation for discovery directories, invocation syntax, instruction precedence, and disabling automatic invocation. If explicit-only invocation cannot be enforced and is required, keep the skill outside automatic discovery and load its file manually when requested. Do not claim runtime compatibility merely because `skills add` succeeds.
