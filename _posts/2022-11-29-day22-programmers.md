---
title:  "프로그래머스 Lv.1 Day 22"
excerpt: "자바(java) - 내적 "

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-29
last_modified_at: 2022-11-29
---

#### 22. 내적


- **문제 설명** 

길이가 같은 두 1차원 정수 배열 a, b가 매개변수로 주어집니다. a와 b의 내적을 return 하도록 solution 함수를 완성해주세요.

이때, a와 b의 내적은 a[0]*b[0] + a[1]*b[1] + ... + a[n-1]*b[n-1] 입니다. (n은 a, b의 길이)

- **제한 사항**

a, b의 길이는 1 이상 1,000 이하입니다.
a, b의 모든 수는 -1,000 이상 1,000 이하입니다.

- **입출력 예**

|**a**|**b**|**result**|
|:---:|:---:|:---:|
|"[1,2,3,4]"|"[-3,-1,0,2]"|"3"|
|"[-1,0,1]	"|"[1,0,-1]	"|"-2"|

입출력 예 #1

a와 b의 내적은 1*(-3) + 2*(-1) + 3*0 + 4*2 = 3 입니다.

입출력 예 #2

a와 b의 내적은 (-1)*1 + 0*0 + 1*(-1) = -2 입니다.


- **My Solution**

```java
class Solution {
    public int solution(int[] a, int[] b) {
        int answer = 0;
        int len = a.length;
        for(int i=0; i<len; i++ ) {
            answer += a[i]*b[i];
        }
        return answer;
    }
}
```
⭐ 두 배열의 모든 값들을 순서대로 곱해준 뒤 더해주는 것
a와 b 배열의 길이는 같다.

**프로그래머스 Lv.1 Day 22 내적 - 자바(java)**