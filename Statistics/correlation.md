---
sort: 1
---

# Correlation Coefficient

## Pearson Correlation Coefficient (PCC)

### For a population
$$\rho_{X,Y}=\frac{Cov(X,Y)}{\sigma_X\sigma_Y}=\frac{\mathbb{E}[(X-\mu_X)(Y-\mu_y)]}{\sigma_X\sigma_Y}=\frac{\mathbb{E}(XY)-\mathbb{E}(X)\mathbb{E}(Y)}{\sigma_X\sigma_Y}$$
where

- $Cov()$  is the covariance
- $\sigma_X$ is the standard deviation of $X$
- $\sigma_Y$ is the standard deviation of $Y$
- $\mu _{X}$ is the mean of $X$
- $\mu _{Y}$ is the mean of $Y$
- $\mathbb{E}$ is the expectation.

### For a sample
Given paired data $\{(x_{1},y_{1}),...,(x_{n},y_{n})\}$ consisting of $n$ pairs, $r_{xy}$ is defined as:

$$r_{xy}=\frac{\sum_{i=1}^n(x_i-\bar{x})(y_i-\bar{y})}{\sqrt{\sum_{i=1}^n(x_i-\bar{x})^2}\sqrt{\sum_{i=1}^n(y_i-\bar{y})^2}}$$

### P-value
For Pearson's correlation coefficient:
$$
H_0: \rho = 0 \\
H_1: \rho \neq 0
$$
To calculate the p-value:
$$t=\frac{r\sqrt{(n-2)}}{\sqrt{1-r^2}}$$
The p-value is $2 \times P(T > t)$ where T follows a t-distribution with n – 2 degrees of freedom.

### Drawbacks
- Only include two sets of data
- Only shows the linear relationship
- Not able to tell the difference between dependent variables and independent variables (Causality)

## Spearman's Rank Correlation Coefficient

Spearman's Rank Correlation Coefficient, is also called Spearman's rho ($\rho$). It is defined as the Pearson correlation coefficient between the rank variables.

For a sample of size n, the n raw scores $X_{i}$, $Y_{i}$ are converted to ranks $R(X_{i})$, $R(Y_{i})$, and $r_{s}$ is computed as

$$
r_s=\rho_{R(X),R(Y)}=\frac{Cov(R(X),R(Y))}{\sigma_{R(X)}\sigma_{R(Y)}}
$$
where

- $\rho$ denotes the usual Pearson correlation coefficient, but applied to the rank variables
- $Cov(R(X),R(Y))$ is the covariance of the rank variables
- $\sigma_{R(X)}$ and $\sigma_{R(Y)}$ are the standard deviations of the rank variables.
