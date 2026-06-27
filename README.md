# Vanguard UX Experiment: Do Clients Complete More Easily?

With a closer look at high-balance clients.

## Project Overview

This project analyzes Vanguard's digital process redesign using A/B testing. The goal is to understand whether the new user interface helped clients complete the online process more easily, and whether the improvement was strong enough to justify a full rollout.

The analysis also focuses on high-balance clients, because this segment is especially important for Vanguard and may need a smoother, more reliable digital experience.

## Research Question

Does Vanguard's redesigned UI increase completion rates compared with the old UI, especially for high-balance clients, and is the improvement strong enough to justify rollout?

## Hypotheses

1. The Test UI will produce a higher completion rate than the Control UI.
2. The Test UI will meet Vanguard's 5% minimum lift requirement.
3. High-balance clients will complete more often in the Test UI than in the Control UI.

## Dataset

The analysis uses cleaned and merged Vanguard experiment data containing client demographics, web process activity, experiment group assignment, and segment flags.

Final cleaned dataset:

- `vanguard_master_cleaned.csv`

Key fields include:

- `client_id`
- `visit_id`
- `process_step`
- `date_time`
- `Variation`
- `clnt_age`
- `clnt_tenure_yr`
- `gendr`
- `bal`
- `is_high_balance`
- `is_multi_account`

The cleaned dataset contains:

- 321,207 process-event rows
- 50,488 unique clients

## Tools Used

- Python
- Pandas
- SciPy
- Statsmodels
- Jupyter Notebook
- Tableau

## Repository Structure

| File | Description |
| --- | --- |
| `phase1_data_cleaning_monika.ipynb` | Data cleaning, merging, and segment creation |
| `iffah_demographics_eda.ipynb` | Phase 1 demographic analysis |
| `iffah_phase2_time_abandonment.ipynb` | Phase 2 time-spent and high-balance abandonment analysis |
| `iffah_phase3&4_hypothesis_testing.ipynb` | Phase 3 hypothesis testing and Phase 4 evaluation notes |
| `vanguard_master_cleaned.csv` | Final cleaned dataset used for analysis and Tableau |

## Methodology

### Phase 1: Data Cleaning and Demographic Analysis

The raw datasets were merged into one cleaned master dataset. New segment columns were created to identify high-balance clients and multi-account clients.

For demographic analysis, duplicate client records were removed so each client was counted once.

Key demographic findings:

- Average client age: 47.32 years
- Average client tenure: 12.03 years
- Gender split was relatively balanced
- High-balance clients represented 22.98% of unique clients
- Multi-account clients represented 21.32% of unique clients

### Phase 2: Time Spent and High-Balance Abandonment

Average time spent was calculated by measuring the time between each process step within the same visit.

Average time spent by step:

| Step | Average Time |
| --- | ---: |
| Start | 61.60 seconds |
| Step 1 | 56.23 seconds |
| Step 2 | 89.97 seconds |
| Step 3 | 131.94 seconds |
| Confirm | 216.47 seconds |

For high-balance clients who abandoned the process, the last recorded step was used as the abandonment step.

High-balance abandonment points:

| Step | Share of Abandoned High-Balance Visits |
| --- | ---: |
| Start | 59.72% |
| Step 1 | 20.90% |
| Step 3 | 12.04% |
| Step 2 | 7.34% |

The main friction point was the start of the process.

### Phase 3: Hypothesis Testing

High-balance completion was compared between the Test and Control groups using a two-proportion Z-test.

High-balance completion rates:

| Group | Completion Rate |
| --- | ---: |
| Control | 66.76% |
| Test | 70.50% |

The Z-test result was statistically significant:

- Z-statistic: 4.34
- P-value: 0.000014

This means the Test UI improved completion for high-balance clients and did not create hidden performance issues for this valuable segment.

An additional tenure hypothesis test was also performed. The result showed no statistically significant difference in average tenure between Test and Control groups, supporting the idea that the experiment groups were reasonably balanced by tenure.

### Phase 4: Experiment Evaluation

The experiment duration was approximately three months, which was sufficient for an initial evaluation because the dataset contained a large number of clients and process events.

However, a longer monitoring period or follow-up test would help confirm whether the results remain stable after users become more familiar with the redesigned UI.

Additional data that would improve future analysis:

- Device type
- Browser type
- Error type
- Loading time
- Click count
- Return visits
- Help or FAQ usage
- Exit survey reason

These fields would help Vanguard understand whether start-step friction is caused by technical issues, user confusion, device limitations, or process design.

## Tableau Dashboard

The Tableau presentation visualizes:

- Demographic balance between Test and Control groups
- Overall completion rates
- High-balance completion rates
- Error volume by process step
- High-balance funnel and friction points
- Business hurdle comparison against Vanguard's 5% lift target

## Key Findings

- The redesigned UI improved completion rates overall.
- High-balance clients also completed more often in the Test group than in the Control group.
- The improvement was statistically significant, but the overall lift did not meet Vanguard's 5% business hurdle.
- The main remaining friction point was the start step, where errors and early drop-off were highest.
- The issue is not a full-journey failure. It is a concentrated early-stage friction point.

## Final Recommendation

Vanguard should not fully roll back to the old UI, because the redesigned UI improves completion overall and for high-balance clients.

However, Vanguard should also avoid a full rollout immediately because the improvement did not meet the 5% business hurdle and the start step still shows friction.

Recommended next steps:

1. Fix start-step technical issues.
2. Add simple automated recovery messages.
3. Continue with a limited rollout.
4. Collect more detailed error and device data.
5. Rerun the A/B test in 3-6 months.

This approach protects high-value clients while staying aligned with Vanguard's scalable, cost-conscious investment model.

## Contributors

- Monika Sinha
- Iffah Nurahmah
