---
title:  "프로그래머스 Lv.1 Day 21"
excerpt: "자바(java) - 수박수박수박수박수박수? "

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-28
last_modified_at: 2022-11-28
---

#### 21. 수박수박수박수박수박수?


- **문제 설명** 

길이가 n이고, "수박수박수박수...."와 같은 패턴을 유지하는 문자열을 리턴하는 함수, solution을 완성하세요. 예를들어 n이 4이면 "수박수박"을 리턴하고 3이라면 "수박수"를 리턴하면 됩니다.

- **제한 사항**

n은 길이 10,000이하인 자연수입니다.

- **입출력 예**

|**n**|**return**|
|:---:|:---:|
|"3"|"수박수"|
|"4"|"수박수박"|



- **My Solution**

```java
class Solution {
    public String solution(int n) {
        int key = n/2;
        String answer = "";
        
        if(n%2==0) {
            for(int i=0; i<key; i++) {
                answer += "수박";
            }
        }else {
            for(int j=0; j<key; j++) {
                 answer += "수박";
            }
            answer += "수";
        }
        return answer;
    }
}
```

⭐ for문으로 n번째까지 처음부터 '수'로 시작해서 입력받은 n값 번째까지 출력해주면 되지만 처리시간을 줄여보고자 key값을 선언해서 그 값에 n값을 2로 나눈 값을 넣어줬다. 그렇게 되면 n값이 짝수인 경우에는 key값의 갯수만큼 '수박'을 출력해주면되고, 홀수인 경우에는 짝수와 똑같이 출력해주고 맨 마지막 글자에만 '수'를 추가해주면 된다. 

- **Other Solution**

```java
class Solution {
    public String solution(int n) {
        String answer = "";
        for(int i=0; i<n; i++) {
          answer += i % 2 == 0 ? "수" : "박" ;
        }
        return answer;
    }
}
```
⭐ 처음 생각한대로 코드를 짜보면 이런식으로 짜볼 수 있겠다!


**프로그래머스 Lv.1 Day 21 수박수박수박수박수박수? - 자바(java)**