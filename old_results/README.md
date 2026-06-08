# Old results (previous CPU study)

This folder preserves the artifacts of the earlier `analysis-report` study before the experiments are redone with a real training budget on Colab Pro.

## What is here

- `PROJECT_ANALYSIS.md` — written report of the previous study.
- `analysis/` — curated figures and CSV tables from the previous runs.
- `ai_content/` — raw logs, experiment registry, and processed intermediate files (gitignored, local-only).
- `outputs/` — Hydra working directories from the previous runs (gitignored, local-only).
- `results/` — Sacred / tensorboard outputs from the previous runs (gitignored, local-only).

## Why it is here, not deleted

The previous study ran every PPO experiment with `num_envs=1`, `rollout_length=16`, `num_updates=50` → only **800 environment steps** per run, which is far below the budget needed for RWARE PPO to produce a learning signal. The numerical results are therefore not informative as a comparison between IPPO and MAPPO. They are kept for two reasons:

1. The research questions, experimental layout, scenarios, seed protocol, and analysis structure are still useful as a starting point.
2. The new GPU study (see `experiments/` at the repository root) can be compared against the old runs to show the effect of the larger training budget.

## Do not re-use the numbers in `analysis/tables/` as study results

Treat the old tables as a record of a smoke-budget pipeline, not as evidence about algorithm behavior.
