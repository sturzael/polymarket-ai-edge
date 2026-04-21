# Can a Laptop Trader Beat the Bots on Polymarket's AI Markets?

**A pre-registered reconnaissance study into whether a retail operator with $1k and 200-300ms latency can find tradeable edge on Polymarket's AI-themed markets — release-date binaries, leaderboard baskets, and corporate-valuation markets.**

**Status:** pre-registration and Day-2 retrospective calibration complete. Forward observation window (30 days) is planned — not yet begun. Verdict lands at end of observation window.

> 👉 **Not a markets person?** Read the [Explain Like I'm Five version](docs/ELI5.md) *(coming soon)* instead.

---

## TL;DR

- AI markets on Polymarket are the fastest-growing category: **~$10M in 30-day volume across 234 active markets** (scanned 2026-04-21)
- Tested three hypotheses: news-to-market latency, leaderboard directional pricing, corporate-catalyst repricing tails
- **Reconnaissance mode** — no pre-committed numerical GO thresholds; pre-commitment is on reporting structure, with a four-state verdict (GO / KILL / INCONCLUSIVE / EXPLORATORY POSITIVE)
- Day 2 retrospective calibration surfaced an asymmetric-bot-coverage pattern (Western labs bot-covered within hours, Chinese / peripheral labs lagged 20+ hours) that is **explicitly logged out-of-scope** to avoid HARKing
- Verdict lands Day 30

---

## Key numbers

| What | Value |
|------|-------|
| Active AI markets on Polymarket (scanned 2026-04-21) | **234** |
| 30-day volume across those markets | **~$10M** |
| Hypotheses under test | **3** (H1 latency / H2 leaderboard / H3 corporate) |
| Release-date markets in H1 | **12** |
| Leaderboard-basket candidates in H2 | **15** (sum-of-asks ≈ 1.02, tight neg-risk) |
| Corporate markets in H3 | **5** |
| Observation window | **30 days** (Days 5–29) |
| Polymarket CLOB base fees (empirically) | **0 bps** across 16 sampled markets in 6 categories |

---

## The three hypotheses (and their fair trial)

### H1 — News-to-market latency on release-date markets
Can a retail operator capture edge between when a release-date rumor/leak lands and when Polymarket reprices? Measured against 12 pre-registered release-date markets (GPT-5.5/6, DeepSeek V4, Gemini 3.5, Claude Mythos, MAI).

**Day 2 found:** lead times of ~5 hours on Western-lab news (fast) vs ~20 hours on Chinese-lab news (slow). n=3 Class-1 attributable events — too small to conclude. Verdict pending 30-day observation.

### H2 — Leaderboard directional view
Is the market's "best AI model end of April" basket (Anthropic 80% / OpenAI 19% / 13 others at 0.1-0.2%) pricing the April 30 LM Arena outcome correctly? A specific decomposed probability model gets built, disagreement ≥5pp after ÷5 adjustment flags as edge.

**Most likely to KILL** — Polymarket AI traders include AI researchers; asymmetric-information edge is rare.

### H3 — Corporate / valuation markets
Do slow-developing catalysts (SEC filings, funding rounds, CEO actions) give retail a multi-hour repricing window? 5 corporate markets monitored (OpenAI IPO, OpenAI acquired, Anthropic/OpenAI IPO order, xAI-Tesla merger, etc.).

---

## Why reconnaissance mode (not hypothesis-test mode)

The sibling [`trump-polymarket-replication`](https://github.com/sturzael/trump-polymarket-replication) ran as a strict hypothesis-test with pre-committed numerical GO thresholds. That's appropriate when you have a specific published claim to replicate (their 61.3% hit rate).

This study has no such prior — we're characterising a category, not testing a specific number. Pre-commitment is on **reporting structure** instead: what gets measured, what counts as a jump, what news sources are selectable, which attribution class (1 vs 2) each event falls into.

The integrity defences that replace numerical thresholds:
1. All observed events in pre-registered categories must appear in the Day-30 writeup
2. Metric definitions locked Day 1
3. ÷5 heuristic on edge estimates
4. Counter-memo before verdict
5. EXPLORATORY POSITIVE as a legitimate verdict state

---

## Core integrity artefacts

- [`PLAN.md`](PLAN.md) — 30-day schedule, three hypotheses, seven risks + mitigations
- [`PRE_REGISTRATION.md`](PRE_REGISTRATION.md) — exact markets / metrics / source lists, with all amendments dated and reasoned
- [`RISKS.md`](RISKS.md) — seven specific failure modes including R7 (HARKing under loose kill-gate mode)
- [`docs/day2_summary.md`](docs/day2_summary.md) — Day 2 retrospective calibration findings, including the out-of-scope asymmetric-lag observation logged for Phase 1

Each is committed to git before the observation it describes begins.

---

## Honest caveats

**What this study cannot establish:**
- Whether any AI signal is actionable at capital levels above $1k
- Whether VPS-grade latency (<100ms) changes the verdict
- Whether AI markets on venues other than Polymarket (Kalshi, Manifold) differ
- Whether non-AI categories of Polymarket markets have similar or different dynamics

**What the loose kill-gate mode costs:**
Without pre-committed numerical thresholds, the researcher's Day-30 judgment carries more integrity weight. A reviewer auditing this study should verify the five integrity commitments in [`RISKS.md`](RISKS.md) §R7 were honoured before crediting the verdict.

---

## Reproduce it yourself

Python 3.12+, standard library only. No third-party dependencies.

```bash
git clone https://github.com/sturzael/polymarket-ai-edge.git
cd polymarket-ai-edge
# Day 2 retrospective calibration
python3 day2/scan_ai_markets.py        # (when committed)
# Jump detection on hourly price history
python3 day2/detect_jumps.py           # (when committed)
```

Raw data is gitignored; all pulls regenerate from public Polymarket Gamma / CLOB endpoints.

---

## Related studies

This is part of a three-repo portfolio on solo-operator trading research:

| Repo | Question | Verdict |
|------|----------|---------|
| [`polymarket-edge-research`](https://github.com/sturzael/polymarket-edge-research) | Does retail edge exist on Polymarket at $1k bankroll across 10 candidate strategies? | KILL (all 10 strategies falsified) + durable tooling |
| [`trump-polymarket-replication`](https://github.com/sturzael/trump-polymarket-replication) | Does the sstklen/trump-code signal set (claimed 61.3% hit rate on S&P from Trump tweets) translate to Polymarket political binaries? | KILL — 0 cells cleared the 7-gate pre-registered test |
| **`polymarket-ai-edge`** (this repo) | Is there retail edge on Polymarket's AI markets? | Pre-registration complete; forward observation not yet begun |

All three share methodology DNA: pre-registration before data access, ÷5 heuristic on edge estimates, counter-memo before verdict, git log as audit trail.

---

## Citation

```
Sturzaker, E. (2026). Polymarket AI-Markets Edge Investigation:
A 30-Day Pre-Registered Reconnaissance.
GitHub: sturzael/polymarket-ai-edge
```

## Disclosure

No capital is deployed at any phase. All observation data comes from public Polymarket APIs (Gamma, CLOB) and public news sources listed in [`PRE_REGISTRATION.md`](PRE_REGISTRATION.md) §1. Operator profile, thresholds, and non-goals are stated in advance and will not be revised post-hoc.

Independent audit of the Day-30 verdict should begin by verifying the five integrity commitments in [`RISKS.md`](RISKS.md) §R7 were honoured.

**Star ⭐ this repo if you want to follow the Day-30 verdict when it lands.**
