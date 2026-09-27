# Large-Scale A/B Test Analysis: Digital Advertising Campaign

## Objective
Measure whether an online ad campaign causally increased website visits and conversions, and check whether the experiment was trustworthy and adequately powered.

## Data
Criteo Uplift Prediction Dataset: a 10% random sample of **1,397,959 users** (85% treatment / 15% control).

**Citation:** Diemert, Betlei, Renaudin & Amini, "A Large Scale Benchmark for Uplift Modeling", AdKDD 2018 Workshop (KDD 2018).

The data is not included in this repository due to its size and license; the notebook shows how to download it.

## Methods
- **Experiment validity:** sample ratio mismatch (chi-square test), covariate balance (standardized mean difference), exposure check
- **Effect estimation:** two-proportion z-test, 95% confidence intervals, bootstrap CI for relative lift
- **Power analysis:** minimum detectable effect (MDE), sample size requirements, power curve, 85/15 vs. 50/50 allocation
- **Effect on exposed users:** CACE (Wald estimator)

## Key Results
| Metric | Control | Treatment | Relative lift | 95% bootstrap CI | p-value |
|---|---|---|---|---|---|
| Conversion | 0.194% | 0.310% | **+59.7%** | +44.8% to +77.5% | 1.3e-19 |
| Visit | 3.796% | 4.850% | **+27.8%** | +24.9% to +30.7% | 2.9e-98 |

- **Trustworthy experiment:** no sample ratio mismatch (treatment share 85.00%, p = 0.968); all 12 features balanced (max |SMD| = 0.048); no control users exposed
- **Well powered:** MDE of 15.05%; the observed lift is about 4x the MDE. A 50/50 split would have lowered the MDE to 10.75%
- **Low exposure:** only 3.61% of treated users actually saw the ad; the estimated effect on exposed users is +3.21 pp in conversion (indicative)

## Charts

### Conversion rate by group
![Conversion rate by group](Conversion%20Rate%20by%20Group%20%2895%25%20CI%29.png)

### Bootstrap distribution of relative lift
![Bootstrap distribution of relative lift](Bootstrap%20Distribution%20of%20Relative%20Lift%20%28Conversion%29.png)

### Covariate balance
![Covariate balance](Covariate%20Balance%20%28Standardized%20Mean%20Difference.png)

### Power curve
![Power curve](Power%20curve.png)

## Recommendation
- **Roll out the campaign:** it delivers a robust, statistically significant lift in both visits and conversions.
- **Improve ad reach:** only 3.6% of targeted users saw the ad, so most of the potential value is untapped.
- **Next step:** build uplift models to identify which users respond most, and focus spend on them.

## Limitations
- Results are intent-to-treat; the CACE estimate relies on additional assumptions and has wider uncertainty.
- Features are anonymized, which limits business interpretation of segments.
- Conversions are rare (407 in control), which widens the conversion confidence interval.

## Notebook
Full analysis: [ab_test_criteo.ipynb](ab_test_criteo.ipynb)

## Tools
Python (pandas, NumPy, SciPy, statsmodels, Matplotlib), Jupyter Notebook
