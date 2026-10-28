# TriPPA Experimental Results

This repository provides recording-level scores and evaluation metrics for the comparison and ablation experiments in **TriPPA: Reference-conditioned three-branch modeling for Mandarin pronunciation assessment**. It covers accuracy, fluency, and prosody scoring across five OMPAL speaker combinations.

## Files

| File | Contents | Rows, excluding header |
| --- | --- | --- |
| `recording_level_scores.csv` | Target and predicted scores for each model, speaker combination, and test recording | 14,768 |
| `evaluation_metrics_by_combination.csv` | PCC, MSE, and MAE for each model, combination, evaluation scope, and task | 480 |

Both CSV files use UTF-8 encoding and include a header row.

## Recording-Level Scores

Each row represents one model/configuration, speaker combination, and recording, with scores for all three tasks.

| Field | Description |
| --- | --- |
| `model_id` | Model or ablation identifier; see the mapping below |
| `combination` | Speaker combination index: 1, 2, 3, 4, or 5 |
| `recording_id` | Reassigned recording identifier, consistent across models and combinations |
| `speaker_type` | `learner` or `native` |
| `target_accuracy` | Human-rated target score for accuracy |
| `prediction_accuracy` | Predicted accuracy score |
| `target_fluency` | Human-rated target score for fluency |
| `prediction_fluency` | Predicted fluency score |
| `target_prosody` | Human-rated target score for prosody |
| `prediction_prosody` | Predicted prosody score |

Scores are expressed on the original 1-5 rating scale. The files retain the numerical precision of the stored targets and model outputs.

## Evaluation Metrics

Each row represents one model/configuration, speaker combination, evaluation scope, and task.

| Field | Description |
| --- | --- |
| `model_id` | Model or ablation identifier |
| `scope` | `all_test_recordings`: all test recordings; `learner_subset`: learner recordings only |
| `combination` | Speaker combination index, from 1 to 5 |
| `task` | `accuracy`, `fluency`, or `prosody` |
| `n_recording_occurrences` | Number of recordings evaluated within the specified combination and scope |
| `PCC` | Pearson correlation coefficient; higher is better |
| `MSE` | Mean squared error; lower is better |
| `MAE` | Mean absolute error; lower is better |

MSE and MAE are calculated on the original 1-5 rating scale.

## Model Identifiers

| `model_id` | Model or configuration in the manuscript |
| --- | --- |
| `ompal_blstm` | OMPAL-BLSTM |
| `multipa` | MultiPA |
| `gopt` | GOPT |
| `gopt_suprasegmental_wl` | 11 Feat. (LN) + WL |
| `hipama` | HiPAMA |
| `hiertfr` | HierTFR |
| `hia` | HIA |
| `hmamba` | HMamba |
| `hiercb` | Adapted HierCB scoring backbone without the ConPCO training constraint |
| `trippa` | Full TriPPA model |
| `shared_local_path` | Shared Local Path |
| `without_film` | w/o FiLM |
| `standard_film` | Standard FiLM |
| `without_local_prosodic_residual` | w/o LPR: without the local prosodic residual |
| `without_global_statistics` | w/o GS: without global statistics |
| `without_both` | w/o (LPR + GS): without both components |

## Using the Results

For combination-specific results, filter the metrics file by `model_id`, `scope`, `combination`, and `task`.

For the manuscript's five-combination averages, hold the model, scope, and task fixed, then take the equally weighted arithmetic mean of each metric across the five combinations. Round the resulting values to the precision shown in the manuscript tables.

To recompute a combination-specific metric, filter the scores file by model and combination. For the learner subset, additionally select `speaker_type=learner`. Calculate the metric using the relevant `target_*` and `prediction_*` columns.

The results cover 16 models/configurations and 712 distinct test recordings. Each scores-file row is indexed by model, combination, and recording. Recordings can appear in multiple speaker combinations. The number of test recordings per model is shown below.

| Combination | All test recordings per model | Learner recordings per model |
| --- | --- | --- |
| 1 | 193 | 164 |
| 2 | 160 | 131 |
| 3 | 193 | 164 |
| 4 | 193 | 164 |
| 5 | 184 | 164 |

## Data Source and License

Target scores originate from the human annotations of the OMPAL corpus. Predicted scores were generated in the experiments reported in this study. The original corpus and its license are available from the official repository: <https://github.com/phantomhsieh/OMPAL-corpus>.

The data files and documentation are shared under the Creative Commons Attribution 4.0 International (CC BY 4.0) license; see [LICENSE](LICENSE). OMPAL is also distributed under CC BY 4.0. When reusing these results, please cite this repository and acknowledge the OMPAL corpus and its source publication.

OMPAL reference: Hsieh et al., OMPAL, Interspeech 2025, pp. 2415-2419, <https://doi.org/10.21437/Interspeech.2025-983>.

Results and documentation prepared by Wenzhe Liu, Xinjiang University.
