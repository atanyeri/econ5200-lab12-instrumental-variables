# Instrumental Variables: Weak Instruments, Compliers and the Exclusion Restriction

## Objective
I tested when an instrumental-variables estimate can be trusted, using simulated data with a known true effect and Card's (1995) college-proximity data.

## Methodology
- Simulated data where the true effect of the treatment on the outcome is 1.0 and an unobserved confounder pushes OLS upward. I varied the strength of the instrument and ran 500 samples at each strength, recording the median first-stage F, the median OLS and 2SLS estimates, and how often a significant 2SLS estimate was far from the truth.
- Replicated Card's college-proximity instrument for schooling, using experience, experience squared, race, region and metropolitan residence as controls. I reported the first-stage F with the OLS and 2SLS returns to schooling.
- Added a small direct effect of the instrument on the outcome in a simulation, and swept it from 0 to 0.5 to see how far it moves the 2SLS estimate.
- Applied the same idea to the Card data by subtracting a direct effect from the outcome before re-estimating.
- Wrote my own two-stage least squares function from two OLS regressions, with the first-stage F, and checked it against the linearmodels package.

## Key Findings
- **Weak instrument:** At the weakest strength, the median first-stage F was 0.5. The median 2SLS estimate was 2.038, against a median OLS estimate of 1.998. A weak instrument pulls 2SLS toward OLS, not toward the truth of 1.0.
- **Significance is not reassurance:** At that strength, 21.0% of samples gave a significant 2SLS estimate, and 98.1% of those were more than 0.5 away from the truth. With a slightly stronger instrument, 75.2% of the significant estimates were still that far off. Inference breaks before the estimate does, so I check the first-stage F before reading the second stage.
- **Card (1995):** The first-stage F was 16.7. The OLS return to schooling was 0.0740 and the 2SLS return was 0.1323. The 2SLS estimate is larger than OLS, which fits an effect for compliers, or measurement error in schooling, rather than ability bias alone.
- **Exclusion restriction:** In the simulation, each 0.05 of direct effect added about 0.111 to the estimate, and the estimate moved by more than 0.5 once the direct effect reached 0.25. In the Card data, a direct effect of 0.02 was enough to take 2SLS (0.0730) below OLS (0.0740).
- **My own function:** It matched linearmodels on Card, giving 0.1323 and an F of 16.7.
