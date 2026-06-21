---
layout: post
title: "블로그를 시작합니다"
date: 2026-06-21
---

통계, 데이터 과학, 그리고 실무 분석 과정에서 배운 내용을 기록하기 위해 블로그를 시작합니다.

## Markdown 예시

Markdown에서는 다음과 같이 내용을 구성할 수 있습니다.

- 목록 항목
- **굵은 글씨**
- [GitHub](https://github.com/)

## Python 코드 블록 예시

```python
def mean(values):
    return sum(values) / len(values)


samples = [1, 2, 3, 4, 5]
print(mean(samples))
```

## 수식 예시

표본 평균은 다음과 같이 표현할 수 있습니다.

$$
\bar{x} = \frac{1}{n}\sum_{i=1}^{n}x_i
$$

## 이미지 삽입 예시

아래 경로에 `sample.png` 파일을 추가하면 이미지가 표시됩니다.

![샘플 이미지]({{ "/assets/images/sample.png" | relative_url }})
