# Explain Like I'm Five

← [Back to the technical version](../README.md)

---

## What is this?

There's a website called **Polymarket** where people bet real money on whether things will happen in the future. You buy a "yes" or "no" ticket for somewhere between 1¢ and 99¢. If you're right, your ticket turns into $1. If you're wrong, it turns into $0. The ticket's price tells you how likely people think it is — a 30¢ "yes" ticket means people think there's a 30% chance.

Polymarket has lots of different types of bets. This project focuses on a specific slice: **AI-themed markets.** Things like:

- "Will OpenAI release GPT-6 before July?"
- "Which company will have the best AI model at the end of April?"
- "Will Anthropic file for IPO this year?"
- "Will xAI acquire Tesla's neural-net division?"

This category is the fastest-growing on Polymarket right now. Around **$10 million in bets** have been placed across **234 different AI markets** in a single month. That's a lot of money moving around on questions about robots.

## What are we trying to figure out?

**Can a regular person — a laptop, $1,000, sitting at home — find places where Polymarket's AI markets are wrong, and make money by betting against the wrong price?**

We're not asking "who will win?" We're asking "are the people setting the prices on Polymarket sometimes slow, sloppy, or mistaken in ways you could bet against?"

There are three specific places we're looking. They're the three most plausible spots where a human who pays attention might still beat the computers.

## The three places we're looking

### 1. "Breaking news" markets

When a big AI company (OpenAI, Anthropic, Google, DeepSeek, Meta) releases a new model or drops a hint about one, the market has to react. Does it react instantly? Or does it take a few hours?

If there's a delay, a person who reads the news fast could theoretically buy the right ticket before the price catches up.

**What we've seen so far:** Western-lab news (OpenAI, Anthropic, Google) gets priced in fast — about 5 hours on average. But **Chinese or smaller-lab news** (DeepSeek, Mistral, smaller players) takes more like **20 hours** to get priced in. That's interesting. But we're not drawing conclusions from it yet — we only have 3 observations, which is way too few. It could easily be noise.

### 2. "Who will be #1?" markets

There's a leaderboard called LM Arena that ranks AI models by how well they do in head-to-head comparisons. Polymarket has bets on "who will be #1 at the end of the month."

Right now Polymarket thinks Anthropic (Claude) is an 80% favorite, OpenAI is 19%, and the 13 other companies combined are about 1%.

**Is that right?** We're going to build our own model of what the probabilities should be based on the actual current leaderboard, do the math carefully, and see if the market is off by more than 5 percentage points anywhere. If it is, we might have an edge. If it isn't, the market is already smarter than us.

### 3. "Corporate news" markets

Things like "Will OpenAI IPO this year?" or "Will Anthropic be acquired before 2027?" These are bets that take months to resolve and only move when there's a specific announcement — a funding round, a regulatory filing, a CEO leaving.

The theory: announcements happen slowly. A regular filing gets posted, spreads through financial Twitter, then through prediction markets. A careful person might catch the move before it finishes.

## Why we're doing it this carefully

The boring part of research is setting the rules **before** you look at the results. Otherwise it's really easy to accidentally fool yourself. You go: "hey that Chinese-model-news thing looks interesting!" and suddenly the thing you didn't originally plan to test has become your headline finding. That's called "p-hacking" or "HARKing" and it's how people end up believing in things that aren't real.

So we wrote down — before we looked — **exactly what we'd measure, what counts as a hit vs miss, and what result would count as a win vs a loss.** Every observation we make has to fit into those pre-written rules.

This is also why this project is labeled **"reconnaissance"** instead of "test." We don't have a specific claim we're disproving — like the [sibling project](https://github.com/sturzael/trump-polymarket-replication) which disproved a specific viral "61% hit rate" claim about Trump tweets. Here we're just trying to characterize a whole category to see if there's edge anywhere, so the rules are about what counts as good evidence, not specific pass/fail numbers.

## What's happened so far?

- **Day 1:** Wrote down the plan. Locked in the three hypotheses, the news sources, the pre-registered markets.
- **Day 2:** Pulled a historical snapshot of how these markets have behaved. Spotted the Western-vs-Chinese latency pattern mentioned above, but — importantly — logged it as "out of scope" so it doesn't accidentally become the punchline.
- **Days 5–30:** We wait. Every time something happens in our pre-registered categories (a model releases, a corporate news hits, the leaderboard shifts), we note what the market was priced at, what actually happened, and what the gap was.

**Verdict lands on Day 30.** Not earlier. The answer is one of four:

- **GO:** we found real edge and we'll deploy capital to test it for real
- **KILL:** no edge, category is efficient, move on
- **INCONCLUSIVE:** we didn't get enough events to tell — run again later
- **EXPLORATORY POSITIVE:** a signal that's interesting but wasn't in the original hypotheses — logged, not acted on

Which one lands depends on the data. We genuinely don't know yet.

## What's the big-picture lesson?

Three things, most of which apply to life beyond prediction markets:

1. **The hard part of research is honesty, not cleverness.** It's easy to look at data and find a story. It's hard to look at data and find *the* story — the one that would have been there even if you weren't hoping to find it.

2. **Publishing in advance beats publishing in retrospect.** This whole repo started with a pre-registration doc that listed every measurement we'd make. When the results come in, we can't pretend we were testing something different. That constraint is a feature, not a bug.

3. **"AI markets" is a neat place to look because the people betting there are also the people building AI.** Unlike sports betting where the professionals are fast-executing bots, these markets are partly populated by AI researchers who have genuine information. That makes edges rarer — but if there are any, it's likely in the specific corners where information asymmetries still exist (like news traveling slowly from non-Western labs).

## Related projects

- **[polymarket-edge-research](https://github.com/sturzael/polymarket-edge-research)** — The parent project. Tested 10 strategies, found 9 didn't work, found 1 that might. The work that made this reconnaissance possible.
- **[trump-polymarket-replication](https://github.com/sturzael/trump-polymarket-replication)** — Sibling study. Tested whether the viral "Trump tweets predict the S&P" claim translates into tradeable edge on Polymarket political markets. Verdict: KILL.

---

← [Back to the technical version](../README.md)
