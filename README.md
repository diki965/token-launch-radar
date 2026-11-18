# token-launch-radar

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/diki965/token-launch-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/diki965/token-launch-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Build the best token launch radar. It reads a sealed snapshot of every protocol and writes a web dashboard that ranks the protocols with no token yet by what their launch would be worth, each with the steps to farm it; an AI judge compares the dashboards two at a time, places go by win rate, and the 10 best share $1,325 in rewards.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input ../input/snapshot.json
```

## How it works

`main.ts` (Node 22, standard library only) reads the sealed snapshot, scores every
pre-token protocol with the model in `lib/model.ts`, and writes `board.json`, `data.js`,
the static `dashboard/` and `screenshots/` to the output directory, plus `dossier.json`
via `vendor/makefun-board.ts`.

The board covers all 40 watchlist protocols and adds the 138 clean pre-token protocols
below the $50M floor — 178 rows. Each row's implied value is
`TVL × category multiple × growth multiplier × maturity multiplier`, where the category
multiple is the median mcap/TVL of the live-token protocols in that category, shrunk
toward the global median (0.241) with 5 pseudo-observations and capped at 1.0x TVL. The
dashboard shows every multiple with the count of live comparables behind it, and a
sandbox to change the constants and re-rank in the page. Every row carries a six-step
farm plan derived from its category, chains, TVL and age, with cost and time per step.

A protocol is on the board when its record carries no token — no market cap, no
CoinGecko id, no symbol — and it is not a wrapped, staked or bridged product of a token
that already trades. The record is not proof it has none: the board says a protocol
"records no token", never that it has none.

---

<sub>Entered on [make.fun](https://make.fun/?ref=3qvyaq49&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
