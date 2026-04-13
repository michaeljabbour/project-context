# Setup Prompt

Copy and paste this prompt into your AI coding session to generate customized project coordination files from the templates.

---

## Full Setup

```
Read project-context/README.md first to understand the coordination file
system — its tiers, cognitive modes, and maintenance expectations. Then read
all the templates in project-context/templates/. Scan the codebase to
understand the project — its structure, language, dependencies, and current
state. Look for any existing files that already serve coordination functions
(READMEs, CONTRIBUTING guides, decision logs, changelogs, onboarding docs,
architecture docs, glossaries, etc.) and consolidate their relevant content
into the new format rather than starting from scratch. Generate customized
versions of each coordination file at the project root — do not modify
anything inside project-context/templates/ (those are the versioned source of
truth). Start with PROJECT_CONTEXT.md and GLOSSARY.md (Tier 1), then
STRUCTURE.md, WAYSOFWORKING.md, and HANDOFF.md (Tier 2). Ask me before
generating Tier 3 files (PROVENANCE.md, EXPERIMENT_JOURNAL.md) or the
optional CLAIMS_TRACKER.md.
```

---

## Quick Setup (Tier 1 Only)

For a minimal start:

```
Read project-context/README.md to understand the coordination file system.
Then read project-context/templates/PROJECT_CONTEXT.md and
project-context/templates/GLOSSARY.md. Scan the codebase and any existing
coordination files (READMEs, glossaries, onboarding docs) and generate
customized versions of both at the project root. Do not modify anything
inside project-context/templates/.
```

Then add Tier 2 files when you're ready:

```
Read project-context/templates/STRUCTURE.md, project-context/templates/WAYSOFWORKING.md,
and project-context/templates/HANDOFF.md. Scan the codebase and any existing docs
(CONTRIBUTING guides, architecture docs, decision logs) and generate customized versions
at the project root, consolidating relevant existing content into the new format.
```

---

## Session Start Prompt

Use this at the beginning of every session after setup is complete:

```
Read PROJECT_CONTEXT.md and GLOSSARY.md before starting any work.
Check HANDOFF.md for what happened last session and what to do next.
```

---

## Session End Prompt

Use this before ending any session:

```
Update HANDOFF.md with what we accomplished this session, what's blocked,
and what the next session should start with. Be specific.
```
