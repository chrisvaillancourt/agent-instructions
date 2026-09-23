# Principles and design decisions

These are this project's decisions, informed by the [source register](sources.md), not rules attributed wholesale to Matt Pocock. The executable workflow lives in [SKILL.md](../skills/agent-instructions/SKILL.md); this document explains its rationale.

## Behavior is the objective

Success means the agent preserves required behavior while avoiding irrelevant context. A short file, low token count, or tidy directory tree is not sufficient. A useful instruction may be lengthy; an essential safety constraint may be rarely exercised. Test the effect of removal instead of deleting to a size target.

A new model can make a previous instruction redundant or expose a new failure. That is a reason to compare behavior, not automatically rewrite all instructions or assume every model has the same limits.

## Keep sources of truth authoritative

Configuration, current code, and executable checks are better homes for discoverable facts than prose caches. Documentation still earns its place for non-obvious decisions, domain constraints, operational hazards, or expensive discovery. “Discoverable” is contextual: a fact technically present somewhere can still be unreliable to find before a consequential action.

Root context is scarce shared attention. Scope guidance to where it matters, and keep specialized procedures behind specific pointers. A pointer must say when to read its target; splitting files without a reliable trigger merely hides requirements. Account for the harness's actual import and precedence behavior.

## Preserve constraints during migration

Instruction pruning is not a license to weaken requirements. Conflicting policies need a precedence decision or a human answer. A proposed enforcement mechanism does not replace an existing instruction until the mechanism is implemented and verified. Hooks can enforce some behavior, but require correct event coverage, failure handling, and permissions; this skill recommends them rather than installing them implicitly.

## Separate selection from writing

`agent-instructions` selects what belongs where and governs changes. `writing-for-agents` is a complementary writing reference, not a required dependency. The installed package must remain usable without another skill or this repository's maintainer docs.

The keep/disclose/enforce/delete classification, proposal-first boundary, and verification protocol are our synthesis. They are not presented as an official Pocock workflow.

## Explicit invocation, narrow authority

This is an occasional maintenance workflow. It should not run merely because an agent is changing code. A user-invoked skill gives it a portable package and a deliberate entry point; a second custom command would initially duplicate infrastructure. We do not replace `/init` automatically.

Invocation controls differ by harness and are not security boundaries. The body also requires an explicit request and defaults to a proposal. Approval to edit a repository's instructions does not grant access to secrets, permission changes, installation, commits, or publication.

## Minimize maintenance, not useful judgment

One skill, one bundled harness reference, no runtime dependencies, no mandatory model/provider, no fixed line cap, and no automatic migration script. The root maintainer docs are not shipped as runtime dependencies. Add a new file or abstraction only for a demonstrated branch or maintenance need.

Run realistic cases after changes. Retain uncertainty when observations do not establish a claim. Use [maintenance](maintenance.md) to distinguish editorial changes, policy changes, and changes driven by model or harness behavior.
