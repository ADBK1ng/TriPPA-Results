# TriPPA Experimental Results

This package contains recording-level target and predicted scores from the comparison and ablation experiments reported in the TriPPA manuscript, together with evaluation metrics for each speaker combination.

## Files

| File | Contents | Rows, excluding header |
| --- | --- | --- |
| `recording_level_scores.csv` | Target and predicted scores for each model, speaker combination, and test recording | 14,768 |
| `evaluation_metrics_by_combination.csv` | PCC, MSE, and MAE for each model, combination, evaluation scope, and task | 480 |
| `README.md` | File descriptions, field definitions, model identifiers, and evaluation conventions | Not applicable |

Both CSV files use UTF-8 encoding and include a header row. This package does not contain audio, implementation code, model weights, feature caches, or the complete source data for the analysis figures.

## Recording-Level Scores

Each row represents one model/configuration, speaker combination, and recording, with scores for all three tasks.

| Field | Description |
| --- | --- |
| `model_id` | Model or ablation identifier; see the mapping below |
| `combination` | Speaker combination index: 1, 2, 3, 4, or 5 |
| `recording_id` | Pseudonymous recording identifier, consistent across models and combinations |
| `speaker_type` | `learner` or `native` |
| `target_accuracy` | Human-rated target score for accuracy |
| `prediction_accuracy` | Predicted accuracy score |
| `target_fluency` | Human-rated target score for fluency |
| `prediction_fluency` | Predicted fluency score |
| `target_prosody` | Human-rated target score for prosody |
| `prediction_prosody` | Predicted prosody score |

Scores are expressed on the original 1-5 rating scale, not the normalized 0-1 training scale. Predictions retain the original model outputs; a small number of baseline predictions fall slightly outside the rating range. Long decimal tails in target scores reflect floating-point storage rather than additional rating precision. Values have not been rounded for display.

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

MSE and MAE are calculated on the original rating scale. PCC measures the linear correlation between target and predicted scores. MSE is the mean squared prediction error, and MAE is the mean absolute prediction error.

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

These identifiers refer to the configurations evaluated in this study. They do not indicate that prediction outputs were taken directly from the original baseline publications.

## Relation to the Manuscript Tables

For combination-specific results, filter the metrics file by `model_id`, `scope`, `combination`, and `task`.

For the five-combination averages, hold the model, scope, and task fixed, then take the arithmetic mean of each metric across the five combinations. The manuscript reports equally weighted combination averages, not metrics recalculated after pooling all predictions and not averages weighted by recording counts. Round the resulting values to the precision shown in the manuscript tables; the CSV files retain higher numerical precision.

To recompute a combination-specific metric, filter the scores file by model and combination. For the learner subset, additionally select `speaker_type=learner`. Calculate the metric using the relevant `target_*` and `prediction_*` columns.

The package covers 16 models/configurations and 712 distinct test recordings. Recordings may overlap across speaker combinations; the combinations are not mutually exclusive cross-validation folds. Each recording is also evaluated by multiple models. The 14,768 rows therefore do not represent 14,768 independent recordings.

| Combination | All test recordings per model | Learner recordings per model |
| --- | --- | --- |
| 1 | 193 | 164 |
| 2 | 160 | 131 |
| 3 | 193 | 164 |
| 4 | 193 | 164 |
| 5 | 184 | 164 |

## Data Source and Sharing Scope

Target scores originate from the human annotations of the OMPAL corpus. Predicted scores were generated in the experiments reported in this study. The original corpus and its license are available from the official repository: <https://github.com/phantomhsieh/OMPAL-corpus>.

The data files and documentation in this repository are shared under the Creative Commons Attribution 4.0 International (CC BY 4.0) license; see `LICENSE`. The original OMPAL resources are also provided under CC BY 4.0. When reusing target annotations, acknowledge the OMPAL corpus and its source publication as well as this results repository. The license applies to the files included here, not to implementation code or other materials that are not distributed in this repository.

OMPAL reference: Hsieh et al., OMPAL, Interspeech 2025, pp. 2415-2419, <https://doi.org/10.21437/Interspeech.2025-983>.

Original recording identifiers have been replaced. The identifier mapping is not included. The files contain no unique speaker identifiers, recording transcripts, server information, or local filesystem paths. Pseudonymization does not guarantee anonymity because scores may potentially be linked to public corpus records.

This repository contains scoring predictions and combination-level metrics, not the complete source data for the analysis figures.

## Dataset Contributor

Wenzhe Liu, Xinjiang University. Contribution: experimental evaluation, data curation, and preparation of the results files and documentation. This dataset contributor entry is separate from the manuscript author list and does not replace the attribution to the OMPAL creators.
