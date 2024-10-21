---
title: 카카오 프로그래머스 기출문제
description: '2023 KAKAO BLIND RECRUITMENT 기출 문제 첫 번째 문제 - 개인정보 수집 유효기간' 풀어보기
author: braelyn
date: 2024-10-21 22:09:57 +0900
categories: [기술블로그, 놀이터기록]
tags: [프로그래머스, 기출, KAKAO BLIND RECRUITMENT, 코테, 코딩테스트]
render_with_liquid: false
---

## 문제에 대해
2023 KAKAO BLIND RECRUITMENT 기출 문제 첫 번째 문제는 '[**개인정보 수집 유효기간**](https://school.programmers.co.kr/learn/courses/30/lessons/150370)'이다.
문제 설명은 굉장히 길지만 핵심은 간단하다. 문자열을 다루고 날짜 계산하는 것이다.
제한 사항도 많아서 복잡해 보이는데 입출력 예시를 보면서 하나씩 체크해 두면 된다.


## 생각 과정
날짜 계산하고 비교하는 것은 아무래도 가장 작은 단위인 '일'로 전환하고 비교하는 것이 가장 간단하다고 판단했다.
주어진 날짜들은 '.'으로 자르면 년/월/일을 구할 수 있고, 그다음으로 '일'로 계산하면 된다.

그리고 'terms'는 나중에 빈번으로 참고해야 해서 시간복잡도도 줄이고자 dictionary로 전환해야겠다는 생각이 든다.

제한사항과 입출력을 보면서 중요한 포인트들을 적어본다.
    - privacies 번호/순서를 기록 필요
    - 1 <= 약관 종류 <= 20
    - 1 <= 약관 기간(달) <= 100
    - 1 <= 약관 수 <= 100
    - 월/일은 두 자릿수
    - 2000 <= 연도 <= 2022
    - 한 달은 28일
    - 예: 1월 1일 + 5개월은 6월 1일 아니고 5월 28일

채결된 약관의 기간을 오늘 날짜와 비교하고 그 기간이 짧거나 같으면 만료된 약관이니 파기해야 한다. 그 약관의 서수를 return해야 한다.

## 코드

```python
# 날짜 배열을 자르고 총 일수로 계산
def date_to_days(date):
    y, m, d = map(int, date.split("."))
    days = y * 12 * 28 + m * 28 + d

    return days

def solution(today, terms, privacies):
    result = []

    # 오늘의 날짜로 총 일수를 계산하는 함수 호출
    tdy_days = date_to_days(today)

    # 'terms'를 dictionary로 전환 -> {약관 종류(t[0:1]): 약관 기간 일수(int(t[2:]) * 28)}
    terms_dict = {}
    for t in terms:
        terms_dict[t[0:1]] = int(t[2:]) * 28

    signed_seq = 0  # 약관 서수 추적
    for p in privacies:
        signed_seq += 1     #몇번째 약관
        signed_days = date_to_days(p[0:10])     #약관 채결 날짜로 총 일수를 계산하는 함수 호출
        signed_type = p[11:12]      # 약관 종류 추출
        term_len = terms_dict[signed_type]      # 'terms' dictionary에서 약관 기한 추출
        exp_days = signed_days + term_len       # 약관 기한 계산
        
        # 약관 기한과 오늘 비교, 짧거나 같으면 파기해야 하니 result 베열에 약관 서수를 기입
        if exp_days <= tdy_days:
            result.append(signed_seq)

    return result
```

