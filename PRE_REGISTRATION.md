# Pre-Registration — Polymarket AI-Markets Edge Investigation, Phase 0

**Commit timestamp = pre-observation baseline.** This file is append-only. Amendments are dated subsections below, not edits to original sections. Pre-registration is the integrity anchor for a reconnaissance-mode experiment without numerical GO thresholds; see `PLAN.md` for why.

**Snapshot source:** Polymarket Gamma API and event-level state queried 2026-04-21. Markets may change status (endDate extensions, closure, re-listings) during the observation window; any change is logged in a dated amendment.

---

## 1. H1 — Release-date markets under observation

Monitored hourly via CLOB `/prices-history?market=<token_id>&fidelity=60`. Every hourly price jump of ≥ 15 percentage points gets logged to the event log; news-correlation research performed within 24 hours of the jump.

| # | Slug | conditionId | Initial ask | endDate |
|---|------|-------------|------------:|---------|
| 1 | `will-gpt-5pt5-be-released-on-april-23-2026` | `0x704a7b123805bc24337695f260c664effc8135bfb294336c6415958ab9ceeb77` | 0.78 | 2026-04-30 |
| 2 | `will-gpt-5pt5-be-released-on-april-22-2026` | `0x6213a4e3c9657d2caf897624d50dd1540d39664b081b5fce96be0e9b195bdf69` | 0.029 | 2026-04-30 |
| 3 | `will-gpt-5pt5-be-released-on-april-30-2026` | `0xfc2542558e284aca60f3dc3e2ee649d6c034238489dcfd3c8d071cef71f426d6` | 0.124 | 2026-04-30 |
| 4 | `will-gpt-5pt5-be-released-on-april-21-2026` | `0x921c8b1ad76c45ae7b791e0b14e5a957a3743a4616fc3934bb428e551ac73cf0` | 0.037 | 2026-04-30 |
| 5 | `will-gpt-5pt5-be-released-on-april-20-2026` | `0x2b8c2cb33a898e967de7b6c12aa5d1f545b8cf6888959e6160ba7ac879c602ed` | 0.003 | 2026-04-30 |
| 6 | `will-gpt-5pt5-be-released-on-april-28-2026` | `0x1a85044d2ff844e7ed4ebe4ac51da2914519e6699cc8558a405d071f9dd6f6e6` | 0.023 | 2026-04-30 |
| 7 | `will-gpt-5pt5-be-released-on-april-29-2026` | `0x80a944852beb37777984618be0468a778bae60fd0a528f7263baba6153c9f102` | 0.028 | 2026-04-30 |
| 8 | `will-gpt-6-be-released` | `0x0ea8005efbc460378340a2f28a6d97b0d1d9d9d7fba4d16f529b8a415dca77a2` | 0.71 | 2026-07-31 |
| 9 | `gemini-3pt5-released-by-may-31` | `0x009cb79c526eff4af80e0e568c648a165a837c0417f4e1de3cde02bfc4a3ab42` | 0.088 | 2026-06-30 |
| 10 | `deepseek-v4-released-by-may-15` | `0x3be93b488f2a9b2480dd5d5e9a04ca0b37fd2a6b20664ef2b1584d75c5a1d93e` | 0.9 | 2026-05-15 |
| 11 | `will-a-claude-mythos-model-be-released-by-june-30-2026-684` | `0xcfd48c874ae1760c1ec3c87a8c46c221af6a4f2be3b56618ba261bef4c92e768` | 0.23 | 2026-04-30 |
| 12 | `will-a-new-mai-model-be-released-by-april-30-2026` | `0x54e36797c1b460ffada25fb66ef39d591333a3d2adc2dc1a3cb0914a088e6901` | 0.38 | 2026-06-30 |

### Pre-committed reporting for H1 (locked)

For every observed price jump ≥ 15 pp within a 60-minute window:

- Market slug + conditionId
- Jump-start UTC timestamp + price_before
- Jump-end UTC timestamp + price_after
- Magnitude (pp)
- Candidate triggering news events within ±60 min (ALL candidates logged, not just the selected one)
- Selected triggering event (if unambiguous)
- 50%-capture lead time = minutes from selected-news-timestamp to first hourly bar at which price had moved ≥ 50% of (price_after − price_before)
- 90%-capture lead time = same to 90%
- "Ambiguous" flag if multiple candidate news events are plausible
- "No-news-identified" flag if no candidate within ±60 min

Jumps marked "ambiguous" or "no-news-identified" are **included in the full reporting table** but excluded from headline median statistics.

### News sources for H1 correlation (locked Day 1)

Canonical list, in priority order:
1. Official company channels: openai.com/blog, anthropic.com/news, deepmind.google, x.ai/news, mistral.ai, huggingface.co/blog
2. Company social: @OpenAI, @AnthropicAI, @GoogleDeepMind, @xai, @mistralai
3. Leaker accounts with track record: @testingcatalog, @apples_jimmy, @Teortaxes, @kimmonismus
4. Aggregator: @alexwei_ (LiveBench), @scaling01, @reach_vb
5. Structural sources: github.com/huggingface/transformers commits, vllm-project/vllm, ollama/ollama (for feature-flag signals)
6. Baseline news: Reuters AI vertical, Bloomberg Technology, The Information

**Post-hoc adding of news sources not allowed.** If a candidate triggering event comes from a source not on this list, it may be noted in the candidate log but may not be selected as the primary driver.

---

## 2. H2 — April 2026 leaderboard basket (15 real candidates)

Parent event: `which-company-has-the-best-ai-model-end-of-april` (ticker `which-company-has-the-best-ai-model-end-of-april`). Resolution expected 2026-04-30. Neg-risk basket with 12 phantom placeholder markets excluded from this pre-registration.

| Company | Slug | conditionId | Initial ask |
|---------|------|-------------|------------:|
| Anthropic | `will-anthropic-have-the-best-ai-model-at-the-end-of-april-2026` | `0x6ac0f239c53763cc907a6707eb73d3b6a5b3308584efe37b10bad4174918377c` | 0.81 |
| OpenAI | `will-openai-have-the-best-ai-model-at-the-end-of-april-2026` | `0xf105ea1a83605540617366526881a245bd0fb586e0cfe15c1582d0d3ee579558` | 0.192 |
| xAI | `will-xai-have-the-best-ai-model-at-the-end-of-april-2026` | `0xe0c2bd9d549184bc37a80ed0494bfb0b83dc20e4a2ca695e0698062f23d73372` | 0.002 |
| Baidu | `will-baidu-have-the-best-ai-model-at-the-end-of-april-2026` | `0xb543d97766c60645f6971e1d43ee4bc4ece1c41528d97e24894c9e661ba5adf5` | 0.002 |
| Amazon | `will-amazon-have-the-best-ai-model-at-the-end-of-april-2026` | `0x82c85fd89271efb1ad356855d4ca1c2fc248e0d14c9740b628d28d9d6b0261f1` | 0.002 |
| Mistral | `will-mistral-have-the-best-ai-model-at-the-end-of-april-2026` | `0xefe76c93fb76cb82524874a321f5442bb67a586c6d04fa91856fc9506af56c06` | 0.001 |
| Meituan | `will-meituan-have-the-best-ai-model-at-the-end-of-april-2026` | `0xedcc1af0d27a8e2d59466ec26156050b11187aebc6fb02becf50ca685f5475ba` | 0.002 |
| Meta | `will-meta-have-the-best-ai-model-at-the-end-of-april-2026` | `0xc12b1659e928a5b6f620df220fba12621c87bba9a226dbed0d6cbe04510a0848` | 0.001 |
| Google | `will-google-have-the-best-ai-model-at-the-end-of-april-2026` | `0xb8683df5ebcc52d9f3577ce65667082544b368f7e3b84120aa345b31dd89d832` | 0.002 |
| Alibaba | `will-alibaba-have-the-best-ai-model-at-the-end-of-april-2026` | `0x42c86ccd2f53f6265d28e351b4e124df60a8cea3df23da8d965cdc4b401b6012` | 0.002 |
| ByteDance | `will-bytedance-have-the-best-ai-model-at-the-end-of-april-2026` | `0xa0d2521a751e1c1323af9e7c054ee2adda96adb0979bdffd7a324bb39bb64e3d` | 0.001 |
| Moonshot | `will-moonshot-have-the-best-ai-model-at-the-end-of-april-2026` | `0x415e8fe26c593799227079b0eb3abd119ddd469e4cea9e550baea01bbaf77d25` | 0.001 |
| Z-AI | `will-zai-have-the-best-ai-model-at-the-end-of-april-2026` | `0x191c90a6c432001b40b1e8bc4dd7af0abc857faa6326f8ea283bd8daa35e6148` | 0.002 |
| DeepSeek | `will-deepseek-have-the-best-ai-model-at-the-end-of-april-2026` | `0x93a144757495d68c867022424152e77ed5ff20a473cb05e16960de2b88300bd8` | 0.002 |
| Microsoft | `will-microsoft-have-the-best-ai-model-at-the-end-of-april-2026` | `0xe672a023070559745290e22390b0c27a6a38ae0ddd07b082af901795ffd94466` | 0.001 |

Sum of initial asks: ≈ 1.020. Tight neg-risk basket.

### Pre-committed reporting for H2 (locked)

- Weekly snapshot table of each market's bid/ask/mid price
- Researcher's modelled probability (built Day 3; updated weekly as new information arrives)
- Model-vs-market delta per candidate, per week
- ÷5 heuristic applied to max observed delta before any interpretive claim of "edge"
- Resolution outcome (which company was #1 on April 30)
- Explicit note on any H2 model parameter that relied on information not trivially available to an attentive Polymarket AI trader

### H2 model-build rules (locked Day 3)

- Must be a probability decomposition into named sub-events (release probabilities × leadership probabilities)
- All sub-event probabilities drawn from public information only
- Sources used recorded in the model's markdown
- Sensitivity analysis required: report probability-ranges for key parameters
- The model is for illustration; no capital is committed regardless of what it says

---

## 3. H3 — Corporate / valuation markets under observation

Five markets with 6-20 month resolution horizons and slow-developing catalysts.

| # | Slug | conditionId | Initial ask | endDate |
|---|------|-------------|------------:|---------|
| 1 | `will-openai-ipo-by-december-31-2026` | `0x66f5b8203ee1c36b993af623fd7f9ef7271dd87b3aebf6df508048ad4b563432` | 0.36 | — |
| 2 | `will-openai-be-acquired-before-2027-859` | `0x8880cafadc71125e18f7c8c768475d589df7b7ca514270fc37656aa0a8dbfbd1` | 0.075 | 2026-12-31 |
| 3 | `openai-ipo-closing-market-cap-above-800b` | `0x48dc4d6bae89b6401210186b94db6618050505c520b1ead26a5806b978fd0e6c` | 0.79 | 2027-12-31 |
| 4 | `will-anthropic-or-openai-ipo-first` | `0xc289a877bc155123069739b21d690b3e8dc220b98f6ae3924468bbcbdfaf98dc` | 0.61 | 2027-12-31 |
| 5 | `tesla-and-xai-merger-officially-announced-by-june-30` | `0xc49487996b94574c24dfc6250a0dfe01815485c679784822fee6a359022cae0f` | 0.06 | 2026-06-30 |

### Pre-committed reporting for H3 (locked)

For each catalyst observed during the window:

- Catalyst type (SEC filing, reputable-source reporting, official company announcement, leaked cap-table)
- Catalyst first-public-availability UTC timestamp + source
- Market price at catalyst timestamp T+0 (closest hourly bar)
- Market price at T+1h, T+6h, T+24h, T+72h
- "Moved before catalyst public" flag if market showed significant movement in the 24 hours pre-catalyst
- Baseline drift rate per market (computed from non-catalyst weeks) to distinguish news-driven movement from noise

### Catalyst source registry (locked Day 4)

- SEC EDGAR filings for OpenAI, Anthropic, xAI, related entities
- Reputable corporate reporting outlets: WSJ, FT, Bloomberg, The Information, Reuters, Axios
- Official company blogs and press releases
- Credible leaked-information channels: The Information (private company reporting), Bloomberg BNN Intel

Post-hoc adding of catalyst sources not allowed. If a catalyst comes from a source not on this list, it may be noted in the log but does not qualify as an "official source timestamp."

---

## 4. Non-goals (locked)

1. No capital deployed at any phase. Paper trades only.
2. No sub-100ms execution infrastructure. Operator profile locked.
3. No building a news-event classifier. Manual human judgement for news correlation.
4. No expansion beyond Polymarket AI markets. No Kalshi cross-venue work in this repo.
5. No trump-code rule import. This experiment has no rule set.
6. No live trading during the 30-day observation window.
7. No retroactive market additions. The lists above are frozen until Day-30 verdict.
8. No post-hoc threshold movement. The integrity claim rests on reporting-structure commitment, not on pre-committed thresholds (by design).

---

## 5. Integrity commitments (carry the integrity weight because no numerical thresholds exist)

1. **All observed events in pre-registered reporting categories appear in the Day-30 writeup.** No selective reporting. If 9 news-identified jumps happened, all 9 appear with the same columns.
2. **Metric definitions above are fixed in advance and will not be redefined.**
3. **The ÷5 heuristic is applied before any edge estimate enters a GO recommendation.**
4. **Counter-memo written before verdict.** Day 30 counter-memo argues from the same data that both false-GO and false-KILL are plausible.
5. **EXPLORATORY POSITIVE is a legitimate verdict.** Research finding "worth further investigation, not yet actionable" is a real result.
6. **Git log is the audit trail.** Pre-registration, observation logs, counter-memo, and verdict are each separate commits with timestamps.
7. **Amendment policy: this file is append-only.** Corrections go in dated amendment subsections below, not edits to sections above.

---

## 6. Observation window

**Start:** Day 5 of the plan (after infrastructure deployment).
**End:** Day 29 (inclusive). Day 30 is verdict.

Calendar: pre-registration commits 2026-04-21; observation window roughly 2026-04-26 through 2026-05-20, verdict 2026-05-21. Exact dates shift if any earlier day overruns.

---

## Amendments

(None yet. Each amendment is a dated subsection appended below, referencing the section it modifies.)
