---
sort: 2
---

# Some ML

## Curse of Dimensionality

"The common theme of these problems is that when the dimensionality increases, the volume of the space increases so fast that the available data become sparse. In order to obtain a reliable result, the amount of data needed often grows exponentially with the dimensionality. Also, organizing and searching data often relies on detecting areas where objects form groups with similar properties; in high dimensional data, however, all objects appear to be sparse and dissimilar in many ways, which prevents common data organization strategies from being efficient." ([Wikipedia: Curse of dimensionality](https://en.wikipedia.org/wiki/Curse_of_dimensionality))

The more dimensions, the less likely points are "close" to each other. Or we can say in high dimensions, distances are almost the same. “Distance” kind of loses its efficacy in high dimensions. 

Another perspective, when picking a point in a 'cube' randomly, the probability that it is close to the border is increasing. E.g. See lec8 pdf slides of 5293: dimensionality reduction.

Solutions: Dimensionality reduction; More data.

## Normalization & Standardization

0-1 normalization: $X_{0-1} = \frac{X - X_{min}}{X_{max} - X_{min}}$

Z-score standardization: $X_{z} = \frac{X - \mu}{\sigma}$

Why and when do we need to do normalization/standardization before modeling?

- Some machine learning algrithms are based on distances. E.g. In PCA, variables are combined to maximize the variances. Without normalization/standardization, some variables with bigger ranges, i.e. bigger variances, would become too much important in PCA. Also, KNN, K-means.

- For neural networks, normalization/standardization can help converge more quickly. E.g. for sigmoid or tanh function, the gradient is bigger around 0, when the value is large, the gradient is much smaller. 