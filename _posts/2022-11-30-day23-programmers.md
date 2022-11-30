---
title:  "프로그래머스 Lv.1 Day 23"
excerpt: "자바(java) - 문자열 다루기 기본 "

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-30
last_modified_at: 2022-11-30
---

#### 23. 문자열 다루기 기본


- **문제 설명** 

문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, solution을 완성하세요. 예를 들어 s가 "a234"이면 False를 리턴하고 "1234"라면 True를 리턴하면 됩니다.

- **제한 사항**

`s`는 길이 1 이상, 길이 8 이하인 문자열입니다.
`s`는 영문 알파벳 대소문자 또는 0부터 9까지 숫자로 이루어져 있습니다.

- **입출력 예**

|**s**|**return**|
|:---:|:---:|
|"a234"|false|
|"1234"|true|



- **My Solution**

```java
class Solution {
    public boolean solution(String s) {
        boolean answer = true;
        
        if(s.length() !=4 && s.length() !=6) 
            return false;
        
        for(int i= 0; i<s.length(); i++) {
            if(s.charAt(i) < '0' || s.charAt(i) > '9')
                return false;
        }
        return answer;
    }
}
```

⭐ 먼저 문자열 s의 길이가 4와 6이 맞는지 판단해줬다. 그 후 for문에서는 OR연산자를 사용해 숫자만 있는 문자열이 있다면 초기화 값인 true가 반환되고, 문자열이 한개라도 있다면 false가 반환되게 구현해줬다.

- **Other Solution**

```java
class Solution {
    public boolean solution(String s) {
        if((s.length()==4 || s.length()==6)) {
            try {
                int x = Integer.parseInt(s);
                return true;
                
            }catch(NumberFormatException e) {
                return false;
        }
        else return false;
        }
    }
}

```
⭐ 문자열 s 전체를 정수형으로 변환할 때 예외가 발생하지 않으면 true, 예외가 발생하면 false를 반환해주는 코드다.. 예외처리를 사용하는 방법은 생각하지 못했는데 정말 괜찮은 방법인 것 같다.


**프로그래머스 Lv.1 Day 23 문자열 다루기 기본 - 자바(java)**