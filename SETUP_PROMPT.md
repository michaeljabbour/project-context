# Setup Prompt

Copy and paste this prompt into your AI coding session to generate customized project coordination files from the templates.

---

## Full Setup (All Tiers)

```
Read the templates in project-context/templates/ and set up project coordination
files for this project.

For each template:
1. Read the template to understand its structure and purpose.
2. Analyze the codebase to gather relevant information.
3. Generate a customized version at the project root with placeholders filled in.

Work through the tiers in order:

Tier 1 (generate first):
- PROJECT_CONTEXT.md -- Fill in project name, phase, version, team, and milestone.
- GLOSSARY.md -- Identify key domain terms from the codebase and document them.

Tier 2 (generate next):
- STRUCTURE.md -- Map the actual directory layout and document naming conventions.
- WAYSOFWORKING.md -- Document build/test/deploy workflows and any known failure patterns.
- HANDOFF.md -- Initialize with current project state as the first handoff entry.

Tier 3 (ask me before generating):
- PROVENANCE.md -- Document key architectural decisions visible in the codebase.
- EXPERIMENT_JOURNAL.md -- Initialize empty, ready for first experiment entry.

Extension (skip unless I ask):
- CLAIMS_TRACKER.md -- Only for projects with patent/IP tracking needs.

After generating each file, show me a brief summary of what you filled in so I can
correct anything before moving to the next tier.
```

---

## Quick Setup (Tier 1 Only)

For a minimal start, use this shorter prompt:

```
Read project-context/templates/PROJECT_CONTEXT.md and project-context/templates/GLOSSARY.md.
Analyze the codebase and generate customized versions of both files at the project root.
Fill in all placeholders based on what you find.
```

Then add Tier 2 files when you're ready:

```
Read project-context/templates/STRUCTURE.md, project-context/templates/WAYSOFWORKING.md,
and project-context/templates/HANDOFF.md. Generate customized versions at the project root.
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
