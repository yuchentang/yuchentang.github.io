---
sort: 4
---

# Some Tips

## Curse of Dimensionality

"The common theme of these problems is that when the dimensionality increases, the volume of the space increases so fast that the available data become sparse. In order to obtain a reliable result, the amount of data needed often grows exponentially with the dimensionality. Also, organizing and searching data often relies on detecting areas where objects form groups with similar properties; in high dimensional data, however, all objects appear to be sparse and dissimilar in many ways, which prevents common data organization strategies from being efficient."

The more dimensions, the less likely points are "close" to each other. Or we can say in high dimensions, distances are almost the same. “Distance” kind of loses its efficacy in high dimensions. 

Solutions: Dimensionality reduction; More data.

## Normalization & Standardization

0-1 normalization: $X_{nor} = \frac{X - X_{min}}{X_{max} - X_{min}}$

z-score standardization: $X_{z} = \frac{X - \mu}{\sigma}$

Why and when do we need to do normalization/standardization before modeling?

- Some machine learning algrithms are based on distances. E.g. In PCA, variables are combined to maximize the variances. Without normalization/standardization, some variables with bigger ranges, i.e. bigger variances, would become too much important in PCA. Also, KNN, K-means.

- For neural networks, normalization/standardization can help converge more quickly. 