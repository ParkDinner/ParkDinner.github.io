---
layout: post
title: matrixMultiply
date: 2022-10-03 22:50:00 +0900
hide_description: true
sitemap: false
# comments: true
# image: /assets/img/math/linearalgebra_matrixMultiply.png
categories: [math, linearalgebra]
description: >
  행렬 곱에 대해 알아보자
---
# [LinearAlgebra] 행렬 곱


## 1. 행렬 곱

_m x n_ 행렬 **_A_**와 _n_ 열 벡터 **_x_** 의 곱은 다음과 같이 나타낼 수 있다.

---
$$
Ax=
\left[\begin{array}{cccc}
a_{11}&a_{12}&\dots&a_{1n}\\
a_{21}&a_{22}&\dots&a_{2n}\\
\vdots&\vdots&\ddots&\vdots\\
a_{m1}&a_{m2}&\dots&a_{mn}\\
\end{array}\right]
\left[\begin{array}{c}
x_{1}\\x_{2}\\\vdots\\x_{n}
\end{array}\right]=
\left[\begin{array}{c}
\textstyle\sum_{k=1}^na_{1k}x_k\\
\textstyle\sum_{k=1}^na_{2k}x_k\\
\vdots\\
\textstyle\sum_{k=1}^na_{mk}x_k
\end{array}\right]
$$

---

행렬을 column 벡터의 모음으로 고려한다면, 다음과 같은 표현도 가능하다.

---

$$
A=
\left[\begin{array}{cccc}
a_1&a_2&\dots&a_m
\end{array}\right]
,(a_1=\left[\begin{array}{c}a_{11}\\a_{21}\\\vdots\\a_{m1}\end{array}\right])\\Ax=
\left[\begin{array}{cccc}a_1&a_2&\dots&a_m\end{array}\right]\left[\begin{array}{c}
x_{1}\\x_{2}\\\vdots\\x_{n}
\end{array}\right] = a_1x_1 + a_2x_2 +\dots+a_nx_n 
$$

---

이번에는 column 벡터 _**v**_ 와 row _**w**_ 벡터의 곱을 표현해보자.

---

$$
vw=\left[\begin{array}{cccc}
v_{1}\\v_{2}\\\vdots\\v_{m}
\end{array}\right]
\left[\begin{array}{c}
w_1&w_2&\dots&w_n
\end{array}\right]=\left[\begin{array}{cccc}
v_1w_1&v_1w_2&\dots&v_1w_n\\
v_2w_1&v_2w_2&\dots&v_2w_n\\
\vdots&\vdots&\ddots&\vdots\\
v_mw_1&v_mw_1&\dots&v_mw_n
\end{array}\right]
$$

### 일반화
마지막으로, _m x n_ 행렬 **_A_**와 _n x p_ 행렬 **_B_**의 곱을 일반화해서 표현해보자.

$$
AB=
\left[\begin{array}{cccc}
a_{11}&a_{12}&\dots&a_{1n}\\
a_{21}&a_{22}&\dots&a_{2n}\\
\vdots&\vdots&\ddots&\vdots\\
a_{m1}&a_{m2}&\dots&a_{mn}\\
\end{array}\right]
\left[\begin{array}{cccc}
b_{11}&b_{12}&\dots&b_{1p}\\
b_{21}&b_{22}&\dots&b_{2p}\\
\vdots&\vdots&\ddots&\vdots\\
b_{n1}&b_{n2}&\dots&b_{np}\\
\end{array}\right]
\\=
\left[\begin{array}{cccc}
\textstyle\sum_{k=1}^na_{1k}x_{k1}&
\textstyle\sum_{k=1}^na_{1k}x_{k2}&\dots&
\textstyle\sum_{k=1}^na_{1k}x_{kp}\\
\textstyle\sum_{k=1}^na_{2k}x_{k1}&
\textstyle\sum_{k=1}^na_{2k}x_{k2}&\dots&
\textstyle\sum_{k=1}^na_{2k}x_{kp}\\
\vdots&\vdots&\ddots&\vdots\\
\textstyle\sum_{k=1}^na_{mk}x_{k1}&
\textstyle\sum_{k=1}^na_{mk}x_{k2}&\dots&
\textstyle\sum_{k=1}^na_{mk}x_{kp}
\end{array}\right]\in\R^{m\times n}
$$

행렬 곱은 다음 조건을 만족시켜야만 한다.
> 행렬 A의 row 길이와 행렬 B의 column 길이가 같아야 한다.
> 즉, (_m x n_ 행렬 **_A_**와 _n x p_ 행렬 **_B_**의 곱) = (m x p) 행렬 _**AB**_

마무리로, 행렬 곱을 코드로 나타내 보자.

```java
        //java
        double[][] matrixA = new double[COL_A][ROW_A];
        double[][] matrixB = new double[COL_B][ROW_B];
        if(ROW_A == COL_B){
            double[][] matrixAB = new double[COL_A][ROW_B];
            for(int i = 0; i < COL_A ; i++)
                for(int j = 0; j < ROW_B; j++)
                    for(int k = 0; k < ROW_A ; k++)
                        matrixAB[i][j] = matrixA[i][k] * matrixB[k][j];
        }
```

## 2. 행렬 곱의 성질
### 교환 법칙

---

$$AB\not=BA$$

행렬의 덧셈 같은 경우에는 교환 법칙이 성립하지만, 행렬 곱의 경우에는 계산 자체가 달라지기에 성립할 수 없다.

---

### 결합 법칙

---
$$(AB)C=A(BC)$$

결합 법칙의 경우에는 계산식은 변하지 않으며 순서만 변하게 되므로 성립한다. 
재미있는 점은, 계산 순서에 따라 필요한 연산의 수가 달라질 수 있다는 점이다.
이에 관한 건 연쇄 행렬 알고리즘 포스트에 구체적으로 서술하겠다.

---

### 분배 법칙

---

$$C(A+B)=CA+CB\\(A+B)C=AC+BC$$


상술하였듯, 행렬 곱에서는 교환 법칙이 성립하지 않는다. 
수식에 따라 계산에 유의해야 한다.