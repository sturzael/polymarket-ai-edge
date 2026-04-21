# Phase 0 Plan — Polymarket AI-Markets Edge Investigation

**Status:** draft, pending review. Not executed. No data pulls conducted against this repo's experimental design.

**Mode:** reconnaissance, not hypothesis test. No pre-committed numerical GO thresholds; pre-commitment is on **what to report**, not on where the line is. The final GO / KILL / INCONCLUSIVE / EXPLORATORY-POSITIVE call is made by the researcher at Day 30 after reviewing the full data, with the reporting structure and non-goals fixed in advance to prevent retroactive metric selection.

---

## Research question

Is there retail-accessible trading edge on Polymarket's AI-themed markets — specifically the release-date, leaderboard, corporate-valuation, and benchmark-capability categories — at a $1k bankroll and 200-300ms network latency, over the next ~4 weeks of live observation?

**Operator profile (locked):**
- $1k bankroll simulated, no capital deployed
- 200-300ms network latency (NZ laptop, no VPS)
- REST/WebSocket polling only; no sub-second co-located execution
- Single-operator; no in-house news feed aggregation beyond free tools (Twitter, RSS, GitHub watches)

The conclusion should explicitly reference this operator profile. Any edge that requires VPS-colocation, $10k+ bankroll, or atomic multi-leg execution is out of scope regardless of what the data shows.

---

## Why this experiment is worth running

1. The AI-markets category on Polymarket is growing — ~$10M in 30-day volume across 234 active markets (scanned 2026-04-21). Biggest concentrations are leaderboard baskets and release-date binaries.
2. Unlike e10 (geopolitical news arbs, falsified at 1.12× ratio vs 3× threshold) and e22 (cross-venue spreads), AI news has **non-Twitter leading indicators**: HuggingFace uploads, GitHub commits in inference infrastructure repos, APK/iOS teardowns, DNS records. These are slower than Twitter and less automated.
3. The leaderboard baskets have **resolution ambiguity** ("best AI model" = which leaderboard, which conditions) that creates sustained pricing dispersion independent of latency.
4. Corporate/valuation markets (Anthropic cap, OpenAI IPO) have 12-20 month horizons and slow-developing catalysts — retail attention windows can matter here.

These are hypotheses, not findings. The experiment characterises rather than tests.

---

## Three hypotheses, characterised via observation (no hard GO thresholds)

### H1 — Release-date markets: what is the news-to-market latency distribution?

**What we measure:**
- Monitor all 12 active release-date markets (GPT-5.5/6, DeepSeek v4, Gemini 3.5, Claude Mythos, etc.)
- For each price jump ≥ 15 percentage points within any 60-minute window, identify the triggering news event timestamp (testingcatalog, official channels, Jimmy Apples, OpenAI, Anthropic, Twitter more broadly)
- Measure per-jump: lead time from news-timestamp to the moment the market reached 50% of the eventual move, and the moment it reached 90%
- Also measure: price jumps ≥ 15 pp where NO news event can be identified (baseline speculation-driven volatility)

**Pre-committed reporting structure (locked before observation):**
- Full table of all observed jumps ≥ 15 pp during observation window
- For each: market, timestamp, magnitude, candidate news events, chosen-news timestamp (if any), 50%-capture lead time, 90%-capture lead time
- Separate "news-identified" from "no-news-identified" jumps in the reporting
- Summary histogram of lead times, not a single median

**What the researcher decides at Day 30, not Day 1:**
- Whether the distribution of lead times on news-identified jumps is wide enough to support retail-accessible edge at this operator profile.
- Whether the observed sample size is sufficient to conclude anything.

### H2 — Leaderboard basket: is the current pricing directionally tradeable on a specific view?

**What we measure:**
- Build a decision-tree model of LM Arena #1 at April 30 using public information:
  - P(Anthropic holds) × P(no GPT-5.5 ship)
  - P(OpenAI takes #1) × P(GPT-5.5 ships AND leads arena)
  - P(other)
- Snapshot the market's implied probabilities at plan approval
- Update the model weekly as information arrives (release rumours, confirmations, leaderboard changes)
- At resolution (April 30), record the actual outcome

**Pre-committed reporting structure:**
- Weekly snapshot of model-vs-market delta
- Final outcome
- ÷5 heuristic applied to any observed model-vs-market delta before interpreting as edge
- Explicit note on whether any model parameter relied on information that would be asymmetric (i.e., non-public or not easily available to an attentive PM trader)

**What the researcher decides at Day 30:**
- Whether the observed model-market-delta trajectory across the 9 days to resolution suggests a persistent mispricing worth acting on in future similar markets, or whether the two converged as information arrived (market was efficient, modelling added nothing).

### H3 — Corporate / valuation markets: how do slow-developing catalysts actually reprice?

**What we measure:**
- Identify 3-5 corporate markets with 6-12 month resolution horizons (Anthropic cap band, OpenAI IPO, OpenAI acquired, IPO market cap thresholds)
- Monitor for catalysts over the 4-week window:
  - SEC filings (S-1, 8-K, amended filings)
  - Reputable funding-round reporting (WSJ, FT, The Information, Bloomberg)
  - Official company announcements
  - Leaked cap-table information via credible sources
- For each catalyst: record timestamp of first-public availability, trace market price at T+0, T+1h, T+6h, T+24h, T+72h

**Pre-committed reporting structure:**
- Full catalyst log with timestamps
- Per-catalyst repricing curve from T+0 through T+72h
- Separate analysis of "market moved before catalyst became public" cases (leaked in-market)
- Baseline repricing on non-catalyst weeks (drift only)

**What the researcher decides at Day 30:**
- Whether the corporate market repricing curve has a meaningful tail past T+1h where retail could have entered.

---

## Four-state verdict at Day 30

Each of H1/H2/H3 gets one of:

- **GO** — specific opportunity type clearly tradeable at the locked operator profile. Document the exact trade thesis, required edge over cost, and next-step Phase 1 plan.
- **KILL** — observation makes it clear retail edge is absent for this hypothesis at this operator profile. No further investigation.
- **INCONCLUSIVE** — insufficient data (e.g., sparse news cycle, missed catalyst, data quality issue). Document what additional observation would resolve it.
- **EXPLORATORY POSITIVE** — signal worth expanded investigation but current sample does not support committing capital. Document exactly what a Phase 1 would need to establish to promote to GO.

The researcher's Day-30 judgement is the decision. The integrity constraint is that the REPORTING structure above is fixed in advance — any observation that matches a pre-committed reporting category must be included in the Day-30 writeup regardless of whether it supports the eventual verdict.

---

## Thirty-day schedule

### Day 1 — Pre-registration [BLOCKING]

- Finalise and commit `PRE_REGISTRATION.md` with:
  - Exact list of markets monitored per hypothesis
  - Exact metrics reported per hypothesis (see H1/H2/H3 reporting structures above)
  - Commitment to report ALL observed events in the pre-registered categories
  - Non-goals (below)
  - News-source feeds: the exact list of channels we'll use to identify H1 news events (reduces post-hoc source selection bias)

### Day 2 — Retrospective calibration [non-blocking, informational]

- Pull hourly price history for all 12 release-date markets (last 30 days)
- Identify every hourly price jump ≥ 15 pp
- For each jump, research the triggering news event manually
- Compute lead-time distribution on this retrospective sample
- **No kill gate.** Result informs expectations but does not terminate observation. Live observation starts Day 5 regardless.

### Day 3 — H2 modelling [non-blocking]

- Build the H2 decision-tree model with current best estimates
- Snapshot market prices; compute initial model-market delta
- Apply ÷5 heuristic mentally to any delta before committing to "this looks like edge"
- **No kill gate.** Even if Day-3 model says "no edge," keep observing — the H2 question includes whether edge emerges as resolution approaches.

### Day 4 — H3 catalyst calendar [non-blocking]

- Research scheduled or rumoured catalysts during observation window
- Pre-register the catalyst list (post-hoc additions not allowed for H3 verdict purposes)
- **No kill gate.** Sparse catalyst calendar just means H3 is more likely to land INCONCLUSIVE.

### Day 5 — Monitoring infrastructure [BLOCKING for observation start]

- Deploy hourly price-pull loop for all pre-registered markets (release-date + leaderboard + corporate)
- Deploy news-event log scaffold (manual entry; automation is out of scope)
- Verify CLOB `/prices-history` rate limits against pull cadence
- Verify post-V2 (2026-04-22) fee structure matches pre-V2 sampling

### Days 6–29 — Live observation

- Daily: pull hourly price history updates
- On observed price jumps ≥ 15 pp within 60 min: log immediately; research triggering news event within 24 hours
- On observed corporate catalysts: log official-source timestamp; trace price movement through T+72h
- Weekly: update H2 model-vs-market delta
- Weekly: produce a brief progress note (what was observed, what's in the log, any data quality issues — nothing interpretive yet)

### Day 30 — Counter-memo + verdict [BLOCKING]

- Before writing the verdict, write `COUNTER_MEMO.md` arguing why the most natural interpretation of the data might be wrong, in both directions (false-GO and false-KILL).
- Apply ÷5 heuristic to every numerical edge estimate before including in the verdict.
- Produce `PHASE_0_VERDICT.md` with three separate H1/H2/H3 calls from {GO, KILL, INCONCLUSIVE, EXPLORATORY POSITIVE}.
- If EXPLORATORY POSITIVE on any hypothesis: document exactly what a Phase 1 would need to observe to promote to GO.

---

## Non-goals (locked)

1. **No capital deployed at any phase.** Paper trades only. If a Phase 1 recommendation follows, it requires a separate capital decision.
2. **No sub-100ms execution infrastructure.** The test is about whether retail latency is tradeable, not about upgrading retail latency.
3. **No building a news-event classifier.** Identifying triggering news is done manually with human judgement during observation. Automating it is Phase 1 work contingent on H1 non-KILL.
4. **No expansion beyond Polymarket AI markets.** Kalshi cross-venue is a related but separate experiment (considered in scope reasoning but out of scope for execution here).
5. **No speculation on rule classifications from the trump-code project.** This experiment has no rule-set to import.
6. **No live trading during the 30-day observation window.** Verdict comes at Day 30 after the full observation, regardless of intermediate appearances.
7. **No retroactive market additions.** Markets in the pre-registered list stay in. Markets not in it stay out. If a new high-volume AI market launches mid-observation, it's a Phase 1 candidate, not a Phase 0 addition.

---

## Integrity commitments (the thing that replaces pre-committed thresholds)

Because we are explicitly running in reconnaissance mode with no hard GO thresholds, these commitments carry the integrity weight:

- **All observed events in pre-registered categories appear in the Day-30 writeup.** No selective reporting. If 9 news-identified jumps happened and only 3 support a story, all 9 appear in the table with the same columns.
- **The metric definitions are fixed in advance.** What counts as a "jump" (≥15 pp within 60 min), what counts as "50%-capture lead time" (first timestamp at which price had moved ≥50% of the way from pre-jump to post-jump level), what counts as a "catalyst" (specific source list pre-registered) — all locked Day 1.
- **The ÷5 heuristic is applied before any edge estimate is used in a GO recommendation.** Imported from the event-impact-mvp findings log; has precedent in the trump-polymarket-replication counter-memo.
- **Counter-memo written before verdict.** Pre-committed adversarial pass arguing from the same data that both false-GO and false-KILL are plausible. Same pattern as trump-polymarket-replication Day 8.
- **EXPLORATORY POSITIVE is a legitimate verdict, not a cop-out.** Research that finds "worth further investigation but not yet actionable" is a real result.
- **The git log is the audit trail.** Pre-registration, observation logs, counter-memo, verdict are each separate commits with timestamps. Anyone can reconstruct the exact state of the experiment at each decision point.

---

## Risks and mitigations

### R1 — Sparse news cycle during observation window
AI announcements cluster. A 4-week window may have 0–1 major releases if timing is unlucky.
**Mitigation:** INCONCLUSIVE is a first-class verdict. A sparse window produces INCONCLUSIVE, not a spurious GO.

### R2 — Confirmation bias in news-correlation
When reverse-engineering "what news moved this price," researcher prior biases interpretation.
**Mitigation:** For every jump, log ALL candidate news events within ±60 min, not just the selected one. If multiple candidates are plausible, mark the lead time as ambiguous and exclude from headline numbers but include in the full table.

### R3 — "I understand AI better than the median PM trader"
H2 edge often evaporates when you realise PM AI traders include AI researchers.
**Mitigation:** ÷5 heuristic on any H2 delta. Explicit check in counter-memo: what would a Polymarket-attentive AI researcher already know that I'm claiming as edge?

### R4 — Polymarket data-API limitations (documented in trump-polymarket-replication)
`/trades` timestamp filter broken; pagination capped at offset=5000; hourly history caps ~30 days.
**Mitigation:** Observation relies on hourly pulls forward, not historical backfill. Day 5 infrastructure is sized for the forward window only.

### R5 — V2 cutover mid-experiment (2026-04-22, one day from today)
All observation post-V2. Fee structure, market mechanics may have changed.
**Mitigation:** Day 5 includes post-V2 fee re-verification. Pre-commit reporting at fee_bps ∈ {0, 3, 7.2, 15, 30} to cover any shift.

### R6 — Observation cost creep
30 days of daily pulls + event logging is sustained commitment. Lapsed coverage risk.
**Mitigation:** <21 of 30 days covered → INCONCLUSIVE on affected hypothesis. No partial-coverage GO claims allowed.

### R7 — The loose kill-gate structure permits HARKing
Without numerical thresholds, researcher may rationalise noise into signal at Day 30.
**Mitigation:** Pre-committed reporting structure + counter-memo + ÷5 heuristic are the defences. If these aren't honoured in spirit, the integrity pitch doesn't hold.

---

## What commits, and when

| Day | Artefact | Commit |
|-----|----------|--------|
| 1 | `PRE_REGISTRATION.md` — exact markets, metrics, non-goals | pre-observation timestamp |
| 2 | `docs/day2_retrospective_calibration.md` — jump-log + lead-time table | informational |
| 3 | `docs/day3_h2_model.md` — initial H2 model + market delta | informational |
| 4 | `docs/day4_catalyst_calendar.md` — pre-registered catalyst list | frozen before observation |
| 5 | `scripts/` — monitoring infrastructure, fee re-verification | pre-observation |
| 6-29 | weekly progress notes (no interpretation) | rolling |
| 30 | `COUNTER_MEMO.md` then `PHASE_0_VERDICT.md` | final |

Nothing commits to this repo until this plan is reviewed. No data pulls, no observation scaffolding, no retrospective calibration until sign-off.
