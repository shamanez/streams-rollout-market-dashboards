# streams-rollout-market — live dashboards

This repo is a **read-only snapshot** of the live dashboards produced by
[streams-rollout-market](https://github.com/shamanez/streams-rollout-market).
The source code (Pydantic contracts, OPBC, validators, LiveStore,
worker SDK, observatory labs, CLIs, tests) lives in the private
`streams-rollout-market` repo. This repo holds only the rendered HTML
+ JSON dashboards so they can be browsed publicly without exposing
the implementation.

**Browse the dashboards:**
[https://shamanez.github.io/streams-rollout-market-dashboards/](https://shamanez.github.io/streams-rollout-market-dashboards/)

## What's here

| dashboard | what it measures |
|---|---|
| Endpoint identity-gap | Free-tier API probe coverage matrix — which providers expose token IDs, logprobs, top_logprobs, seed_supported. |
| Dense mismatch | Per-`(rollout_engine, trainer_engine)` ESS / max\|log_ratio\| over Qwen3-32B response tokens. 8 prompts × 4 engine cells. |
| MoE router | Qwen3-30B-A3B router trace: per-`(token, layer)` top-1 flip rate and top-k set disagreement, FP8 vs bf16. |
| Agent trajectory | Multi-step tool-using Qwen3-32B runs across 4 engine cells: first-divergence step, tool-call Jaccard, final-answer match rate. |
| Marketplace simulation | Synthetic 7-worker simulation (honest / noisy / stale / 4 toxic) driving the full validators + OPBC + LiveStore + audit stack. |

Each dashboard is a self-contained HTML page with inline CSS and no
JavaScript. The `*.json` sibling holds the raw aggregate data the
HTML was rendered from.

## How to regenerate

In the private source repo:

```bash
python scripts/live/publish_dashboards.py --out-dir /path/to/this/repo
```

then `git commit && git push`. GitHub Pages picks up the new snapshot
within ~30 seconds.
