# Controlled MARL Experiment Study on Mava

This branch presents my course-project study built on top of the [Mava](https://github.com/instadeepai/Mava) multi-agent reinforcement learning framework. I used Mava as the experimental platform and focused on a controlled comparison of PPO-family methods rather than proposing a new algorithm.

## Project at a glance

| Item | Scope |
| --- | --- |
| Main environment | `rware` |
| Main algorithms | `ff_ippo`, `ff_mappo` |
| Main scenarios | `tiny-2ag`, `tiny-4ag`, `tiny-4ag-easy`, `small-4ag` |
| Main seed protocol | `1..5` |
| Follow-ups | recurrent variants, learning-rate sensitivity, `lbf` extension, exploratory budget sweep |

## Research question

How do `ff_ippo` and `ff_mappo` behave on cooperative warehouse-style tasks when scenario difficulty, random seed, selected hyperparameters, and model recurrence are controlled?

## Main takeaway

The main five-seed `rware` study did **not** reveal a stable winner between `ff_ippo` and `ff_mappo`: both methods stayed at zero mean final return across the selected scenarios under the tested informative budget. Follow-up analyses showed the same floor-level pattern for recurrent variants, while the `lbf` extension produced non-zero returns and confirmed that the experimental pipeline could capture learning signal in a second environment family.

![Final returns across the main rware scenarios](analysis/figures/final_return__rware__all_scenarios__informative.png)

## Headline findings

| Result block | Key takeaway |
| --- | --- |
| Main `rware` core | All final means stayed at `0` under the five-seed informative budget. |
| Recurrent follow-up | Recurrent variants did not break the floor-level pattern on representative `rware` scenarios. |
| Sensitivity follow-up | Lower `actor_lr` produced some small positives, but the main conclusion did not change. |
| `lbf` extension | The same pipeline produced positive final returns in a second environment family. |
| Threshold sweep | No stable `rware` budget threshold was identified up to `51200` timesteps. |

## Selected follow-up results

### Recurrence

![Feed-forward versus recurrent comparison](analysis/figures/feedforward_vs_recurrent__rware__tiny-2ag_small-4ag__informative.png)

### Learning-rate sensitivity

![Actor learning-rate sensitivity](analysis/figures/sensitivity_actorlr__ff_ippo__rware.png)

### Exploratory budget sweep

![Exploratory threshold sweep](analysis/figures/threshold_sweep__rware__tiny-2ag_small-4ag.png)

## What this project demonstrates

- I designed a repeatable MARL experiment pipeline with matched seeds, scenarios, budgets, and evaluation settings.
- I compared feed-forward and recurrent PPO-family methods under controlled conditions.
- I treated negative findings as valid evidence instead of forcing a winner from weak signals.
- I separated the main five-seed study from weaker exploratory follow-ups to avoid overclaiming.

## Where to read more

- [Detailed analysis report](PROJECT_ANALYSIS.md)
- [Methodology and validity boundaries](analysis/methodology.md)
- [Selected tables](analysis/tables/)
- [Selected figures](analysis/figures/)

## Upstream framework

This study is built on top of InstaDeep's Mava repository, a JAX-based framework for distributed multi-agent reinforcement learning. The upstream framework source remains available at the original Mava project; this branch is intentionally focused on my experiment design and selected results.
