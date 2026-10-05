---
title: "[GLM] #03. GLM의 확률분포는 왜 Exponential Family일까?"
date: 2026-10-05 20:00:00 +0900
categories:
  - Statistics
  - Applied Statistics
  - Regression
tags:
  - GLM
  - Generalized Linear Model
  - Linear Regression
math: true
toc: true
published: true
---

# GLM의 확률분포는 왜 Exponential Family일까?

지난 글에서는 Generalized Linear Model(GLM)이 일반적인 선형회귀와 달리 반응변수의 특성에 맞는 확률분포를 사용할 수 있다는 점을 살펴보았다.

예를 들어,

- 이진자료에는 Bernoulli 분포
- 개수자료에는 Poisson 분포
- 양수 연속형 자료에는 Gamma 분포

등을 사용할 수 있다.

그런데 여기서 한 가지 의문이 생긴다.

> **GLM에서는 어떤 확률분포든 사용할 수 있는 것일까?**

그렇지는 않다.

고전적인 GLM에서는 반응변수의 분포가 **Exponential Family(지수족)** 에 속한다고 가정한다.

Bernoulli, Binomial, Poisson, Normal, Gamma 등은 겉보기에는 서로 전혀 다른 확률분포처럼 보이지만, 이들을 적절하게 정리하면 하나의 공통된 수학적 형태로 표현할 수 있다.

이번 글에서는 이 공통된 구조가 무엇인지 살펴보고, Bernoulli 분포를 직접 Exponential Family의 형태로 변환해 보려고 한다.

---

# 1. Exponential Family란 무엇인가?

GLM에서 사용하는 Exponential Family는 일반적으로 다음과 같은 형태로 표현할 수 있다.

$$
f(y;\theta,\phi)
=
\exp
\left[
\frac{y\theta-b(\theta)}{a(\phi)}
+
c(y,\phi)
\right]
$$

처음 보면 다소 복잡해 보인다.

하지만 우선 모든 기호를 이해하려 하기보다 가운데에 있는

$$
y\theta-b(\theta)
$$

에 주목해 보자.

여기서

- $y$ : 실제 관측값
- $\theta$ : Natural Parameter(자연모수)
- $\phi$ : Dispersion Parameter(산포모수)

를 의미한다.

즉, Exponential Family에 속하는 분포들은 서로 다른 확률분포임에도 불구하고 **관측값과 모수 사이의 관계를 공통된 형태로 정리할 수 있다.**

이것이 Bernoulli, Poisson, Normal, Gamma와 같은 서로 다른 분포들을 하나의 Family로 묶을 수 있는 이유이다.

---

# 2. 왜 이런 형태가 중요한가?

단순히 여러 확률분포를 하나의 식으로 표현할 수 있다는 것만으로는 큰 의미가 없어 보일 수도 있다.

Exponential Family가 중요한 이유는 이러한 형태를 가지면 **분포의 평균과 분산을 매우 체계적으로 표현할 수 있기 때문**이다.

위와 같은 형태의 Exponential Family에서는 적절한 정규성 조건 아래

$$
E[Y]=b'(\theta)
$$

이고,

$$
Var(Y)=a(\phi)b''(\theta)
$$

라는 관계가 성립한다.

즉, $b(\theta)$를 한 번 미분하면 평균이 나오고, 두 번 미분하면 분산의 구조가 나타난다.

이것은 GLM에서 매우 중요한 성질이다.

GLM은 결국

$$
\mu=E[Y|X]
$$

라는 **조건부 평균**을 설명하는 모형이기 때문이다.

따라서 Exponential Family를 사용하면

$$
\theta
\longleftrightarrow
\mu
$$

의 관계를 체계적으로 정의할 수 있다.

그리고 이 관계가 이후 살펴볼 **Link Function**과 연결된다.

---

# 3. 모든 확률분포가 Exponential Family인 것은 아니다.

물론 세상에 존재하는 모든 확률분포가 Exponential Family에 속하는 것은 아니다.

예를 들어 일반적인 형태의

- Cauchy distribution
- Student's $t$ distribution
- 일부 mixture distribution

등은 GLM에서 사용하는 일반적인 유한차원 Exponential Family의 형태로 표현되지 않는다.

그렇다고 이러한 분포가 통계적으로 잘못된 분포라는 뜻은 아니다.

Exponential Family에 속한다는 것은 분포의 우수성을 의미하는 것이 아니라,

> **관측값과 모수 사이에 특정한 수학적 구조가 존재한다**

는 것을 의미한다.

이 구조 덕분에 Exponential Family에서는 평균, 분산, 충분통계량, Likelihood, Fisher Information 등 여러 통계적 성질을 하나의 체계 안에서 다룰 수 있다.

GLM은 바로 이러한 구조를 활용하는 모형이다.

---

# 4. Bernoulli 분포를 Exponential Family로 표현해보자.

그렇다면 실제 확률분포 하나를 Exponential Family 형태로 바꾸어 보자.

가장 단순한 Bernoulli 분포부터 시작한다.

$$
Y\sim Bernoulli(p)
$$

라면 확률질량함수는

$$
P(Y=y)
=
p^y(1-p)^{1-y},
\qquad
y\in\{0,1\}
$$

이다.

여기에 지수함수를 사용하면

$$
P(Y=y)
=
\exp
\left[
\log\left(
p^y(1-p)^{1-y}
\right)
\right]
$$

로 표현할 수 있다.

로그의 성질을 이용하면

$$
=
\exp
\left[
y\log p
+
(1-y)\log(1-p)
\right]
$$

이고,

이를 다시 정리하면

$$
=
\exp
\left[
y\log\left(\frac{p}{1-p}\right)
+
\log(1-p)
\right]
$$

가 된다.

이제 앞에서 보았던 Exponential Family의 형태와 비교해보자.

$$
f(y;\theta,\phi)
=
\exp
\left[
\frac{y\theta-b(\theta)}{a(\phi)}
+
c(y,\phi)
\right]
$$

Bernoulli 분포에서는 $y$와 함께 나타나는 부분이

$$
y\log\left(\frac{p}{1-p}\right)
$$

이다.

따라서 Bernoulli 분포의 Natural Parameter는

$$
\boxed{
\theta
=
\log\left(\frac{p}{1-p}\right)
}
$$

가 된다.

---

# 5. Natural Parameter가 왜 중요할까?

여기서 중요한 개념 하나가 등장했다.

바로 **Natural Parameter(자연모수)** 이다.

Bernoulli 분포는 원래 확률 $p$를 이용하여 표현했다.

$$
Y\sim Bernoulli(p)
$$

하지만 이를 Exponential Family의 관점에서 바라보면 자연스럽게 등장하는 모수는 $p$ 자체가 아니라

$$
\theta
=
\log\left(\frac{p}{1-p}\right)
$$

이다.

즉,

$$
p
\longrightarrow
\log\left(\frac{p}{1-p}\right)
$$

라는 변환이 단순히 임의로 선택된 것이 아니다.

**Bernoulli 분포를 Exponential Family의 형태로 표현했더니 자연스럽게 등장한 모수**이다.

그래서 이를 Natural Parameter라고 부른다.

---

# 6. 여기서 Logit이 등장한다.

Bernoulli 분포의 평균은

$$
E[Y]=p
$$

이다.

이를

$$
\mu=E[Y]
$$

라고 표현하면

$$
\mu=p
$$

이므로 자연모수는

$$
\theta
=
\log\left(\frac{\mu}{1-\mu}\right)
$$

가 된다.

그런데 GLM에서는 평균 $\mu$와 설명변수의 선형결합을 Link Function을 통해 연결한다.

$$
g(\mu)=X\beta
$$

만약 Link Function을 자연모수와 동일하게 선택한다면

$$
g(\mu)=\theta
$$

이고,

Bernoulli에서는

$$
g(\mu)
=
\log\left(\frac{\mu}{1-\mu}\right)
$$

가 된다.

이 함수가 바로 **Logit Link**이다.

따라서 Bernoulli 분포에서 Logit Link가 등장하는 것은 우연이 아니다.

Bernoulli 분포를 Exponential Family의 형태로 표현하면 자연모수가

$$
\log\left(\frac{p}{1-p}\right)
$$

로 나타나기 때문이다.

이처럼 **Link Function을 Natural Parameter와 동일하게 선택한 경우** 이를 **Canonical Link**라고 한다.

따라서 Bernoulli 분포의 Canonical Link는 Logit Link이다.

---

# 7. 다른 분포에서도 같은 일이 일어난다.

이러한 관계는 Bernoulli에서만 나타나는 것이 아니다.

대표적인 분포들을 정리하면 다음과 같다.

| Distribution | Mean $\mu$ | Natural Parameter $\theta$ | Canonical Link |
|---|---:|---:|---:|
| Normal | $\mu$ | $\mu$ | Identity |
| Bernoulli / Binomial | $\mu$ | $\log\frac{\mu}{1-\mu}$ | Logit |
| Poisson | $\mu$ | $\log\mu$ | Log |
| Gamma | $\mu$ | $-\frac{1}{\mu}$ | Inverse* |

\* Gamma의 경우 parameterization과 부호 convention에 따라 canonical parameter의 표현을 주의해서 볼 필요가 있다.

예를 들어 Poisson 분포를 Exponential Family 형태로 정리하면 자연모수가

$$
\theta=\log\mu
$$

가 된다.

따라서 Poisson의 Canonical Link는 자연스럽게

$$
g(\mu)=\log\mu
$$

인 Log Link가 된다.

반면 Gamma 분포에서는 Log Link를 자주 사용하지만, Log Link가 Canonical Link인 것은 아니다.

즉,

> **실무에서 자주 사용하는 Link Function과 Canonical Link가 반드시 같은 것은 아니다.**

---

# 8. 그렇다면 Exponential Family가 아닌 분포는 무엇이 다를까?

여기까지 살펴보면 Exponential Family의 의미를 조금 다르게 볼 수 있다.

핵심은 단순히 여러 분포를 하나의 이름 아래 묶는 것이 아니다.

Exponential Family에서는

$$
\text{Distribution}
\rightarrow
\text{Natural Parameter } \theta
\rightarrow
E[Y]=\mu
$$

라는 관계를 체계적으로 구성할 수 있다.

그리고 GLM에서는 여기에 Link Function을 추가하여

$$
\mu
\rightarrow
g(\mu)
\rightarrow
X\beta
$$

로 연결한다.

특히

$$
g(\mu)=\theta
$$

로 선택하면 Canonical Link가 된다.

따라서 전체적인 구조는

$$
\boxed{
\text{Exponential Family}
\rightarrow
\text{Natural Parameter}
\rightarrow
\text{Mean}
\rightarrow
\text{Link Function}
\rightarrow
X\beta
}
$$

로 이어진다.

Exponential Family에 속하지 않는 분포가 사용할 수 없는 분포라는 의미는 아니다.

다만 이러한 **공통된 구조를 그대로 이용할 수 없기 때문에 고전적인 GLM의 틀에서 벗어나게 된다.**

---

# 정리

이번 글의 핵심은 다음과 같다.

> **GLM에서는 서로 다른 확률분포를 아무렇게나 사용하는 것이 아니라, Exponential Family라는 공통된 수학적 구조를 가진 분포들을 사용한다.**

Exponential Family의 중요한 특징 중 하나는 Natural Parameter $\theta$가 존재하고, 이 자연모수와 평균 $\mu$ 사이의 관계를 체계적으로 표현할 수 있다는 것이다.

Bernoulli 분포의 경우

$$
\theta
=
\log\left(\frac{p}{1-p}\right)
$$

이고,

$$
\mu=p
$$

이므로

$$
\theta
=
\log\left(\frac{\mu}{1-\mu}\right)
$$

가 된다.

그리고 이를 Link Function으로 사용하면 바로 Logit Link가 된다.

따라서

$$
\boxed{
Bernoulli
\rightarrow
Exponential\ Family
\rightarrow
Natural\ Parameter
\rightarrow
Logit
}
$$

이라는 연결관계를 이해할 수 있다.