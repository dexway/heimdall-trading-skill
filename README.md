# Heimdall Trading Skill

A free Claude skill that reads a chart from the top down and shows, rule by rule, which conditions of a setup are met and which are missing.

Covers market structure, order blocks, liquidity, imbalances, the 50 EMA bias and a WAIT-STATE guardrail.

## Install

Paste this link into Claude Code and tell it to install the skill, or run:

```bash
git clone https://github.com/dexway/heimdall-trading-skill.git
cp -r heimdall-trading-skill/heimdall-trading ~/.claude/skills/
```

## Use it

Share a chart or describe one, and ask Claude to read it with the Heimdall rules.

Want it live on Deriv markets? Try the app: https://heimdall-quant.vercel.app

## Disclaimer

Educational only, not financial advice. It describes charts against rules and never tells you to buy or sell. Trading carries a real risk of loss, and no rule here is proven profitable.
