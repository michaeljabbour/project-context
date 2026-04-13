# Changelog

All notable changes to the project coordination templates.

This project uses [Semantic Versioning](https://semver.org/):
- **MAJOR**: Breaking changes to template structure (renamed files, removed sections)
- **MINOR**: New templates, new sections in existing templates, new features
- **PATCH**: Fixes to wording, formatting, or examples

---

## [1.0.0] - 2026-04-13

### Added
- Initial release of 8 project coordination templates
- **PROJECT_CONTEXT.md** (Tier 1) -- current project state at a glance
- **GLOSSARY.md** (Tier 1) -- terminology contract with anti-definitions
- **STRUCTURE.md** (Tier 2) -- directory layout and file routing table
- **WAYSOFWORKING.md** (Tier 2) -- session loop, failure patterns, error recovery protocol
- **HANDOFF.md** (Tier 2) -- session continuity between work sessions
- **PROVENANCE.md** (Tier 3) -- decision journal with structured IDs
- **EXPERIMENT_JOURNAL.md** (Tier 3) -- scientific experiment record with archival policy
- **CLAIMS_TRACKER.md** (Extension) -- patent/IP tracking (optional)
- YAML frontmatter on all templates (type, tier, priority, tokens_estimate)
- HTML comment agent directives for machine-readable behavioral hints
- Structured entry IDs for cross-referencing between files
- Tiered loading system (Tier 1 always, Tier 2 when working, Tier 3 on demand)
- SETUP_PROMPT.md with ready-to-use prompts for full setup, quick setup, session start, and session end
