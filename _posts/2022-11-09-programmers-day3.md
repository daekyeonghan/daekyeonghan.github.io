---
title:  "프로그래머스 Lv.1 Day 3"
excerpt: "자바 - 약수의 합 "

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-09
last_modified_at: 2022-11-09
---

#### 3. 약수의 합


- **문제 설명** 

정수 n을 입력받아 n의 약수를 모두 더한 값을 리턴하는 함수, solution을 완성해주세요.

- **제한 사항**

n은 0 이상 3000이하인 정수입니다.

- **입출력 예**

|**n**|**return**|
|:---:|:---:|
|12|28|
|5|6|

입출력 예 
12의 약수는 1, 2, 3, 4, 6, 12입니다.    이를 모두 더하면 28입니다.

입출력 예 
5의 약수는 1, 5입니다. 이를 모두 더하면 6입니다.

- **My Solution**

```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        int sum = 0;
        
        for(int i=1; i<=n; i++) {
            if(n%i==0) {
                sum += i;
            }
        }
        return answer = sum;  
    }
}
```
for문을 이용해 입력받은 값과 같아질 때까지 i값을 증가시킨다   
이 때 입력받은 값을 1씩 증가되는 i값으로 나누었을 때   
나머지가 0이 되는 수가 입력받은 수의 약수가 된다.

ex)
n의 값이 6이면 나눌 값 i는 1~6의 수가 된다.   
나누었을 때 나머지가 0인 수는   
1(O), 2(O), 3(O), 4, 5, 6(O) 이다.   
n의 약수는 1,2,3,6 이므로   
sum 변수에 더해주면서 저장된다.   
결과값은 12가 나온다.   



- **Other Solution**

```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        
        for(int i = 1; i <= n/2; i++) {
          if(n%i == 0) {
            answer += i;
            }
            return answer+n;
            }
        }
    }

```

제한사항에 써져있는 것 처럼 n값으로 큰 수가 들어오면
반복 횟수도 같이 커질것이다.
처음부터 들어온 n 값을 반으로 나눠주고 약수를 구해준 다음
반복문이 종료될 때 들어온 n 값을 더해주어
반복횟수를 절반으로 줄일 수 있다.

**프로그래머스 Lv.1 Day 3 약수의 합**