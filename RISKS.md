# Risks and Mitigations — Polymarket AI-Markets Edge Investigation

Seven specific failure modes this experimental design is vulnerable to, and the mitigation committed to for each. These are more load-bearing than usual because this experiment uses pre-committed *reporting* rather than pre-committed *numerical thresholds* — the integrity defence is spread across these risks rather than concentrated in a single GO line.

---

## R1 — Sparse news cycle during observation window

**Failure mode.** AI announcements cluster around conferences and scheduled releases. A 4-week window may contain 0–1 major events if timing is unlucky. H1 can't be evaluated with n=1.

**Mitigation.** INCONCLUSIVE is a first-class verdict per the four-state framework. A sparse window produces INCONCLUSIVE on H1, not a spurious GO from a single lucky jump. Pre-committed rule: fewer than 5 price jumps ≥ 15 pp with identifiable news → INCONCLUSIVE.

---

## R2 — Confirmation bias in news correlation

**Failure mode.** When reverse-engineering "what news moved this price," researcher prior expectations bias interpretation. A jump at 21:00 might be attributed to a testingcatalog tweet at 20:45 when the real driver was a different event five minutes later.

**Mitigation.** For every jump, log ALL candidate news events within ±60 min to the event log, not just the selected one. If multiple candidates are plausible, mark the lead time "ambiguous" and exclude from headline median statistics while still reporting in the full table. Pre-committed news source list prevents post-hoc source addition when a convenient event can't be found.

---

## R3 — "I understand AI better than the median Polymarket trader"

**Failure mode.** H2 edge often evaporates once you realise Polymarket AI traders include AI researchers. What looks like retail insight is frequently asymmetric information the other side also has.

**Mitigation.** ÷5 heuristic applied to any H2 delta before it's quoted in the verdict. Explicit check in the Day-30 counter-memo: "what would an attentive Polymarket-AI trader already know that I'm claiming as edge?" If the model's edge depends on information a pro could source in 15 minutes on Twitter, it is not retail edge.

---

## R4 — Polymarket data-API limitations propagate (carried from trump-polymarket-replication)

**Failure mode.** The data-api `/trades` endpoint accepts but ignores timestamp filters; pagination caps at offset=5000; CLOB `/prices-history` returns hourly data only for the last ~30 days. These constraints limit what the experiment can measure.

**Mitigation.** Observation relies on hourly-forward pulls, not historical backfill. Day 5 infrastructure sized for the 30-day forward window only. If an H3 catalyst requires trade-volume detail beyond what's accessible, the catalyst is logged with the data we have and flagged for Phase 1 if the question warrants it.

---

## R5 — V2 cutover mid-experiment (2026-04-22, one day after pre-registration)

**Failure mode.** CTF Exchange / CLOB V2 cutover occurred one day after pre-registration. Fee structure and order mechanics may have changed in ways that alter baseline behaviour across the observation window.

**Mitigation.** Day 5 infrastructure deployment includes post-V2 fee re-verification (CLOB `/markets/<cid>` base-fee check across sampled AI markets, same pattern as trump-polymarket-replication Day 3 PM). Pre-commit reporting at fee_bps ∈ {0, 3, 7.2, 15, 30} to cover any V2 shift in baseline fees. V2-specific structural breaks (if observed) get a dedicated section in the Day-30 verdict.

---

## R6 — Observation cost creep

**Failure mode.** A 30-day daily observation schedule plus manual news-event correlation is sustained researcher commitment. Risk: observation lapses after week 2, producing partial data that still gets used for conclusions.

**Mitigation.** Pre-committed coverage rule: if fewer than 21 of 30 days have completed observation logs, the affected hypothesis lands INCONCLUSIVE. No partial-coverage GO claims allowed. Weekly progress notes (Days 12, 19, 26) provide visible checkpoints; if a checkpoint reveals lapsed coverage, the researcher decides whether to extend the window or mark INCONCLUSIVE — not whether to quietly backfill.

---

## R7 — The loose kill-gate structure permits HARKing

**Failure mode.** Without numerical GO thresholds, the researcher may rationalise noise into signal at Day 30. "Well, we observed lead times of 18–45 minutes, which *could* be retail-accessible if you squint, and the model-market delta on H2 was 4pp which is *close* to the 5pp I was going to require, so…"

**Mitigation.** The integrity weight rests on five specific defences:
1. Pre-committed reporting categories (can't selectively report)
2. Metric definitions locked Day 1 (can't redefine what counts as a jump or lead time)
3. ÷5 heuristic on all edge estimates (halves any post-hoc rationalised edge)
4. Counter-memo before verdict (forces adversarial pass)
5. EXPLORATORY POSITIVE verdict (legitimate category for "worth more investigation, not yet actionable")

If any of these five are skipped in spirit, the Day-30 verdict has no integrity claim. The reviewer of the verdict should check that each was honoured before crediting the result.

---

## Residual risks not fully mitigated

Documented for the Day-30 reviewer even though no clean mitigation fits the 30-day budget.

### Resolution ambiguity on H2 leaderboard basket

"Best AI model" resolves by some canonical leaderboard (expected: LM Arena on April 30). If the leaderboard has a tie, a re-ranking, or a resolution-source change, the market may not resolve as the researcher's model expects. Phase 0 does not address this; a Phase 1 on H2 would need to pre-commit a resolution source per candidate and monitor for changes.

### Observation Heisenberg effect

If the researcher publicly shares observations during the 30-day window (Twitter, public repo commits), this could influence trader behaviour on low-volume AI markets. Not expected at observation scale but worth noting.

### Platform-level mechanics change mid-window

Polymarket could add, remove, or restructure markets during the window (e.g., launch a May 2026 leaderboard basket mid-April, or pause a market due to regulatory action). Mid-window platform changes are logged as amendments but not compensated for in the verdict — they can shift a hypothesis from meaningful to irrelevant and that becomes part of the result.

### Single-operator subjectivity

All news-correlation judgements are made by one researcher. An independent second-pass on the event log would strengthen any positive finding but is out of scope for Phase 0.
