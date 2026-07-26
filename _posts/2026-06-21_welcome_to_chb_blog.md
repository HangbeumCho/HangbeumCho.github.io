---
title: "CHB Blog를 시작합니다"
date: 2026-06-21 00:00:00 +0900
categories:
  - Statistics
  - Hypothesis Testing
tags:
  - Statistics
  - Applied Statistics
  - Data Science
math: true
toc: true
published: false
image: /assets/img/posts/2026-06-21-welcome-to-chb-blog/cover.png
---

이 글은 실제 공개용 글이 아니라, 앞으로 작성할 포스트의 형식과 마크다운 문법을 확인하기 위한 참고용 템플릿입니다.
내용의 정확성보다는 Chirpy/Jekyll에서 어떤 요소들이 어떻게 보이는지 확인하는 데 목적이 있습니다.

## 1. 기본 문단과 강조

통계 분석에서는 **문제 정의**, **데이터 이해**, **모형 선택**, **결과 해석**이 모두 중요합니다.
특히 실무에서는 _완벽한 가정_ 보다 `충분히 쓸 수 있는 근거`를 찾는 과정이 더 자주 등장합니다.

예를 들어 다음과 같은 질문을 생각할 수 있습니다.

- 두 집단의 평균은 정말 다른가?
- 표본 크기가 작을 때 어떤 검정을 선택해야 하는가?
- 독립성 가정이 약간 깨져도 결론은 유지되는가?
- 효과 크기와 p-value를 함께 어떻게 설명할 것인가?

## 2. 체크리스트

분석 글을 작성할 때는 아래 항목을 빠뜨리지 않는 것이 좋습니다.

- [x] 분석 질문을 한 문장으로 정리하기
- [x] 사용한 데이터와 변수 설명하기
- [ ] 가정과 한계 명시하기
- [ ] 재현 가능한 코드 제공하기
- [ ] 시각화와 해석을 함께 제시하기

## 3. 표 예시

| 항목 | 설명 | 예시 |
| --- | --- | --- |
| 모수 | 모집단의 특성값 | 평균, 분산 |
| 통계량 | 표본에서 계산한 값 | 표본평균, 표본분산 |
| 추정량 | 모수를 추정하는 규칙 | $\bar{x}$ |
| 검정통계량 | 가설검정에 사용하는 값 | t-statistic |

## 4. 인용문 예시

> 좋은 분석 글은 계산 결과를 나열하는 데서 끝나지 않고,
> 그 결과가 어떤 의사결정에 연결되는지 설명합니다.

## 5. 코드 블록 예시

Python 코드는 다음처럼 작성할 수 있습니다.

```python
import numpy as np
from scipy import stats

group_a = np.array([12.1, 11.8, 13.0, 12.7, 11.9])
group_b = np.array([10.4, 10.9, 11.2, 10.7, 11.0])

result = stats.ttest_ind(group_a, group_b, equal_var=False)

print(f"t-statistic: {result.statistic:.3f}")
print(f"p-value: {result.pvalue:.3f}")
```

SQL 예시는 다음처럼 넣을 수 있습니다.

```sql
SELECT
  experiment_group,
  COUNT(*) AS n_users,
  AVG(conversion) AS conversion_rate
FROM experiment_result
GROUP BY experiment_group;
```

## 6. 수식 예시

인라인 수식은 표본평균을 $\bar{x}$처럼 표현할 때 사용합니다.

블록 수식은 다음처럼 작성합니다.

$$
\bar{x} = \frac{1}{n}\sum_{i=1}^{n}x_i
$$

Welch의 t-test에서 사용하는 검정통계량은 다음과 같이 쓸 수 있습니다.

$$
t = \frac{\bar{x}_1 - \bar{x}_2}
{\sqrt{\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2}}}
$$

## 7. 이미지 예시

포스트별 이미지는 `assets/img/posts/<post-slug>/` 아래에 저장합니다.

![통계와 데이터 분석을 표현한 추상 이미지](/assets/img/posts/2026-06-21-welcome-to-chb-blog/cover.png)

## 8. 링크와 각주 예시

블로그 저장소는 [GitHub](https://github.com/HangbeumCho)에서 관리할 수 있습니다.
간단한 보충 설명은 각주로 분리할 수 있습니다.[^note]

[^note]: 각주는 본문 흐름을 해치지 않으면서 부가 설명을 남길 때 유용합니다.

## 9. 접기/펼치기 예시

<details>
  <summary>분석 메모 펼치기</summary>

  이 영역에는 긴 설명, 실험 결과, 추가 코드, 참고 메모 등을 넣을 수 있습니다.
  공개 글에서는 핵심 흐름을 방해하지 않는 보조 정보를 담기에 좋습니다.

</details>

## 10. 앞으로 사용할 글 구조

앞으로의 통계/데이터 분석 글은 대략 아래 흐름을 따를 예정입니다.

1. 문제 정의
2. 직관적 설명
3. 수식 또는 이론 정리
4. Python/R/SQL 예제
5. 결과 해석
6. 실무 적용 시 주의점

---

이 포스트는 템플릿 검토용이므로 `published: false` 상태로 유지합니다.
