---
title: "Welch's t-test: 등분산 가정이 깨졌을 때의 평균 비교"
date: 2026-06-22 10:00:00 +0900
categories:
  - Statistics
  - Applied Statistics
tags:
  - Statistics
  - Hypothesis Test
  - t-test
  - Welch Test
math: true
toc: true
---



# Welch's t-test: 등분산 가정이 깨졌을 때의 평균 비교

## 1. 들어가며

두 집단의 평균을 비교할 때 가장 많이 사용하는 검정은 독립 이표본 t-test(Two Sample t-test)이다.

예를 들어,

- 남성과 여성의 평균 소득 차이
- 신약 투여군과 대조군의 평균 혈압 차이
- 대기업과 중소기업의 평균 매출 차이

등을 검정할 때 사용한다.

하지만 우리가 흔히 배우는 Student's t-test는 하나의 중요한 가정을 가지고 있다.

> 두 모집단의 분산이 동일하다.

즉,

$$
\sigma_1^2=\sigma_2^2
$$

를 가정한다.

현실에서는 이 가정이 생각보다 자주 깨진다.

예를 들어 대기업과 중소기업의 매출 분포를 생각해보면 평균뿐만 아니라 변동성 자체가 매우 다르다. 이러한 상황에서 기존의 Student's t-test를 사용하면 검정의 유의수준(Type I Error)이 왜곡될 수 있다.

이를 해결하기 위해 사용하는 방법이 바로 **Welch's t-test**이다.

---

## 2. Student's t-test 복습

두 집단에서

$$
Y_{1i}\sim N(\mu_1,\sigma^2)
$$

$$
Y_{2j}\sim N(\mu_2,\sigma^2)
$$

라고 하자.

등분산 가정 하에서는 pooled variance를 이용하여

$$
s_p^2=
\frac{
(n_1-1)s_1^2+
(n_2-1)s_2^2
}{
n_1+n_2-2
}
$$

를 정의할 수 있다.

그러면 검정통계량은

$$
t=
\frac{
(\bar Y_1-\bar Y_2)-(\mu_1-\mu_2)
}{
s_p
\sqrt{
\frac1{n_1}+\frac1{n_2}
}
}
$$

가 되고,

$$
t\sim t_{n_1+n_2-2}
$$

를 정확히 따른다.

---

## 3. 문제점: 분산이 다르면?

현실에서는

$$
\sigma_1^2 \neq \sigma_2^2
$$

인 경우가 많다.

이때 평균 차이의 분산은

$$
Var(\bar Y_1-\bar Y_2)
=
\frac{\sigma_1^2}{n_1}
+
\frac{\sigma_2^2}{n_2}
$$

가 된다.

즉, 분산이 서로 다르면 pooled variance 자체가 성립하지 않는다.

그럼에도 불구하고 Student's t-test를 사용하면 분모가 잘못 계산되고, 결과적으로 p-value와 신뢰구간이 왜곡될 수 있다.

특히,

- 표본 수가 많이 다르고
- 분산도 크게 다를 때

왜곡이 심해질 수 있다.

---

## 4. Welch's t-test

어쩔 수 없이, 분모를 솔직하게 계산하자.

평균 차이의 분산을 그대로 추정하면

$$
\widehat{Var}
(\bar Y_1-\bar Y_2)
=
\frac{s_1^2}{n_1}
+
\frac{s_2^2}{n_2}
$$

이다.

따라서 검정통계량은

$$
T=
\frac{
(\bar Y_1-\bar Y_2)-(\mu_1-\mu_2)
}{
\sqrt{
\frac{s_1^2}{n_1}
+
\frac{s_2^2}{n_2}
}
}
$$

가 된다.

---

## 5. 새로운 문제: 더 이상 t 분포가 아니다

Student's t-test가 정확한 t 분포를 따르는 이유는

분모가 하나의 카이제곱 분포(χ²)로 표현되기 때문이다.

하지만 Welch 검정의 분모는

$$
\frac{s_1^2}{n_1}
+
\frac{s_2^2}{n_2}
$$

이다.

즉,

두 개의 서로 다른 χ² 변수를 더한 형태이다.

예를 들면,

$$
a\chi_{10}^2+b\chi_{20}^2
$$

와 비슷한 형태가 된다.

이 분포는 더 이상 χ² 분포가 아니다.

따라서 검정통계량 역시 정확한 t 분포를 따르지 않는다.

---

## 6. Welch-Satterthwaite Approximation

Welch의 핵심 아이디어는 다음과 같다.

> 복잡한 분모를 적당한 χ² 하나로 근사하자.

즉,

$$
\frac{s_1^2}{n_1}
+
\frac{s_2^2}{n_2}
$$

가

$$
C\cdot
\frac{\chi_d^2}{d}
$$

처럼 행동한다고 가정한다.

여기서

- $C$ : 적절한 상수
- $d$ : 근사적인 자유도

이다.

---

## 7. Moment Matching

Welch-Satterthwaite 근사는 사실상 **Moment Matching**이다.

즉,

1. 평균(E)
2. 분산(Var)

이 서로 같도록 척도상수 $C$와 자유도 $d$를 선택한다.

카이제곱 분포는

$$
E(\chi_d^2)=d
$$

$$
Var(\chi_d^2)=2d
$$

라는 성질을 가진다.

따라서

복잡한 분산 추정량과

가상의 χ² 분포가

동일한 평균과 분산을 가지도록 척도상수와 자유도를 결정한다.

그 결과,

유효 자유도(Effective Degrees of Freedom)

$$
d=
\frac{
\left(
\frac{s_1^2}{n_1}
+
\frac{s_2^2}{n_2}
\right)^2
}{
\frac{
(s_1^2/n_1)^2
}{
n_1-1
}
+
\frac{
(s_2^2/n_2)^2
}{
n_2-1
}
}
$$

를 얻는다.

이를 **Welch-Satterthwaite Approximation**이라고 부른다.

<small> 척도상수 C는, 검정통계량을 상쇄하는 과정에서 삭제되어, 식에 나타나지 않는다. </small>

<details markdown="1">

### Welch–Satterthwaite 근사의 구체적인 과정

두 집단의 표본분산을 이용하여 평균 차이의 분산을 추정한 값을

$$
Q=
\frac{s_1^2}{n_1}
+
\frac{s_2^2}{n_2}
$$

라고 하자. 정규성 가정 아래에서

$$
\frac{(n_i-1)s_i^2}{\sigma_i^2}
\sim
\chi_{n_i-1}^2
$$

이므로

$$
Q=
\frac{\sigma_1^2}{n_1}
\frac{\chi_{n_1-1}^2}{n_1-1}
+
\frac{\sigma_2^2}{n_2}
\frac{\chi_{n_2-1}^2}{n_2-1}
$$

로 나타낼 수 있다.

Welch–Satterthwaite 근사는 이 복잡한 가중합을 다음과 같은 하나의 카이제곱 확률변수로 근사한다.

$$
Q
\approx
C\frac{\chi_d^2}{d}
$$

#### 1. 평균을 맞추면 $C$가 결정된다

먼저 $Q$의 평균은

$$
E(Q)
=

\frac{\sigma_1^2}{n_1}
+
\frac{\sigma_2^2}{n_2}
$$

이다. 한편 근사분포의 평균은

$$
E\left(
C\frac{\chi_d^2}{d}
\right)
=

C
$$

이므로, 두 평균을 일치시키면

$$
C=
\frac{\sigma_1^2}{n_1}
+
\frac{\sigma_2^2}{n_2}
$$

를 얻는다.

즉, $C$는 두 표본평균 차이의 실제 분산이다.

$$
C=
\operatorname{Var}(\bar{Y}_1-\bar{Y}_2)
$$

#### 2. 분산을 맞추면 $d$가 결정된다

$Q$의 분산은

$$
\operatorname{Var}(Q)
=

2\left[
\frac{(\sigma_1^2/n_1)^2}{n_1-1}
+
\frac{(\sigma_2^2/n_2)^2}{n_2-1}
\right]
$$

이다. 근사분포의 분산은

$$
\operatorname{Var}\left(
C\frac{\chi_d^2}{d}
\right)
=

\frac{2C^2}{d}
$$

이므로, 두 분산을 일치시키면

$$
d=
\frac{
\left(
\frac{\sigma_1^2}{n_1}
+
\frac{\sigma_2^2}{n_2}
\right)^2
}{
\frac{(\sigma_1^2/n_1)^2}{n_1-1}
+
\frac{(\sigma_2^2/n_2)^2}{n_2-1}
}
$$

를 얻는다.

실제로는 모집단 분산 $\sigma_i^2$을 알 수 없으므로 표본분산 $s_i^2$을 대입한다. 이에 따라 Welch 검정의 유효 자유도는

$$
df=
\frac{
\left(
\frac{s_1^2}{n_1}
+
\frac{s_2^2}{n_2}
\right)^2
}{
\frac{(s_1^2/n_1)^2}{n_1-1}
+
\frac{(s_2^2/n_2)^2}{n_2-1}
}
$$

로 계산된다.

#### 그렇다면 왜 $C$는 최종 공식에서 사라지는가?

평균 차이에서 귀무가설이 주장하는 값을 뺀 것을

$$
D=
(\bar{Y}_1-\bar{Y}_2)
-

(\mu_1-\mu_2)
$$

라고 하자. 그러면

$$
\frac{D}{\sqrt{C}}
\sim
N(0,1)
$$

이다.

Welch 검정통계량은

$$
T=
\frac{D}{\sqrt{Q}}
$$

이며, 이를 다음과 같이 나타낼 수 있다.

$$
T=
\frac{D/\sqrt{C}}
{\sqrt{Q/C}}
$$

Moment matching에 따르면

$$
Q
\approx
C\frac{\chi_d^2}{d}
$$

이므로

$$
\frac{Q}{C}
\approx
\frac{\chi_d^2}{d}
$$

이다.

또한 정규성 가정 아래에서 표본평균과 표본분산은 서로 독립이므로

$$
T
\approx
\frac{N(0,1)}
{\sqrt{\chi_d^2/d}}
\sim
t_d
$$

를 얻는다.

따라서, 분자와 분모를 동일한 분산 $C$로 표준화하는 과정에서 $C$가 상쇄된 것이다. 그 결과 최종 검정통계량에는 $C$가 나타나지 않고 근사 자유도 $d$만 남는다.

<summary>증명 보기</summary>

</details>

---

## 8. 왜 자유도가 소수가 되는가?

Welch 검정을 해보면

```
df = 15.7
df = 22.4
df = 31.9
```

처럼 자유도가 소수로 나온다.

처음 보면 이상해 보인다.

우리는 보통 자유도를

```
n-1
n-p
```

처럼 정수로 배웠기 때문이다.

하지만 Welch의 자유도는

> 실제 정보량(Effective Information)

을 나타낸다.

즉,

```
df = 15.7
```

이라는 의미는

> 약 16개의 독립적인 관측치를 가진 것과 비슷한 정도의 정보량을 가진다.

라고 해석할 수 있다.

---

## 9. 직관적으로 이해하기

분산이 큰 집단은 평균을 불안정하게 추정한다.

즉,

- 평균 추정의 오차가 크고
- 정보량은 적다.

반대로 분산이 작은 집단은

- 평균을 안정적으로 추정하고
- 정보량은 크다.

Welch 자유도는

두 집단의 정보량을 적절히 반영한

**유효 자유도(Effective Degrees of Freedom)**

라고 이해할 수 있다.

---

## 10. 정리

Welch's t-test는

> "분산이 서로 다른 두 집단의 평균을 비교하기 위한 t-test"

이다.

핵심 아이디어는 다음과 같다.

1. 등분산 가정을 버린다.
2. 평균 차이의 분산을 직접 추정한다.
3. 분모는 더 이상 χ²가 아니므로 정확한 t 분포가 깨진다.
4. 평균과 분산(moment)을 맞추어 하나의 χ² 분포로 근사한다.
5. 그 결과 유효 자유도(Effective Degrees of Freedom)가 도출된다.

결국 Welch's t-test의 본질은

> **복잡한 분모를 Moment Matching을 통해 하나의 χ² 분포로 근사하고, 그 결과 얻어진 유효 자유도를 이용하여 t 분포를 흉내 내는 방법**

이라고 이해할 수 있다.