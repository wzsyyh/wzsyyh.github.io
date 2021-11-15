---
title: Math
date: 2021-07-30 09:14:28
tag: 学习笔记
category: 学习笔记
---

### 类欧几里得算法

$$\begin{split} f(a,b,c,n)&=\sum_{i=0}^n\left\lfloor \frac{ai+b}{c} \right\rfloor\\ &=\sum_{i=0}^n\left\lfloor \frac{\left(\left\lfloor\frac{a}{c}\right\rfloor c+a\bmod c\right)i+\left(\left\lfloor\frac{b}{c}\right\rfloor c+b\bmod c\right)}{c}\right\rfloor\\ &=\frac{n(n+1)}{2}\left\lfloor\frac{a}{c}\right\rfloor+(n+1)\left\lfloor\frac{b}{c}\right\rfloor+ \sum_{i=0}^n\left\lfloor\frac{\left(a\bmod c\right)i+\left(b\bmod c\right)}{c} \right\rfloor\\ &=\frac{n(n+1)}{2}\left\lfloor\frac{a}{c}\right\rfloor +(n+1)\left\lfloor\frac{b}{c}\right\rfloor+f(a\bmod c,b\bmod c,c,n) \end{split}$$