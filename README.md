# Polymarket AI-Markets Edge Investigation

**A pre-registered, 30-day reconnaissance study of three candidate edge sources on Polymarket's AI-themed markets: news-to-market latency on release-date binaries, directional mispricing on leaderboard baskets, and catalyst-reaction tails on corporate/valuation markets.**

---

## Abstract

This repository documents a reconnaissance-mode investigation into whether retail-accessible trading edge exists on Polymarket's AI-themed markets for a single operator at $1k bankroll and 200-300ms network latency. The AI category hosts ~$10M in 30-day volume across 234 active markets (scanned 2026-04-21), concentrated in end-of-period leaderboard baskets, release-date binaries, and longer-horizon corporate/valuation markets.

Three hypotheses are characterised rather than tested against hard thresholds: H1 (news-to-market latency on release-date markets), H2 (leaderboard directional view), H3 (corporate catalyst repricing tails). Pre-commitment is on **reporting structure**, not on numerical GO thresholds — a deliberate shift from the hypothesis-test mode used in the sibling `trump-polymarket-replication` repo. The Day-30 verdict is a four-state call per hypothesis: GO, KILL, INCONCLUSIVE, or EXPLORATORY POSITIVE.

The integrity claim rests on five specific defences: pre-committed reporting categories, locked metric definitions, ÷5 heuristic on edge estimates, counter-memo before verdict, and a legitimate INCONCLUSIVE/EXPLORATORY POSITIVE verdict space so the researcher is not forced into a binary call on insufficient data.

No capital is committed at any phase. The 30-day observation runs forward from plan approval; the verdict lands when the window closes.

---

## Integrity artefacts

- [`PLAN.md`](PLAN.md) — full Phase 0 plan: research question, three hypotheses, reporting structures, 30-day schedule, non-goals, seven risks + mitigations.
- [`PRE_REGISTRATION.md`](PRE_REGISTRATION.md) — exact market lists (12 release-date binaries, 15 leaderboard candidates, 5 corporate markets), metric definitions, news-source registry, catalyst-source registry, locked non-goals.
- [`RISKS.md`](RISKS.md) — seven failure modes this experimental design is vulnerable to, with committed mitigations. R7 specifically addresses why loose kill gates permit HARKing and what defences replace that pressure.

Each of these committed before any observation pull. See git log for baseline timestamps.

## Four-state verdict

Each of H1 / H2 / H3 receives one of:

- **GO** — specific opportunity tradeable at the locked operator profile ($1k bankroll, 200-300ms latency).
- **KILL** — observation makes clear that retail edge is absent for this hypothesis at this operator profile.
- **INCONCLUSIVE** — insufficient data (sparse news cycle, missed catalysts, coverage lapse). Documented with what additional observation would resolve.
- **EXPLORATORY POSITIVE** — signal worth expanded investigation but current sample does not support committing capital. Documented with the exact Phase 1 test that would promote to GO.

## What this repo does and does not produce

**Produces:** a defensible four-state verdict per hypothesis, backed by the full pre-committed reporting tables, a counter-memo written before the verdict, and a git audit trail.

**Does not produce:** live trading, capital deployment, a paper-trade harness against live markets, a Phase 1 design, or any expansion beyond Polymarket AI markets. Phase 1 scoping is conditional on any non-KILL verdict and is a separate exercise.

## Relationship to the parent project

This study uses the same structural pattern as the sibling [`trump-polymarket-replication`](https://github.com/sturzael/trump-polymarket-replication) repo: pre-registration before data access, strict amendment-only policy, counter-memo requirement, git-as-audit-trail. The ÷5 heuristic and counter-memo discipline are carried over from the [`polymarket-edge-research`](https://github.com/sturzael/polymarket-edge-research) parent.

The one deliberate difference: this experiment runs in reconnaissance mode rather than hypothesis-test mode. Pre-committed reporting replaces pre-committed thresholds. This is a defensible choice for a category where we lack a prior to test (no analogue of trump-code's published 61.3%); it would be the wrong choice for a replication study.

## Disclosure

No capital is deployed at any phase. All observation data comes from public Polymarket APIs (Gamma, CLOB) and public news sources listed in the pre-registration. The operator profile, thresholds, and non-goals are stated in advance and will not be revised post-hoc. Independent audit of the verdict should begin by verifying that the five integrity commitments in [`RISKS.md`](RISKS.md) §R7 were honoured.
