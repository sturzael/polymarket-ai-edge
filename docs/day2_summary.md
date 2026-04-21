# Day 2 — Retrospective Calibration Summary

**Status:** observational; no kill gate per loose-mode plan. Day 2 output feeds the `PRE_REGISTRATION.md` amendment (Class 1/2 source expansion + `event_type` classification) and surfaces one out-of-scope observation logged for possible Phase 1 scoping.

---

## What Day 2 did

1. Pulled hourly price history (CLOB `/prices-history?fidelity=60`, ~30-day window) for all 12 pre-registered H1 release-date markets.
2. Detected 47 price jumps (≥15 pp within a 60-min window, plus ≥15 pp over rolling 3-hour cascades).
3. Spawned 8 parallel research agents to investigate candidate triggering news events for the top 8 priority jumps (distinct event clusters).
4. Spawned 4 parallel research agents for retrospective release-date coverage across Anthropic / OpenAI / Google+DeepSeek / Alibaba+Meta+xAI+Mistral since 2026-02-01.
5. Spawned 1 agent for current-day (last 48-hour) AI leaks sweep.
6. Pulled hourly price history for the H2 leaderboard basket markets (Anthropic, OpenAI, Alibaba, Google, xAI, DeepSeek, Moonshot — end-of-April 2026).
7. Cross-referenced detected step functions in H2 market prices against known release events.

---

## 8-jump news correlation — results

Logged in `day2/jump_news_candidates.json`. Summary:

| Jump | Date | Market | Δ pp | event_type | Source class after amendment |
|------|------|--------|-----:|------------|------------------------------|
| 1 | 2026-04-07 | Claude Mythos | −52.0 | resolution_criterion | Class 1 (anthropic.com/news) |
| 2 | 2026-03-31 | DeepSeek v4 | +35.0 | no-news-identified | — (deadline-day speculation) |
| 3 | 2026-04-10 | GPT-5.5 April-23 cascade | −30.0 | release_date_speculation | Class 1 (OpenAI employee tweets — added via amendment) |
| 4 | 2026-04-13 | GPT-5.5 April-21 surge | +28.4 | release_date_speculation | Class 1 + Class 2 (mixed: OpenAI employee re-amp + @synthwavedd + @Polymarket venue-endogenous) |
| 5 | 2026-04-14 | GPT-5.5 April-21 collapse | −29.4 | release_date_speculation | Class 2 (@synthwavedd) |
| 6 | 2026-04-14 | GPT-5.5 April-23 surge | +26.0 | release_date_speculation | Class 1 (@kimmonismus amplifying Dresser memo) |
| 7 | 2026-04-19 | MAI model | +29.0 | resolution_criterion | Class 1 (microsoft.com/ai + @testingcatalog) **BUT 5-day lag** — see §"out-of-scope observation" |
| 8 | 2026-03-28 | Claude Mythos | +21.0 | resolution_criterion | Class 1 (Fortune + anthropic.com + @testingcatalog + @kimmonismus) |

Effective Class-1 H1-valid (`release_date_speculation`) jumps in Day 2 retrospective: **3** (jumps 3, 4, 6).

---

## Retrospective release timeline assembled

From four parallel research agents. Major frontier releases 2026-02-01 to 2026-04-21:

**Anthropic:**
- 2026-02-05: Claude Opus 4.6
- 2026-02-17: Claude Sonnet 4.6
- 2026-04-16: Claude Opus 4.7

**OpenAI:**
- 2026-02-05: GPT-5.3-Codex
- 2026-03-05: GPT-5.4 (flagship)
- 2026-04-14: GPT-5.4-Cyber (gated only)
- 2026-04-16: GPT-Rosalind (life-sciences, Trusted Access only)

**Google:**
- 2026-02-12: Gemini 3 Deep Think upgrade
- 2026-02-19: Gemini 3.1 Pro (flagship)

**DeepSeek:**
- 2026-02-15: DeepSeek V3.2 + V3.2-Speciale
- (V4 not yet released; Polymarket at 90% by May 15)

**Alibaba (Qwen):**
- 2026-04-02: Qwen 3.6 Plus
- 2026-04-20: Qwen 3.6 Max-Preview

**xAI:** Grok 4.2 (Feb), Grok 4.3 Beta (Apr 17)

**Other Chinese labs:** GLM-5 / GLM-5.1 (Z.ai), Doubao-Seed-2.0 (ByteDance), Kimi K2.6 Code Preview (Moonshot, Apr 13)

---

## Lag measurement against H2 leaderboard basket

For each known release event, measured how fast the Anthropic/OpenAI/Alibaba/etc. "best AI model end of April" markets repriced.

| Release event | Market measured | Lag to 50% of total move | Move size |
|---------------|-----------------|--------------------------|-----------|
| GPT-5.5 Spud production-test leak (2026-04-19 12:00 UTC) | GPT-5.5-Apr-23 release-date market | **~5 hours** | +6pp (0.745→0.805) |
| Mythos Preview announcement (2026-04-07 17:00 UTC) | Anthropic-April best-model | **minutes (real-time)** | ~8pp round-trip |
| Claude Opus 4.7 (2026-04-16 15:00 UTC) | Anthropic-April best-model | **pre-priced** (market at 0.90+ before release) | ~0pp at release |
| **Qwen 3.6 Max-Preview (2026-04-20 00:00 UTC)** | **Anthropic-April best-model** | **~20 hours** | **−13pp (0.925→0.795)** |
| **Qwen 3.6 Max-Preview (2026-04-20 00:00 UTC)** | **OpenAI-April best-model** | **~20 hours** | **+13.9pp (0.056→0.195)** |
| **MAI-Image-2-Efficient (2026-04-14)** | **MAI-by-April-30 release market** | **~5 days** | **+29pp (0.235→0.525)** |

---

## Out-of-scope observation (logged for Phase 1, NOT folded into H1 verdict)

Day 2 surfaced a pattern NOT predicted by H1 as pre-registered:

**Polymarket AI-market bot coverage appears to be asymmetric by lab origin.**

- **Tight coverage** on Western flagship labs (Anthropic, OpenAI, Google): repricing happens in minutes to ~5 hours of major news. Bots capture the edge.
- **Loose coverage** on peripheral Western labs (Microsoft AI) and Chinese frontier labs (Alibaba, DeepSeek, Moonshot, etc.): repricing takes 20 hours to 5+ days.

n = 2 clean cases (Qwen Max 20h, MAI 5d) plus 1 counter-example (GPT-5.5 Spud 5h fast). This is **not a claim** — the sample is too small and selection-biased (we went looking for jumps; we found the ones where inattention happened to be the cause). But the direction is consistent with the Day-1 pre-registration's own blind spots (no Chinese-language media, no @mustafasuleyman, no OpenAI-employee handles) — the market appears to have similar blind spots.

**What this means for the experiment:**

Per our pre-commitment to NOT HARK (adding hypotheses after seeing which ones fit the data), this observation is **explicitly NOT promoted to H4 in this experiment.** The H1/H2/H3 scope is unchanged. The observation is logged here for transparency and flagged in the Day-30 verdict's "Phase 1 recommendations" section if the verdict is any non-KILL state.

**What a Phase 1 on this hypothesis would look like:**
- Pre-register a watchlist of "peripheral + non-Western flagship labs" (Alibaba, DeepSeek, Moonshot, ByteDance, Z.ai, Baidu, Meituan, Microsoft AI, xAI)
- For each release event, measure lag to 50% / 90% repricing on the matching Polymarket market
- Over a 30-day window (needs n ≥ 10 release events), characterise the lag distribution
- Pre-commit trade sizing and entry/exit rules
- Require Class-1 source attribution for each release to count

**Why this is NOT being done here:**
1. Adding H4 mid-experiment is the exact HARKing failure mode the pre-registration discipline is supposed to prevent. The fact that it looks tradeable now doesn't make it integrity-valid now.
2. The H4 watchlist would need its own pre-registration amendment; writing it after seeing the MAI/Qwen observations means the watchlist itself is data-informed.
3. The clean path is: finish H1/H2/H3 at Day 30, propose H4 for a fresh Phase 1 with its own clock.

---

## Current-day leaks (as of 2026-04-21)

Summary from 48-hour sweep:

1. **GPT-5.5 "Spud" caught in production testing on 2026-04-19** — API monitors detected live scale-test runs. Already captured: GPT-5.5-April-23 market moved from 0.745 to 0.805 within 5 hours of the leak. No retail edge remaining on this specific signal.
2. **LM Arena changelog 2026-04-17:** Claude Opus 4.6 Thinking at #1 overall (1504 Elo); Claude Opus 4.7 added Apr 17; Grok 4.20 Beta 1 at #4. Consistent with Anthropic's current 80% pricing on Anthropic-April best-model.
3. **Claude Mythos staying gated** — Foreign Policy (2026-04-20) and Barracuda blog reiterate Project Glasswing is invitation-only.
4. **DeepSeek V4 still pending** — Reuters/Gizchina reports continue to project late-April launch, but no official announcement as of 2026-04-21.
5. **No fresh Gemini 3.5 news.** No new MAI frontier-tier release.

---

## Day 2 artefacts

- `day2/jump_news_candidates.json` — 8-jump news correlation output
- `data/h1_jumps.json` — 47 detected price jumps (gitignored; regenerable)
- `data/h2_leaderboard_history.json` — hourly price history for 7 H2 markets (gitignored)
- `PRE_REGISTRATION.md` amendment — source-list expansion + event_type classification + Day-30 reporting separation

## What Day 2 does not change

- Any H1/H2/H3 numerical threshold (none exist by design)
- The 30-day observation window scope
- Non-goals
- The loose-kill-gate mode

## What Day 2 does change

- Expanded news-source list (Class 1 + Class 2 with separate reporting commitment)
- New `event_type` column in the reporting structure
- Revised preliminary read on H1 (retraction of earlier "EXPLORATORY POSITIVE territory" framing — effective Class-1 H1-valid sample in Day 2 = 3 jumps, insufficient for directional claim)
