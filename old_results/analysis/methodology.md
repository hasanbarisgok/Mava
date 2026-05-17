# Methodology

## Study scope

| Component | Choice |
| --- | --- |
| Main environment family | `rware` |
| Main algorithms | `ff_ippo`, `ff_mappo` |
| Main scenarios | `tiny-2ag`, `tiny-4ag`, `tiny-4ag-easy`, `small-4ag` |
| Main seed set | `1, 2, 3, 4, 5` |
| Optional recurrent variants | `rec_ippo`, `rec_mappo` |
| Cross-environment extension | `lbf` |

## Main informative protocol

| Parameter | Value |
| --- | ---: |
| `system.num_updates` | `50` |
| `system.rollout_length` | `16` |
| `system.num_minibatches` | `1` |
| `arch.num_evaluation` | `5` |
| `arch.num_eval_episodes` | `4` |
| `arch.num_absolute_metric_eval_episodes` | `4` |
| `arch.absolute_metric` | `False` |
| `actor_lr` | `0.00025` in the core comparison |
| `critic_lr` | `0.00025` in the core comparison |

## Fairness controls

Direct algorithm comparisons kept the following aligned:

- same environment family
- same scenario definitions
- same seed set
- same total timesteps / update budget
- same evaluation schedule
- same logging settings

## Follow-up blocks

### Recurrent comparison

- algorithms: `rec_ippo`, `rec_mappo`
- representative scenarios: `tiny-2ag`, `small-4ag`
- seeds: `1..5`
- role: test whether recurrence changes the representative `rware` outcome

### Learning-rate sensitivity

- algorithm: `ff_ippo`
- scenarios: `tiny-2ag`, `small-4ag`
- `actor_lr` / `critic_lr`: `0.0001`, `0.00025`, `0.0005`
- seeds: `1..5`
- role: test whether moderate learning-rate variation changes the conclusion

### `lbf` extension

- algorithms: `ff_ippo`, `ff_mappo`
- scenarios: `8x8-2p-2f-coop`, `10x10-3p-3f`
- seeds: `1..5`
- role: provide a small second-environment check rather than a universal benchmark

### Exploratory budget-threshold sweep

- algorithms: `ff_ippo`, `ff_mappo`
- scenarios: `tiny-2ag`, `small-4ag`
- seeds: `1..3`
- updates: `50`, `200`, `800`, `3200`
- approximate timesteps: `800`, `3200`, `12800`, `51200`
- role: exploratory follow-up only; it should not be merged carelessly with the five-seed main study

## Execution context

- backend used for the recorded study: CPU
- CPU: 12th Gen Intel(R) Core(TM) i7-1260P
- GPU present: NVIDIA GeForce MX550
- RAM: 31.71 GB

## Validity boundaries

### External validity

The main claims are limited to the selected `rware` scenarios and should not be generalized to all MARL domains.

### Internal validity

The strongest direct comparisons are those in which environment, scenario, seed set, and training/evaluation settings were matched.

### Statistical validity

Five seeds are useful for a course-scale study, but still limited for detecting small differences. The threshold sweep is weaker evidence because it used only three seeds and was explicitly exploratory.

### Construct validity

Final return alone is not enough to explain learning behavior, so the study also inspected best return, late-stage averages, and learning curves where appropriate.
