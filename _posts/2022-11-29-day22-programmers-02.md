---
title:  "프로그래머스 Lv.1 Day 22"
excerpt: "자바(java) - 문자열 내림차순으로 배치하기 "

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-29
last_modified_at: 2022-11-29
---

#### 23. 내적


- **문제 설명** 

문자열 s에 나타나는 문자를 큰것부터 작은 순으로 정렬해 새로운 문자열을 리턴하는 함수, solution을 완성해주세요.
s는 영문 대소문자로만 구성되어 있으며, 대문자는 소문자보다 작은 것으로 간주합니다.

- **제한 사항**

str은 길이 1 이상인 문자열입니다.

- **입출력 예**

|**s**|**return**|
|:---:|:---:|
|"Zbcdefg"|"gfedcbZ"|


- **My Solution**

```java
import java.util.*;
class Solution {
    public String solution(String s) {
        String answer = "";
        char [] ch = s.toCharArray();
        Arrays.sort(ch);
        
        for(int i=ch.length-1; i>=0; i--) {
            answer += ch[i];
        }
        
        return answer;
    }
}
```
⭐ 문자형 배열을 선언하고 문자열 s의 값들을 넣어준다. 오름차순 정렬 메소드를 사용해 오름차순으로 정렬해주고 for문을 통해 다시 역순으로 answer에 넣어줘 반환했다.

- **Other Solution**

```java
class Solution {
    public String solution(String s) {
        char[] ch = s.toCharArray();
        Arrays.sort(ch);
        return new StringBuilder(new String(ch)).reverse().toString();
    }
}
```
⭐ StringBuilder를 사용하여 오름차순 정렬된ch배열을 reverse() 메소드로 역순으로 정렬해주고 toString() 메소드로 모든 요소를 출력해줬다.

**프로그래머스 Lv.1 Day 22 문자열 내림차순으로 배치하기 - 자바(java)**