---
title:  "프로그래머스 Lv.1 Day 13"
excerpt: "자바(java) - 콜라츠 추측"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-20
last_modified_at: 2022-11-20
---

#### 13. 콜라츠 추측




- **문제 설명** 

1937년 Collatz란 사람에 의해 제기된 이 추측은, 주어진 수가 1이 될 때까지 다음 작업을 반복하면, 모든 수를 1로 만들 수 있다는 추측입니다. 작업은 다음과 같습니다.

`1-1. 입력된 수가 짝수라면 2로 나눕니다.`
`1-2. 입력된 수가 홀수라면 3을 곱하고 1을 더합니다.`
`2. 결과로 나온 수에 같은 작업을 1이 될 때까지 반복합니다.`

예를 들어, 주어진 수가 6이라면 6 → 3 → 10 → 5 → 16 → 8 → 4 → 2 → 1 이 되어 총 8번 만에 1이 됩니다. 위 작업을 몇 번이나 반복해야 하는지 반환하는 함수, solution을 완성해 주세요. 단, 주어진 수가 1인 경우에는 0을, 작업을 500번 반복할 때까지 1이 되지 않는다면 –1을 반환해 주세요.


- **제한 사항**

입력된 수, num은 1 이상 8,000,000 미만인 정수입니다.

- **입출력 예**

|**n**|**result**|
|:---:|:---:|
|6|8|
|16|4|
|626331|-1|



- **My Solution**

```java
class Solution {
    public int solution(long num) {
        int answer = 0;
        long value = (long)num;
        
        while(value != 1) {
            if(value == 1) {
                break;
            }else if(answer>=500){
                answer = -1;
                break;
            }
            if(value%2 == 0) {
                value/=2;
            }else {
                value = (value*3)+1;
            }
            answer++;
        }
         return answer;
    }
}
```
⭐1이 될때까지 무한반복을 시켜주고, 1이 됐을때와 500번 반복해도 1이 안됐을 때 반복문을 빠져나올 수 있게 먼저 짜주었다. 1이 될 때까지 반복한 횟수를 반환시켜주면 되니 횟수를 하나씩 증가해줬다.



- **Other Solution**

```java
```
⭐

**프로그래머스 Lv.1 Day 13 콜라츠 추측 - 자바(java)**