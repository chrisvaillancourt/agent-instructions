# Evidence and source register

Last reviewed: 2026-09-23. This is a research synthesis, not an endorsement by Matt Pocock. Linked material remains its authors' work; this repository contains original summaries rather than copied articles or transcripts.

Evidence labels: **article** = first-party text read; **transcript** = YouTube auto-captions inspected; **description** = video metadata/description only; **implementation** = installed code/docs inspected. Auto-captions can mis-transcribe names. A listing or search summary alone is not evidence of a video's recommendations.

## Matt Pocock: progression of the guidance

| Resource | Date / evidence | Finding and relevance |
| --- | --- | --- |
| [A Complete Guide to AGENTS.md](https://www.aihero.dev/a-complete-guide-to-agents-md) | Updated 2026-01-18; article | Minimal root: project sentence, non-default package manager, nonstandard commands, universally relevant guidance. Move specialized material behind links, nested scope, or skills. Warns about generated comprehensiveness and stale paths. |
| [Never Run Claude /init](https://www.aihero.dev/never-run-claude-init), [video](https://www.youtube.com/watch?v=9tmsq-Gvx6g) | 2026-02-24; article + video description, no available captions | Stricter bar: nearly empty global instructions; retain globally relevant, undiscoverable facts. Explore commands, architecture, and patterns from current source instead of storing duplicate summaries. |
| [How to actually force Claude Code to use the right CLI (don't use CLAUDE.md)](https://www.youtube.com/watch?v=3CSi8QAoN-s) | 2026-02-25; description, no available captions | Prefer deterministic hooks when a workflow restriction needs enforcement. This is not proof that every hook is correct or every requirement is mechanically enforceable. |
| [Claude Code tried to improve /init... Is it any better?](https://www.youtube.com/watch?v=llwTBpPqo9A) | 2026-03-23; transcript | Calls redesigned `/init` an improvement, but aggressively prunes its output. Removes hook-redundant typechecking and discoverable test patterns; moves a rare dependency exception into a narrow skill. Wants the agent to defend why guidance belongs in global context. |
| [Writing for Agents](https://www.aihero.dev/skills-writing-for-agents) | Updated 2026-08-24; article | Behavioral no-op testing, one source of truth, conditional context pointers, completion criteria, and pruning. New models usually warrant another no-op pass, not wholesale rewriting. |
| [My AGENTS.md file for building plans you actually read](https://www.aihero.dev/my-agents-md-file-for-building-plans-you-actually-read) | Article; date not asserted | Concise plans and unresolved questions are examples of useful personal preferences. Minimal project context is not a prohibition on persistent workflow preferences. |
| [How I use Claude Code for real engineering](https://www.youtube.com/watch?v=kZ-zzHVUrO4) | 2025-10-27; transcript | Earlier personal user-memory example includes cross-project workflow preferences. Distinguish personal preferences from generated repository overviews. |

The March video qualifies the literal February “never run” title. Our interpretation: do not accept generated global context uncritically; evaluate each instruction's value and placement. The January minimal template and February near-empty prescription differ in strictness. We adopt a behavioral test rather than hardcoding either template.

No specific relevant YouTube Shorts URL was verified. Do not relabel a full-length video as a Short. Rewiz mirrors were inaccessible (HTTP 526); they are not substantive sources. Video evidence was gathered during the initial investigation on the review date; future maintainers should re-fetch rather than rely on this summary as a transcript archive.

## Research behind the claims

[Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents?](https://arxiv.org/abs/2602.11988), Gloaguen et al., published 2026-02-12. The abstract reports no general success-rate improvement and an average inference-cost increase above 20% across its studied settings, while recognizing utility for nonstandard practices. We inspected the abstract, not a fresh reproduction of its experiments. Consult the full paper, version history, tasks, models, and agents before generalizing those results.

[HumanLayer: Writing a good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md) is an upstream source cited by Pocock's January article. It is a follow-up reading source, not independently evaluated evidence here.

Do not encode a numerical “instruction budget.” The January guide cites roughly 150–200 instructions; February's article claims roughly 300–400, with larger models potentially higher. Those figures are inconsistent and are not a portable model limit. Context occupancy, prompt caching, cost, attention, and compliance are distinct measurements.

## OMP baseline that motivated this skill

**Implementation evidence: OMP 18.2.9**, `packages/coding-agent/src/prompts/agents/init.md`, inspected 2026-09-23 ([upstream location](https://github.com/can1357/oh-my-pi/blob/main/packages/coding-agent/src/prompts/agents/init.md)).

The bundled `/init` asks parallel research agents to inspect source, tests, configuration/build, and scripts/docs, then write one root `AGENTS.md` titled “Repository Guidelines.” Requested sections: project overview; architecture/data flow; key directories; development commands; code conventions/patterns; important files; runtime/tooling; testing/QA. It requires concision and recommends omitting obvious structure, but also requires architecture/pattern coverage and recommends paths.

Our assessment: this is an orientation-guide generator, not instruction triage. The output is model-dependent, and custom commands can override the bundled fallback. We did not run it to generate a sample. The version observation is not a claim about future releases; upstream `main` links are mutable.

## Authoritative sources to monitor

- [Pocock's skills repository](https://github.com/mattpocock/skills): writing-for-agents changes and release history. Optional complementary skill; not a runtime dependency.
- [Pocock's setup topic](https://www.aihero.dev/topics/set-up-your-agent) and [YouTube channel](https://www.youtube.com/@mattpocock): newer qualifications, not just popular older headlines.
- [Agent Skills specification](https://agentskills.io/specification): portable package contract.
- [skills CLI](https://github.com/vercel-labs/skills): discovery, supported agent IDs, installation paths, update behavior.
- [OMP](https://github.com/can1357/oh-my-pi), [Claude Code skills](https://code.claude.com/docs/en/skills), [Claude Code memory](https://code.claude.com/docs/en/memory), [Codex skills](https://developers.openai.com/codex/skills), [OpenCode skills](https://opencode.ai/docs/skills): harness-specific contracts. Linked destinations not otherwise marked above are monitoring resources, not claims of complete validation.

For each future source update, record the URL, observed date, publication/update date if verified, version or commit if available, evidence type, exact affected claim, uncertainty, and whether it changes our policy. Follow [maintenance](maintenance.md); do not silently rewrite history when advice changes.
