---
title:  "프로그래머스 Lv.1 Day 7"
excerpt: "자바(java) - 문자열을 정수로 바꾸기 "

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-13
last_modified_at: 2022-11-13
---

#### 7. 문자열을 정수로 바꾸기


- **문제 설명** 

문자열 s를 숫자로 변환한 결과를 반환하는 함수, solution을 완성하세요.

- **제한 사항**

s의 길이는 1 이상 5이하입니다.
s의 맨앞에는 부호(+, -)가 올 수 있습니다.
s는 부호와 숫자로만 이루어져있습니다.
s는 "0"으로 시작하지 않습니다.

- **입출력 예**

예를들어 str이 "1234"이면 1234를 반환하고, "-1234"이면 -1234를 반환하면 됩니다.
str은 부호(+,-)와 숫자로만 구성되어 있고, 잘못된 값이 입력되는 경우는 없습니다.



- **My Solution**

```java
class Solution {
    public int solution(String s) {
        int answer = Integer.parseInt(s);
        return answer;
    }
}
```
Integer클래스의 parseInt() 메서드를 이용해 문자열을 정수로 변환해줬다

⭐

- **Other Solution**

```java
class Solution {
    public int solution(String s) {
        boolean Sign = true;
        int answer = 0;

        for(int i=0; i<s.length(); i++) {
            char ch = s.charAt(i);
            if(ch == '-') {
                Sign = false;
            }else if(ch != '+'){
                answer = answer * 10 + (ch-'0');
            }
        }
        if(Sign==false) {
            answer *= -1;
        }
        return answer;
    }
}
```
알고리즘 방식? 으로 다시 문제를 풀어보면, +- 부호를 판단하기 위한 논리형 변수를 선언해주고 문자열의 길이만큼 반복문을 돌려준다. 문자형 ch 변수에 문자열 s의 처음부터 끝까지 값을 넣어준다. 부호가 아닌 숫자가 온다면 기존의 answer에 10씩 곱해서 자릿수를 늘려 숫자를 넣어준다.
마지막에 Sign 즉 부호가 true(양수)이면 그대로, false(음수)이면 -를 곱해서 return 한다.

⭐

**프로그래머스 Lv.1 Day 7 문자열을 정수로 바꾸기 - 자바(java)**