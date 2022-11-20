---
title:  "프로그래머스 Lv.1 Day 12"
excerpt: "자바(java) - 두 정수 사이의 합"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-19
last_modified_at: 2022-11-19
---

#### 12. 두 정수 사이의 합




- **문제 설명** 

두 정수 a, b가 주어졌을 때 a와 b 사이에 속한 모든 정수의 합을 리턴하는 함수, solution을 완성하세요.
예를 들어 a = 3, b = 5인 경우, 3 + 4 + 5 = 12이므로 12를 리턴합니다.

- **제한 사항**

a와 b가 같은 경우는 둘 중 아무 수나 리턴하세요.
a와 b는 -10,000,000 이상 10,000,000 이하인 정수입니다.
a와 b의 대소관계는 정해져있지 않습니다.

- **입출력 예**

|**a**|**b**|**return**|
|:---:|:---:|:---:|
|3|5|12|
|3|3|3|
|5|3|12|



- **My Solution**

```java
class Solution {
    public long solution(int a, int b) {
        long answer = 0;
        if(a>b) {
            for(long i=a; i>=b; i--) {
                    answer += i;
            }
        }else {
                for(long j=a; j<=b; j++ ) {
                    answer += j;
            }
        }
        return answer;
    }
}
```
⭐a가 b보다 큰 경우도 있으니 if-else문으로 구현했다.



- **Other Solution**

```java
class Solution {
  public long solution(int a, int b) {
      long answer = 0;
      for (int i = ((a < b) ? a : b); i <= ((a < b) ? b : a); i++) 
          answer += i;

      return answer;
  }
}
```
⭐for문에도 삼항연산자를 사용할 수 있다는것을 배웠다.


**프로그래머스 Lv.1 Day 12 두 정수 사이의 합 - 자바(java)**