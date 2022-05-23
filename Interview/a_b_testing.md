---
sort: 2
---


# A/B Testing
## Basic Steps

- Prerequisites
	- Define key metrics
		- Overall evaluation criterion (OEC)
	- Changes are easy to make
		- E.g. Re-desinging the entire website is difficult
	- Have enough randomization units
		- Thousands. Larger number -> small effect
- Experiment Design
	- What population to select
		- Specific group v.s. all users
		- E.g. Some changes/new features would only affect a particular group people, like in a region...
	- Size of the experiment
		- Statistical power -> sample size
	- How long to run the experiment
- Running Experiment
	- Collect data
		- Instrument loggings
		- Utilize companies platform
- Result to Decision
	- Sanity check (if data is reliable)
	- Consider
		- Tradeoffs between different metrics, like user engagement is up, but revenue is down
		- Cost of launching a change
			- Engineering maintenance, Opportunity cost
			- When costs are high: Benefits should outweigh costs; set practical significance boundary
- Post-launch Monitoring
	- Long term effect can be different from the short-term effect

## Sample Size Determination


$$n\approx\frac{2\sigma^2(Z_{\alpha/2}+Z_\beta)^2}{(\mu_c-\mu_t)^2}$$

## Choose the Right Metrics
- Goal Metric (AKA Success Metric, Primary metric...)
- Driver metric (AKA Surrogate Metric...)
- Guardrail Metric

### Goal Metric
It relates to the company's vision & mission.
E.g. Advertising revenue, daily active users (DAU), monthly active users (MAU)

It should be

- What the company cares about
- Simple to communicate with stakeholders
- Stable over time

Sometimes it is difficult to measure in experiments. E.g. Facebook cares about revenue. But some teams work on improving user engagement, apps and web performance

### Driver Metric
- Short-term
- More suitable for experiments

### Guardrail Metric

- Organizational Guardrail Metric (affect the company's product and benefit)
	- Page loading latency
	- Errors per page
	- Client crashes
- Trustworthy-related Guardrail Metric
	- Check violation of assumptions
	- E.g. Sample Ratio Mismatch (SRM). Chi-squared test. See https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/diagnosing-sample-ratio-mismatch-in-a-b-testing/

## How long to run an A/B test?

Determine the sample size

- Type II error/power
- Significance level
- Minimum detectable effect

$$sample\ size\approx\frac{16\sigma^2}{\delta^2}$$
where $\delta$ is the difference between treatment and control. Then

- More samples if $\sigma$ is larger
- Fewer samples if $\delta$ is larger

$\sigma$ is obtained from data, but we don't know $\delta$ before the experiment, so we use minimum detectable effect.

Minimum detectable effect: smallest difference matters in practice. E.g. 0.1% increase in revenue.

- Round the duration by weeks to capture the weekly pattern

## Multiple Testing Problem

### Bonferroni Correction

Significance / # of tests

Conservative

## Some Other Materials
- Click-through rate (CTR): $\frac{Number\ of\ clicks}{Number\ of\ page\ views}$

 V.S. click-through probability: $\frac{Unique\ visitors\ who\ click}{Unique\ visitors\ to\ page}$

## References

[1] [Youtube: Data Interview Pro by Emma Ding](https://www.baidu.com/)

