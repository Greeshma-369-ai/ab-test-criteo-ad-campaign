# Large-Scale A/B Test Analysis: Digital Advertising Campaign

## Objective
Measure whether an online ad campaign causally increased website visits and conversions, and whether the experiment was trustworthy and adequately powered.

## Data
Criteo Uplift Prediction Dataset (10% random sample, 1,397,959 users; 85% treatment / 15% control).
Citation: Diemert, Betlei, Renaudin & Amini, "A Large Scale Benchmark for Uplift Modeling", AdKDD 2018 Workshop (KDD 2018).
The data is not included here; the notebook shows how to download it.

## Methods
- Experiment validity: sample ratio mismatch (chi-square), covariate balance (standardized mean difference), exposure check
- Effect estimation: two-proportion z-test, 95% confidence intervals, bootstrap CI for relative lift
- Power analysis: minimum detectable effect, sample size requirements, power curve, 85/15 vs. 50/50 allocation
- Effect on exposed users: CACE (Wald estimator)

## Key Results
| Metric | Control | Treatment | Relative lift | 95% bootstrap CI |
|---|---|---|---|---|
| Conversion | 0.194% | 0.310% | +59.7% | +44.8% to +77.5% |
| Visit | 3.796% | 4.850% | +27.8% | +24.9% to +30.7% |

- No sample ratio mismatch (treatment share 85.00%, p = 0.968); all features balanced (max |SMD| = 0.048)
- Minimum detectable effect: 15.05%; the observed lift is about 4x the MDE
- Only 3.61% of treated users were exposed; estimated effect on exposed users: +3.21 pp conversion (indicative)

![Conversion rate by group](<Conversion Rate by Group (95% CI).png>)
![Bootstrap distribution of relative lift](<BOOTSTRAP_FULL_NAME.png>)
![Covariate balance](<COVARIATE_FULL_NAME.png>)
![Power curve](<Power curve.png>)

## Recommendation
Roll out the campaign and improve ad reach, since only 3.6% of targeted users actually saw the ad. Next step: uplift modeling to identify which users respond most.

## Limitations
Results are intent-to-treat; the CACE estimate relies on additional assumptions. Features are anonymized. Conversions are rare (407 in control), which widens the conversion CI.

## Tools
Python (pandas, NumPy, SciPy, statsmodels, Matplotlib), Jupyter Notebook
