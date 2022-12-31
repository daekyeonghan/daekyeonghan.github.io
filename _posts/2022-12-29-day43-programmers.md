---
title:  "프로그래머스 Lv.1 Day 43"
excerpt: "자바(java) - 소수 찾기"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-12-29
last_modified_at: 2022-12-29
---

#### 43. 소수 찾기


- **문제 설명** 

1부터 입력받은 숫자 n 사이에 있는 소수의 개수를 반환하는 함수, solution을 만들어 보세요.

소수는 1과 자기 자신으로만 나누어지는 수를 의미합니다.
(1은 소수가 아닙니다.)


- **제한 사항**

n은 2이상 1000000이하의 자연수입니다.

- **입출력 예**

|**n**|**result**|
|:---:|:---:|
|10|4|
|5|3|

입출력 예 #1

1부터 10 사이의 소수는 [2,3,5,7] 4개가 존재하므로 4를 반환

입출력 예 #2

1부터 5 사이의 소수는 [2,3,5] 3개가 존재하므로 3를 반환


- **My Solution**

```java
class Solution {
    public int solution(int n) {
        int answer = 1;
        boolean chk = true;

        for (int i = 3; i <= n; ++i) {
            for (int j = 2; j < i; ++j) {
                if (i % j == 0) {
                    chk = false;
                    break;
                }
            }
            if (chk) ++answer;
            chk = true;
        }

        return answer;
    }
}
```

⭐ n까지의 값까지 확인하며 해당 값이 어떠한 값 - 해당 값보다 작은수 -로 나누었을 때 0으로 나눠 떨어지는지 아닌지 확인하는것인데 테스트는 통과하였으나, 결국 시간초과로 효율성 테스트에 실패하였다.. 제한 조건을 확인하니 수가 1,000,000이라 그랬던것 ㅜ

- **Other Solution**

```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        int[] arr = new int[n + 1];

        for (int i = 2; i <= (int) Math.sqrt(n); ++i) {
            if (arr[i] == 1) continue;
            for (int j = i + i; j <= n; j += i) {
                arr[j] = 1;
            }
        }
        
        for (int i = 2; i < arr.length; ++i) {
            if (arr[i] != 1) ++answer;
        }

        return answer;
    }
}
```

⭐ 문제의 해결법을 찾지 못하여 검색해본 결과 에라토스테네스의 체를 사용하여 푸는게 맞다고 판단하였다.

에라토스테네스의 체
https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4

소수가 아닌경우 불필요한 반복문을 실행하지 않기 위해 continue를 실행한다.
j를 i+i 부터 시작하여 n까지 증가시킨다. 증감식을 j = j+i로 하여 i의 배수를 체크하도록한다.

**프로그래머스 Lv.1 Day 43 소수 찾기 - 자바(java)**