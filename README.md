# Project Context

Markdown templates that give AI agents persistent project memory across sessions.

Drop this into any repo, run one prompt, and your agent knows your project structure, terminology, decisions, failure patterns, and current state -- every session, without re-explaining.

## Quick Start

**1. Add to your project:**

```bash
# Option A: Clone into your repo
git clone https://github.com/michaeljabbour/project-context.git project-context

# Option B: Add as a submodule (gets updates when you pull)
git submodule add https://github.com/michaeljabbour/project-context.git project-context
```

**2. Generate your project's coordination files:**

Open an AI coding session and use the prompt in [`SETUP_PROMPT.md`](SETUP_PROMPT.md), or:

```
Read project-context/README.md first to understand the coordination file
system — its tiers, cognitive modes, and maintenance expectations. Then
read all the templates in project-context/templates/. Scan the codebase
to understand the project — its structure, language, dependencies, and
current state. Look for any existing files that already serve coordination
functions (READMEs, CONTRIBUTING guides, decision logs, changelogs,
onboarding docs, architecture docs, glossaries, etc.) and consolidate
their relevant content into the new format rather than starting from
scratch. Generate customized versions of each coordination file inside
the project-context/ directory (alongside the templates/ folder) — do
not modify anything inside project-context/templates/ (those are the
versioned source of truth). Start with PROJECT_CONTEXT.md and GLOSSARY.md
(Tier 1), then STRUCTURE.md, WAYSOFWORKING.md, and HANDOFF.md (Tier 2).
Ask me before generating Tier 3 files (PROVENANCE.md,
EXPERIMENT_JOURNAL.md) or the optional CLAIMS_TRACKER.md.
```

**3. Tell your agent to read the files.** At the start of each session:

> "Read project-context/PROJECT_CONTEXT.md and project-context/GLOSSARY.md before starting."

That's it. The agent now has project memory.

---

## How It's Organized

```
project-context/                    # Cloned into your repo
├── README.md                       # You are here
├── SETUP_PROMPT.md                 # Ready-to-paste prompts
├── CHANGELOG.md                    # Template version history
├── LICENSE                         # MIT
├── templates/                      # Versioned source of truth — don't edit
│   ├── PROJECT_CONTEXT.md
│   ├── GLOSSARY.md
│   ├── STRUCTURE.md
│   ├── WAYSOFWORKING.md
│   ├── HANDOFF.md
│   ├── PROVENANCE.md
│   ├── EXPERIMENT_JOURNAL.md
│   └── CLAIMS_TRACKER.md
│
│   # After running the setup prompt, your generated files appear here:
├── PROJECT_CONTEXT.md              # ← Generated, project-specific
├── GLOSSARY.md                     # ← Generated, project-specific
├── STRUCTURE.md                    # ← etc.
├── WAYSOFWORKING.md
├── HANDOFF.md
├── PROVENANCE.md
├── EXPERIMENT_JOURNAL.md
└── CLAIMS_TRACKER.md               # (optional)
```

**Templates** are the versioned reference — they never change per-project. **Generated files** (at the project-context/ root) are your project-specific living documents, maintained session to session. The same filename in both places is intentional: templates are the schema, generated files are the instances.

---

## The Files

Eight templates, organized into tiers by how often agents should read them.

### Tier 1 -- Always Read (<1000 tokens combined)

| File | Purpose |
|------|---------|
| **PROJECT_CONTEXT.md** | Current project state at a glance: phase, version, team, active milestone. Cheap to load, answers "where am I?" instantly. |
| **GLOSSARY.md** | Terminology contract. "We say X, we mean Y, we do NOT mean Z." Prevents agents from silently substituting synonyms that blur important distinctions. |

### Tier 2 -- Read When Working

| File | Purpose |
|------|---------|
| **STRUCTURE.md** | Directory layout, naming conventions, routing table ("I have X, where does it go?"). Prevents files from being created in wrong locations. |
| **WAYSOFWORKING.md** | Session loop, proven workflows, named failure patterns (symptom/cause/fix), verification commands, error recovery protocol. The operational playbook. |
| **HANDOFF.md** | Session continuity. What happened last, what's blocked, what to do next. Rewritten at the end of every session. Highest-impact single file if you adopt only one. |

### Tier 3 -- Read When Investigating

| File | Purpose |
|------|---------|
| **PROVENANCE.md** | Decision journal. Why things are the way they are, what alternatives were considered, what was tried and abandoned. Prevents agents from re-proposing rejected approaches. |
| **EXPERIMENT_JOURNAL.md** | Scientific record. Hypothesis before results, raw data in tables, root cause analysis, running summary. Prevents confabulation. |

### Extension -- Optional

| File | Purpose |
|------|---------|
| **CLAIMS_TRACKER.md** | Patent/IP tracking. Claims, prior art maps, prosecution timeline. Only for projects heading toward filings. |

---

## Why It Works

These files aren't organized by topic -- they're organized by **cognitive mode**. Each maps to a different kind of thinking an agent does:

| File | Thinking Mode | Agent's Question |
|------|--------------|-----------------|
| PROJECT_CONTEXT | Orientation | "Where am I?" |
| GLOSSARY | Semantic grounding | "What do these terms mean?" |
| STRUCTURE | Spatial reasoning | "Where do things go?" |
| WAYSOFWORKING | Procedural reasoning | "How do I work here?" |
| HANDOFF | Session continuity | "What just happened?" |
| PROVENANCE | Causal reasoning | "Why was it done this way?" |
| EXPERIMENT_JOURNAL | Scientific reasoning | "What was tried?" |
| CLAIMS_TRACKER | Strategic reasoning | "What do we protect?" |

This means agents load **only the context relevant to their current task** instead of a monolithic README. Less noise in the context window, more accurate behavior, and knowledge that compounds across sessions instead of evaporating.

**Three mechanisms drive the compounding:**

1. **The terminology table** (GLOSSARY.md) acts as a type system for natural language. The "Does NOT Mean" column constrains interpretation the way a type signature constrains code.

2. **Named failure patterns** (WAYSOFWORKING.md) create institutional memory. An agent in session 12 benefits from the pain of session 3 without repeating it.

3. **Feedback loops** between files: experiments produce findings, findings inform decisions (PROVENANCE), decisions shape procedures (WAYSOFWORKING), procedures guide better experiments.

---

## Maintaining the Files

The value depends entirely on keeping them current. Stale context is worse than no context.

| File | When to Update |
|------|---------------|
| PROJECT_CONTEXT.md | Every session (current phase, milestone) |
| GLOSSARY.md | When new terms emerge |
| HANDOFF.md | End of every session (rewrite completely) |
| STRUCTURE.md | When directory layout changes |
| WAYSOFWORKING.md | When something breaks or a better pattern emerges |
| PROVENANCE.md | When decisions are made |
| EXPERIMENT_JOURNAL.md | After every experiment |
| CLAIMS_TRACKER.md | When claims evolve |

**Rule of thumb:** If you'd re-explain it to a new team member, it belongs in one of these files.

---

## Updating Templates

This repo is versioned with [semantic versioning](https://semver.org/). To get template updates:

```bash
# If cloned directly
cd project-context && git pull

# If using a submodule
git submodule update --remote project-context
```

Template updates don't affect your generated files. Templates are the schema; your generated files are the instances. If a new template version adds a section you want, manually add it to your generated file or re-run the setup prompt (it will consolidate existing content).

See [CHANGELOG.md](CHANGELOG.md) for what changed per version.

---

## Future

This is currently a set of templates. Planned evolution:

- **Amplifier skill** -- loadable via `load_skill()` for automatic discovery
- **Amplifier bundle** -- context injection with agent directives and tiered auto-loading
- **Agent-maintained updates** -- agents automatically update coordination files as they work

Contributions and feedback welcome via issues.

---

## License

[MIT](LICENSE)
