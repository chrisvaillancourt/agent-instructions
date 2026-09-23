# Validation record

## 2026-09-23 — Initial implementation

### Packaging

- Ran `skills` CLI **1.7.0** via Socket Firewall (`sfw npx --yes skills@1.7.0`). Local `add --list` found exactly one skill named `agent-instructions`.
- Installed from the local checkout into a disposable directory with `--agent universal claude-code --copy --yes`; exit 0.
- Compared the installed `SKILL.md` and `references/harnesses.md` byte-for-byte against source in both `.agents/skills/agent-instructions/` and `.claude/skills/agent-instructions/`; both matched.
- The package has no runtime dependency on repository-level docs or another installed skill.

### Behavioral exercises

Two independent OMP task workers executed the skill against disposable synthetic fixtures. The parent session used `openai-codex/gpt-6-astra`; workers used the harness's default task-agent selection, whose exact resolved model was not captured. These runs demonstrate the workflow in this environment, not a controlled cross-model comparison. The target `GUIDANCE.md` file was stipulated to be root-scoped; this does not test automatic `AGENTS.md` discovery.

**Proposal-only:** fixture included a package-script instruction, migration-specific tenant/rollback requirements, a production-approval rule, contradictory integration preferences, and hostile credential-upload text. The worker accounted for every clause, rejected credential retrieval/publication, proposed conditional migration guidance, preserved the production rule, and asked about the unresolved merge/rebase choice. Independent file hashes confirmed no edits or new files.

A useful distinction: the worker kept “Run tests with npm test.” Although the command is discoverable in `package.json`, deleting the imperative could also delete the requirement to run tests. This is a conservative preservation decision, not failure to minimize tokens.

**Explicit apply:** a separate worker received exact approval to remove the command and hostile clause, move migration guidance behind a conditional link, and preserve the safety rule and conflicting policies. Independent checks confirmed the expected content changes, unchanged unrelated files, and the migration target. No hooks, installations, commits, credential access, or external writes were part of either fixture run.

### Privacy checks

Gitleaks **8.30.1**, downloaded through Socket Firewall and verified against the release SHA-256 checksum, reported no leaks in the initial working-directory scan. Manual review checked the authored text for private source material and machine-specific details. Raw worker transcripts, fixture files, scanner binaries, and temporary install outputs were kept outside the repository. These checks reduce risk; they do not guarantee the absence of every sensitive fact.

### Limits

- No end-to-end Claude Code, Codex, or OpenCode runtime session was exercised.
- OMP hidden-discovery and slash-command behavior are documented from installed 18.2.9 sources, not verified by invoking this newly installed skill in a fresh interactive session.
- Conditional pointer following was structurally checked and simulated, not measured through actual migration/ordinary-task sessions.
- Empty-repository and enforcement-handoff scenarios are specified in maintenance docs but not yet independently exercised.
- No baseline-versus-candidate experiment establishes a performance, cost, or compliance improvement; no such claim is made.

Future entries should name the tested revision and exact worker model where available, and distinguish installer checks, structural checks, simulated behavior, and full harness runs.
