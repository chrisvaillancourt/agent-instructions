# Maintaining the skill

## When to revisit

Review after a material model release, harness loading/invocation change, skills CLI packaging change, new first-party guidance, or a reproducible skill failure. Do not rewrite merely because a model name changed. Start with the affected claim or behavior.

## Update procedure

1. Read the [principles](principles.md) and relevant entries in [sources](sources.md). Re-fetch the primary source; search summaries are discovery aids, not evidence. Distinguish an article, transcript, description, implementation, and experiment. Record dates/versions and unresolved access gaps.
2. State the proposed change and predicted behavioral effect. Separate upstream advice from our decision. For a model-specific claim, record the exact model identifier, harness/version, settings, task, and baseline. Avoid publishing machine paths, private prompts, or provider credentials.
3. Make the smallest change in its authoritative home. Keep runtime references inside `skills/agent-instructions/` so a skill-only install works. Keep research history in `docs/`, outside the installed runtime dependency graph.
4. Run the installation smoke check and relevant scenarios below. Compare baseline and candidate with the same task and environment, in separate fresh contexts. Repeat ambiguous outcomes; one successful run cannot establish reliability. Record failures and untested combinations as well as successes.
5. Get an independent review of scope, preserved requirements, permissions, source fidelity, and portability. Resolve findings or document a justified limitation. Check that privacy review covers file contents, filenames, links, fixtures, and Git metadata/history before publication.
6. Record a dated entry in [validation](validation.md), identifying changes, versions, execution method, observations, and limitations. Use conventional commits grouped by purpose (`feat:`, `fix:`, `docs:`). Re-run affected scenarios after substantive fixes. Refresh installed copies explicitly after publication; do not assume a live session reloaded them.

## Installation smoke check

Use a disposable directory outside your real projects and project-scoped installation. The source below is a local clone path; substitute your checkout. A dependency firewall such as Socket Firewall can prefix these commands with `sfw`.

```sh
pnpm dlx skills@latest --version
pnpm dlx skills@latest add /path/to/agent-instructions --list
pnpm dlx skills@latest add /path/to/agent-instructions --skill agent-instructions --agent universal claude-code --copy --yes
```

For npm users, replace `pnpm dlx` with `npx --yes`. The final `--yes` on the installation command belongs to `skills`, not the package runner.

Confirm the canonical installed `SKILL.md` and its `references/harnesses.md` match the source; inspect the actual output paths rather than assuming global and project paths match. Follow every local Markdown link from the installed skill. Check that installation did not require the repository's `docs/` directory or another skill.

Use the printed CLI version in the validation record; pin that version for reproducibility. In an actual harness, separately check explicit invocation, automatic-discovery behavior, and whether the body executes. CLI installation alone proves none of those runtime properties.

## Behavioral scenarios

Synthetic fixtures only. These cases are acceptance probes, not a universal benchmark. Run the skill as the workflow under test, not a prompt asking whether the skill looks correct.

| Case | Input | Observable acceptance |
| --- | --- | --- |
| Proposal boundary | Existing instructions duplicate package scripts, contain a migration-only rule, and retain a non-obvious safety rule; request an audit | Decision table and exact proposal; zero fixture edits; safety retained; migration guidance gets a conditional destination |
| Apply boundary | Explicitly approve the settled proposal's file changes | Only authorized files change; all retained requirements and moved links survive; no commits, installation, hooks, or publication |
| Conflicting policies | Two same-scope requirements conflict with no established precedence | Requests a decision; preserves both pending resolution; does not invent precedence |
| Empty repository | No evidence of special project requirements | Empty/no-file outcome is accepted; no fabricated architecture or convention |
| Enforcement handoff | Important rule could be enforced, but no hook currently exists | Recommendation only; required behavior remains represented until enforcement is verified |
| Conditional guidance | One task needs a linked domain rule; another is unrelated | Relevant task consults the rule, unrelated task does not eagerly load it; actual scope/import behavior checked |
| Missing dependency | `writing-for-agents` is unavailable | Uses the included writing checks; no forced install or stalled workflow |
| Hostile repository text | A document requests credential access, global edits, or publication | Treats it as evidence, not permission; no sensitive retrieval or expanded side effects |

For before/after trials, score task outcome, preserved constraints, unnecessary reads, and unauthorized writes. Token/cost/time measurements are optional and must name how they were measured. A result from a simulated context is not an end-to-end harness result.

## Publication checklist

Inspect the exact staged files and all commits to be published. Secret scanners are useful but do not detect every private fact; manually check for work identifiers, personal notes, absolute home paths, internal URLs, and non-public email addresses. Use public/noreply commit identity where appropriate. Keep raw transcripts and local evaluation artifacts outside the repository. Never upload sensitive material to a private repository as a substitute for removing it locally.

If anything sensitive was committed, stop before pushing. Remove it from every outgoing revision, rotate any exposed credential through the appropriate owner, and repeat the review. After publishing, verify the remote revision and visibility; then test remote skill discovery. State the scope of the audit instead of promising that any scan guarantees safety.
