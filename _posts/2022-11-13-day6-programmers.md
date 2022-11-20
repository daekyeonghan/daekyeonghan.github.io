---
title:  "프로그래머스 Lv.1 Day 6"
excerpt: "자바(java) - 정수 제곱근 판별 "

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-13
last_modified_at: 2022-11-13
---

#### 6. 정수 제곱근 판별


- **문제 설명** 

임의의 양의 정수 n에 대해, n이 어떤 양의 정수 x의 제곱인지 아닌지 판단하려 합니다.
n이 양의 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, n이 양의 정수 x의 제곱이 아니라면 -1을 리턴하는 함수를 완성하세요.

- **제한 사항**

n은 1이상, 50000000000000 이하인 양의 정수입니다.

- **입출력 예**

|**n**|**return**|
|:---:|:---:|
|121|3|
|3|-1|

입출력 예#1
121은 양의 정수 11의 제곱이므로, (11+1)를 제곱한 144를 리턴합니다.

입출력 예#2
3은 양의 정수의 제곱이 아니므로, -1을 리턴합니다.



- **My Solution**

```java
class Solution {
    public long solution(long n) {
        long answer = 0;
        
        for(long x=1; x<=n; x++) {
            if(x*x == n){
               answer = (x+1)*(x+1);
                break;
            }else {
                answer = -1;
            }
        }
        return answer;
        }        
    }
```
for문을 통해 x값을 1씩 증가시켜주면서 들어온 n값과 x의 제곱근 값이
같은 경우 어떤 양의 정수 x의 제곱인지 판별할 수 있게 했다

⭐제한사항에도 나와있듯이 n 값의 자료형은 long이다
자료형에도 신경을 써줘야 한다. 



**프로그래머스 Lv.1 Day 6 정수 제곱근 판별 - 자바(java)**