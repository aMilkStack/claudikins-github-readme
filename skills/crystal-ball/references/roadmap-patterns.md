# Roadmap & Future Vision Patterns

**Goal:** Present what the project COULD become without overpromising or creating maintenance burden.

---

## Why Roadmaps Matter

A public roadmap serves multiple functions:

1. **Defines Scope** - Empowers maintainers to reject off-vision requests
2. **Builds Trust** - Enterprise adopters need confidence before committing
3. **Attracts Contributors** - Shows where help is needed
4. **Manages Expectations** - Prevents "when will X ship?" burnout

---

## Roadmap Format Options

Choose based on project size and governance style.

**Key insight:** Format choice signals target audience.
- Static, commitment-based → Enterprise adopters (need predictability)
- Dynamic, discussion-based → Developers (want velocity and input)

### Integrated File

A `ROADMAP.md` version-controlled alongside source code.

**Pros:** Git-tracked, no context switching, shows vision evolution via blame.
**Cons:** Can go stale if not actively maintained.
**Best for:** Projects with clear scope and single maintainer/small team.

### Pinned Issue

Time-bound GitHub Issues (e.g., "Roadmap: Q1 2026") pinned to Issues tab.

**Pros:** Natural expiration prevents staleness, interactive comments, forces regular updates.
**Cons:** Requires discipline to refresh quarterly.
**Best for:** Projects with operational rhythm and community feedback needs.

### Project Board

Public GitHub Projects board showing features in Kanban columns.

**Pros:** Real-time visibility, demystifies development, "open development" ethos.
**Cons:** Can expose too much internal churn, requires curation.
**Best for:** Community-driven projects emphasising transparency.

### External Portal

Blog posts or dedicated website pages.

**Pros:** Rich storytelling, marketing-friendly, aggregates multiple workstreams.
**Cons:** Disconnected from code, higher maintenance overhead.
**Best for:** Large projects with sub-teams or venture backing.

---

## Temporal Strategies

How to signal WHEN without overpromising.

### Future Flags

Release breaking changes behind opt-in config flags in current version.

```typescript
export default {
  future: {
    v3_newBehaviour: true,
  }
};
```

**Effect:** Migration becomes gradual ramp, not cliff. Users adopt incrementally.

### Release Trains

Fixed schedule (e.g., minor releases every 6-12 weeks).

**Effect:** "When?" becomes predictable. Users only ask "What?" makes the cut.

### Editions / Epochs

Bundle breaking changes into multi-year milestones (v1, v2, 2024 Edition).

**Effect:** Stability guaranteed between editions. Provides rallying point for ecosystem.

### Extended Beta

Keep versions in beta/next state while being production-ready.

**Effect:** Gathers real-world feedback before API freeze. Requires high trust.

### Dual-Track Versioning

Separate versioning for breaking changes vs incremental releases.

- **Editions/Years** for breaking changes (2024 Edition, v2.0)
- **SemVer** for incremental releases (1.84.0, 1.85.0)

**Effect:** Features ship when ready, breaking changes batch into predictable epochs. Prevents roadmap stagnation.

### Marketing Majors

Major version bump signals philosophy shift, not just technical breakage.

**Example:** "v2.0" announces "we changed direction" even if migration is minimal.

**Use when:** Pivoting strategy, entering new market, or shedding legacy reputation.

---

## Status Indicators

Define your legend explicitly. Don't assume meaning is universal.

### Recommended Status Set

| Status | Meaning | Commitment Level |
|--------|---------|------------------|
| **Complete** | Shipped and stable | Done |
| **In Progress** | Actively being built | High |
| **Planned** | Committed, not started | Medium |
| **Considering** | Needs feedback, may happen | Low |
| **Not Planned** | Explicitly out of scope | None |

### What Each Status Communicates

- **Complete:** Safe to depend on
- **In Progress:** Expect volatility, don't build on yet
- **Planned:** Will happen, timeline uncertain
- **Considering:** Your input matters here
- **Not Planned:** Stop asking for this

---

## Technical Debt Transparency

Mature projects roadmap their debt, not just features.

### Include Maintenance Goals

```markdown
## Q1 2026 Goals

### Features
- New caching layer
- Plugin API v2

### Maintenance
- Configuration cleanup
- Deprecate legacy API
- Reduce test flakiness
```

**Why:** Shows long-term thinking. Experienced developers trust projects that allocate cleanup time.

### Acknowledge Limitations Honestly

```markdown
## Known Limitations

- Large files (>10MB) may be slow - optimisation planned for v2.1
- Windows ARM support experimental - please report issues
```

**Effect:** Builds trust through honesty. Users appreciate knowing the edges.

### Drop Support Gracefully

Link to external policies when deprecating:

```markdown
## Deprecations

- **Node.js 18:** Dropped per Node.js LTS schedule
- **Legacy API:** Removed after 12-month deprecation period
```

**Effect:** Externalises justification. "The ecosystem moved, not us."

---

## The Negative Roadmap

Explicitly state what the project will NOT do. This builds trust and prevents scope creep.

### Boundaries Document

```markdown
## Scope & Boundaries

### What This Project IS
- A lightweight CLI for X
- Optimised for single-user workflows

### What This Project is NOT
- A GUI application (use [Alternative] instead)
- A replacement for [Enterprise Tool]
- Suitable for >10GB datasets
```

### "Won't Fix" Transparency

```markdown
## Known Limitations (Won't Fix)

| Limitation | Reason | Alternative |
|------------|--------|-------------|
| No Windows GUI | Out of scope | Use WSL |
| Single-threaded | By design for simplicity | Use [Other Tool] for parallelism |
```

**Effect:** Empowers maintainers to reject off-vision requests without personal conflict. Users self-select out if project doesn't fit their needs.

---

## Contribution Hooks

Turn roadmap readers into contributors.

### Label Strategy

| Label | Purpose |
|-------|---------|
| `help wanted` | Open for external contribution |
| `good first issue` | Suitable for newcomers |
| `needs design` | Requires RFC/discussion first |
| `blocked` | Waiting on dependency/decision |

### Surface Opportunities

```markdown
## Help Wanted

We'd appreciate contributions in these areas:

| Area | What's Needed | Difficulty |
|------|---------------|------------|
| Tests | Coverage for `src/core/` | Beginner |
| Docs | API reference gaps | Beginner |
| Performance | Profiling large datasets | Advanced |
```

### Democratic Prioritisation

```markdown
## Community Priorities

Focusing on highly-upvoted issues this quarter:
- #1234 - Feature X (500+ reactions)
- #5678 - Bug Y (300+ reactions)
```

**Effect:** Incentivises engagement, creates feedback loop.

---

## Anti-Patterns to Avoid

### Wishlist Without Owners

Ideas listed with no champion, timeline, or path to implementation.

**Fix:** Require owner assignment. Remove items without champions.

### Ghost Ship

Roadmap last updated years ago, still linked from README.

**Fix:** Use time-bound formats that naturally expire (Pinned Issues > static files).

### Vaporware

Features promised as "coming soon" indefinitely.

**Fix:** Use explicit status. Distinguish "considering" from "building".

### Secret Garden

Real roadmap on private board; public version is sanitised or delayed.

**Fix:** If claiming open development, make planning genuinely public.

### Unbounded Scope

Every feature request gets added to roadmap.

**Fix:** README states philosophy. Reject requests that violate core principles.

### Help Wanted Ghosting

Tagging issues as `help wanted` but never reviewing submitted PRs.

**Effect:** Destroys contributor morale. Turns roadmap into a lie.

**Fix:** Only tag `help wanted` if someone is assigned to review. If you ask for help, be ready to receive it.

### Zero-Ver Dissonance

Operating in v0.x forever while being used in production.

**Effect:** Creates expectation mismatch. Users expect stability from tools they depend on, but v0.x technically promises none.

**Fix:** Either graduate to v1.0 with stability guarantees, or explicitly document "v0.x but production-ready" status.

---

## Version Signalling

### Granular Stability Flags

Instead of monolithic "unstable" flag, offer per-feature opt-in.

```bash
# Bad: all-or-nothing
--unstable

# Good: granular opt-in
--unstable-kv
--unstable-cron
--unstable-ffi
```

**Effect:** Transforms "Is the project stable?" into "Is feature X stable?" - much easier question for adoption decisions. Enterprise users can opt-in to specific experimental features without risking core stability.

### Maturity Indicators

| Stage | Signal | Language |
|-------|--------|----------|
| **Experimental** | Breaking changes likely | "API may change" |
| **Beta** | Feature-complete, stabilising | "Production use with caution" |
| **Stable** | API frozen | "v1.0+ - Stable" |
| **Mature** | Battle-tested | "Used in production by X" |

### Breaking Change Communication

```markdown
## Breaking Changes in v3

### Removed
- `legacyMode` option (deprecated in v2.5)

### Changed
- `parse()` returns `Result<T>` instead of throwing

### Migration
See [MIGRATION.md](./MIGRATION.md) for upgrade path.
```

---

## Maintenance Status Signals

### Active

```markdown
## Status: Active

- Bug fixes: Within 1 week
- Security: Within 48 hours
- Features: Reviewed quarterly
```

### Maintenance Mode

```markdown
## Status: Maintenance Mode

Feature-complete. Accepting bug fixes and security patches only.
```

### Seeking Maintainers

```markdown
## Status: Seeking Maintainers

Unable to maintain actively. Interested? Open an issue.
```

---

## Implementation Checklist

- [ ] Roadmap accessible within one click from README
- [ ] Status legend defined explicitly
- [ ] Items needing feedback clearly marked
- [ ] Maintenance/debt work included
- [ ] Versioning and stability policy stated
- [ ] Contribution opportunities labelled (with reviewers assigned)
- [ ] Format chosen that prevents staleness
- [ ] Boundaries stated (what project is NOT)
- [ ] Known limitations documented honestly

---

## Quick Reference: Format by Situation

| Situation | Recommended Format |
|-----------|-------------------|
| Solo maintainer | Integrated ROADMAP.md |
| Active community | Pinned Issues (quarterly) |
| Transparency focus | Public Project Board |
| Marketing needs | External blog/portal |
| Rapid iteration | Release train schedule |
