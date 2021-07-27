---
sort: 1
---


# 随机变量函数的p.d.f.

* 例题：$$X$$ has p.d.f. $$f(x)$$, what is p.d.f. of $$Y=aX+b \ (a>0)$$?

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