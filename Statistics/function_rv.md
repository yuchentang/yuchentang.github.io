---
sort: 4
---


# 例题：随机变量函数的p.d.f.

## 例题1

$X$ has p.d.f. $f(x)$, what is p.d.f. of $Y=aX+b (a>0)$?

Solution: 通过c.d.f.作为桥梁来得到随机变量函数的p.d.f.

$$
\begin{align}
F_Y(y) &\triangleq P(Y \leq y)=P(aX+b\leq y)\\
&=P(X\leq \frac{y-b}{a})=\int_{-\infty}^{\frac{y-b}{a}}f(x)dx\\
&=F_x(\frac{y-b}{a})
\end{align}
$$

对 $F_Y(y)$ 进行求导可以得到 $f_Y(y)$ ,

$$
\begin{align}
f_Y(y)=F'_Y(y) &=\frac{d}{dy}F_x(\frac{y-b}{a}) \\
&=F'(\frac{y-b}{a})\cdot \frac{1}{a} \\
&= \frac{1}{a}f_X(\frac{y-b}{a})
\end{align}
$$

## 例题2

X $\perp\,\!\,\!\,\!\,\!\,\!\,\!\,\!\!\!\!\perp$ Y，求 $Z=X+Y$ 的分布？

Solution:

$$
\begin{align}
F_Z(a)&=P(Z\leq a)=P(X+Y\leq a) \\
&=\int_{\{(x,y):x+y\leq a\}}f_X(x)f_Y(y)dxdy \\
&=\int_{-\infty}^{+\infty}[\int_{-\infty}^{a-x}f_X(x)f_Y(y)dy]dx \\
&=\int_{-\infty}^{+\infty}f_X(x)F_Y(a-x)dx \\
\end{align}
$$

于是有

$$
F'_Z(a)=\int_{-\infty}^{+\infty}f_X(x)f_Y(a-x)dx \triangleq f_Z(a)
$$