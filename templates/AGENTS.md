---
type: agent-instructions
tier: 0
priority: automatic
updated: 2026-04-13
tokens_estimate: 600
---

<!-- AGENT DIRECTIVES
- This file is the entry point for ALL AI agents working on this project.
- Read this file automatically at the start of every session.
- Follow the Session Protocol below — it is not optional.
- The Continuous Improvement Contract below defines your obligations
  for maintaining project documentation as you work.
-->

# Agent Instructions

This project uses a coordination file system in `project-context/` that gives you persistent memory across sessions. **Read the coordination files before starting any work.**

---

## Session Protocol

### Starting a Session

Read these files in order before doing anything else:

1. `project-context/PROJECT_CONTEXT.md` — current project state, phase, team, active decisions
2. `project-context/GLOSSARY.md` — terminology contract (use these terms exactly, not synonyms)
3. `project-context/HANDOFF.md` — what happened last session, what to do next

If your task involves writing or moving files, also read:

4. `project-context/STRUCTURE.md` — directory layout, naming conventions, routing table

If your task involves understanding past decisions or experiments, also read:

5. `project-context/PROVENANCE.md` — why decisions were made, what was considered
6. `project-context/EXPERIMENT_JOURNAL.md` — what was tried, what worked, what didn't

### Ending a Session

Before signing off, update `project-context/HANDOFF.md` with:
- What you accomplished (specific files changed, decisions made)
- What's blocked or unresolved
- What the next session should start with
- Any non-obvious context the next agent needs

---

## Continuous Improvement Contract

As you work, you are responsible for keeping the coordination files accurate and growing. This is not extra work — it is part of the work.

### When to Update What

| You just... | Update this file | How |
|-------------|-----------------|-----|
| Used a term that isn't in the glossary | `project-context/GLOSSARY.md` | Add the term with "Means" and "Does NOT Mean" columns |
| Made a design or architectural decision | `project-context/PROVENANCE.md` | Add a decision record: context, alternatives, rationale |
| Hit an error and figured out the fix | `project-context/WAYSOFWORKING.md` | Add a named failure pattern: symptom, root cause, fix |
| Discovered a better workflow | `project-context/WAYSOFWORKING.md` | Add or update a proven workflow with the new sequence |
| Created or moved files | `project-context/STRUCTURE.md` | Update the layout tree and "What Goes Where" table |
| Ran an experiment or benchmark | `project-context/EXPERIMENT_JOURNAL.md` | Add an entry: hypothesis first, then results |
| Changed the project's phase or milestone | `project-context/PROJECT_CONTEXT.md` | Update current state section |
| Finished any session | `project-context/HANDOFF.md` | Write a new entry (see Ending a Session above) |

### The Rule

**If you learned something that would save the next session time, write it down in the appropriate coordination file.** The 30 seconds it takes to add an entry saves 10 minutes of rediscovery.

### What NOT to Do

- Do not modify files inside `project-context/templates/` — those are the versioned source of truth
- Do not create new coordination files outside `project-context/` — add to existing files instead
- Do not skip updates because "it's a small change" — small changes compound
- Do not add speculative entries — only document what actually happened or was actually decided

---

## File Reference

| File | Path | Purpose |
|------|------|---------|
| PROJECT_CONTEXT.md | `project-context/PROJECT_CONTEXT.md` | Current state, phase, team, milestone |
| GLOSSARY.md | `project-context/GLOSSARY.md` | Terminology with anti-definitions |
| STRUCTURE.md | `project-context/STRUCTURE.md` | Directory layout, naming, file routing |
| WAYSOFWORKING.md | `project-context/WAYSOFWORKING.md` | Workflows, failure patterns, verification |
| HANDOFF.md | `project-context/HANDOFF.md` | Session continuity (rewritten each session) |
| PROVENANCE.md | `project-context/PROVENANCE.md` | Decision records with alternatives and rationale |
| EXPERIMENT_JOURNAL.md | `project-context/EXPERIMENT_JOURNAL.md` | Timestamped experiment log |
| CLAIMS_TRACKER.md | `project-context/CLAIMS_TRACKER.md` | Patent/IP tracking (optional) |

---

## For Other Agent Platforms

This file follows the `AGENTS.md` convention. If your platform uses a different file:

- **Claude Code**: Copy or symlink this to `CLAUDE.md`
- **Cursor**: Copy the Session Protocol section to `.cursorrules`
- **GitHub Copilot**: Copy to `.github/copilot-instructions.md`

The content is platform-agnostic — only the filename changes.
