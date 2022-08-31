---
sort: 4
---

# P-value and Significance Test

## P-value

- **Definition**: Probability of obtaining a real-valued test statistic at least as extreme as the one actually obtained, under the assumption that the null hypothesis is correct. 

## Significance Test


'Absence of evidence is not evidence of absence.'

## Type I and II Error

- Type I error ($\alpha$) is the probability of rejecting $H_0$ when $H_0$ is true, i.e., false positive rate. 
- Type II error ($\beta$) is the probability of not rejecting $H_0$ when $H_a$ is true (or $H_0$ is false), i.e., false negative rate. 

$\alpha$ is also referred to as ‘significance level’. 

[Note: R.A. Fisher and all others before J. Neyman and E. Pearson did not use an explicit alternative or talk of error rates. P-values can be defined and used without either concept.]


## Misuse & Controversy

- **Misunderstanding**: Treat the p-value as the probability that the null hypothesis is true.
- **P-hacking**: Also known as 'inflation bias' or 'selective reporting'. It is the misreporting of true effect sizes in published studies. It occurs when researchers try out several statistical analyses and/or data eligibility specifications and then selectively report those that produce significant results. Common practices that lead to p-hacking include: conducting analyses midway through experiments to decide whether to continue collecting data; recording many response variables and deciding which to report postanalysis, deciding whether to include or drop outliers postanalyses, excluding, combining, or splitting treatment groups postanalysis, including or excluding covariates postanalysis, and stopping data exploration if an analysis yields a significant p-value.
- Somebody suggests: P-value is not enough. Report the **effect size**. E.g. [Sullivan and Feinn (2012): Using Effect Size—or Why the P Value Is Not Enough](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3444174/)

## References:

[1] [Head et al. (2015): The Extent and Consequences of P-Hacking in Science](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4359000/)