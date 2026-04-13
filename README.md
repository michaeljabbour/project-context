# Project Coordination Templates

A set of markdown files that give AI agents persistent project memory across sessions.

These templates provide structured context that agents read at the start of each session, eliminating the recurring cost of re-explaining your project, its terminology, its decisions, and its current state. They work with any AI coding assistant but are optimized for multi-session workflows where continuity matters.

---

## Why It Works

These files are not organized by topic. They are organized by **cognitive mode** -- each file maps to a different kind of thinking an agent needs to do. This is why the system works better than a single large README: agents load only the thinking mode they need for the current task.

### Cognitive-mode partitioning

The eight files correspond to distinct reasoning patterns:

- **Orientation** (PROJECT_CONTEXT.md) -- Where am I? What phase is this project in?
- **Semantic grounding** (GLOSSARY.md) -- What do these terms mean, precisely?
- **Spatial reasoning** (STRUCTURE.md) -- Where do things go in this codebase?
- **Procedural reasoning** (WAYSOFWORKING.md) -- How should I work here?
- **Session continuity** (HANDOFF.md) -- What just happened? What's next?
- **Causal reasoning** (PROVENANCE.md) -- Why were these decisions made?
- **Scientific reasoning** (EXPERIMENT_JOURNAL.md) -- What was tried? What was learned?
- **Strategic reasoning** (CLAIMS_TRACKER.md) -- What legal/IP constraints apply?

### The terminology table as semantic contract

The GLOSSARY.md file acts as a type system for natural language. Its "Does NOT Mean" column is the critical feature -- it prevents agents from silently substituting synonyms that blur important distinctions. When an agent reads that "module" means X and does not mean Y, it constrains interpretation the same way a type signature constrains code.

### Named failure patterns as institutional memory

WAYSOFWORKING.md captures named failure patterns (anti-patterns, known gotchas, things that look right but break). These create institutional memory that persists across sessions. An agent that reads "never do X because it causes Y" in session 12 benefits from the pain of session 3 without repeating it.

### Session loop as state machine

The session workflow defined in WAYSOFWORKING.md acts as a state machine: read context, check handoff, do work, update files, write handoff. This loop prevents drift by making each session accountable to both the previous and next session.

### Hypothesis-before-results discipline

EXPERIMENT_JOURNAL.md requires writing the hypothesis before recording results. This prevents confabulation -- the common failure mode where agents retroactively construct explanations that fit observed outcomes rather than testing genuine predictions.

### Feedback loops

The files form a closed loop: experiments produce findings, findings inform decisions (PROVENANCE), decisions shape procedures (WAYSOFWORKING), and procedures guide better experiments. Knowledge compounds across sessions instead of evaporating.

---

## File Reference

| File | Tier | Cognitive Mode | When to Read | When to Update |
|------|------|---------------|--------------|----------------|
| PROJECT_CONTEXT.md | 1 - Always | Orientation | Every session start | Every session |
| GLOSSARY.md | 1 - Always | Semantic grounding | Every session start | When new terms emerge |
| STRUCTURE.md | 2 - Working | Spatial reasoning | When writing or moving code | When directory layout changes |
| WAYSOFWORKING.md | 2 - Working | Procedural reasoning | When starting implementation | When patterns break or improve |
| HANDOFF.md | 2 - Working | Session continuity | Every session start | Every session end |
| PROVENANCE.md | 3 - Investigating | Causal reasoning | When questioning a decision | When decisions are made |
| EXPERIMENT_JOURNAL.md | 3 - Investigating | Scientific reasoning | When designing experiments | After every experiment run |
| CLAIMS_TRACKER.md | Extension | Strategic reasoning | When IP questions arise | When claims evolve |

### Tier explanation

- **Tier 1 (Always Read, <1000 tokens combined):** PROJECT_CONTEXT.md and GLOSSARY.md. These are cheap to load and orient the agent immediately. Read them at the start of every session, no exceptions.
- **Tier 2 (Read When Working):** STRUCTURE.md, WAYSOFWORKING.md, and HANDOFF.md. Load these when the agent is about to write code, make changes, or needs to know what happened last session.
- **Tier 3 (Read When Investigating):** PROVENANCE.md and EXPERIMENT_JOURNAL.md. Load these when the agent needs to understand why something is the way it is or what has already been tried.
- **Extension (Domain-Specific, Optional):** CLAIMS_TRACKER.md. Only relevant for projects with patent or IP tracking needs.

---

## Getting Started

### Path A -- Manual Setup

1. Copy the coordination template files to your project root.
2. Open each file and fill in the `[bracketed placeholders]` with your project's specifics.
3. At the start of each AI session, tell your agent: "Read PROJECT_CONTEXT.md and GLOSSARY.md before starting any work."
4. At the end of each session, update HANDOFF.md with what was accomplished and what comes next.

### Path B -- Amplifier Auto-Setup (recommended)

1. Copy the `project-context/` directory to your repository root.
2. Open an Amplifier session and use this prompt:

```
Read all the templates in project-context/ and set up project coordination
files for this project. Analyze the codebase to understand the project, then
generate customized versions of each coordination file at the project root.
Start with PROJECT_CONTEXT.md and GLOSSARY.md (Tier 1), then STRUCTURE.md,
WAYSOFWORKING.md, and HANDOFF.md (Tier 2). Ask me before generating Tier 3
files (PROVENANCE.md, EXPERIMENT_JOURNAL.md) or the optional CLAIMS_TRACKER.md.
```

3. Review the generated files and adjust anything the agent got wrong.
4. Commit the coordination files to your repo so they persist.

---

## Maintaining the Files

The value of these files depends entirely on keeping them current. Stale context is worse than no context because it misleads with confidence.

| File | Update Frequency | What to Update |
|------|-----------------|----------------|
| PROJECT_CONTEXT.md | Every session | Current phase, active milestone, active decisions |
| GLOSSARY.md | When new terms emerge | New terms, refined definitions, new anti-definitions |
| HANDOFF.md | End of every session | Rewrite completely with current session's state |
| STRUCTURE.md | When layout changes | New directories, moved files, changed conventions |
| WAYSOFWORKING.md | When patterns break or improve | New failure patterns, updated procedures, revised workflows |
| PROVENANCE.md | When decisions are made | New decision records with context and alternatives considered |
| EXPERIMENT_JOURNAL.md | After every experiment | New experiment entry with hypothesis, method, results, conclusion |
| CLAIMS_TRACKER.md | When claims evolve | Claim status changes, office action responses, new claims |

**Rule of thumb:** If you would re-explain something to a new team member, it belongs in one of these files.

---

## Amplifier Integration Tips

- **Always start with Tier 1.** Tell agents "Read PROJECT_CONTEXT.md and GLOSSARY.md before starting any work." This costs under 1000 tokens and prevents the most common failure modes (wrong assumptions about project state, terminology drift).

- **Use @-mentions for selective loading.** In Amplifier, agents can @-mention specific files. The tiered system means agents can load approximately 1000 tokens for orientation, then selectively load STRUCTURE.md, WAYSOFWORKING.md, or other files based on the task at hand.

- **HANDOFF.md is the highest-impact addition.** If you adopt only one practice from this system, make it this: update HANDOFF.md at the end of every session. It eliminates the "where was I?" problem that wastes the first 10 minutes of every new session.

- **Let agents update the files.** These files are living documents. When an agent discovers a new term, a new failure pattern, or makes a decision, ask it to update the relevant coordination file before ending the session.

- **Commit the files.** These are project artifacts, not scratch notes. Version-controlling them means you can see how project understanding evolved over time and revert if an agent introduces errors.
