---
title:  "프로그래머스 Lv.1 Day 30"
excerpt: "자바(java) - 이상한 문자 만들기"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-12-09
last_modified_at: 2022-12-09
---

#### 30. 이상한 문자 만들기


- **문제 설명** 

문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 각 단어는 하나 이상의 공백문자로 구분되어 있습니다. 각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.

- **제한 사항**

문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.
첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.

- **입출력 예**

|**s**|**return**|
|:---:|:---:|
|"try hello world"|"TrY HeLlO WoRlD"|

"try hello world"는 세 단어 "try", "hello", "world"로 구성되어 있습니다. 각 단어의 짝수번째 문자를 대문자로, 홀수번째 문자를 소문자로 바꾸면 "TrY", "HeLlO", "WoRlD"입니다. 따라서 "TrY HeLlO WoRlD" 를 리턴합니다.


- **My Solution**

```java
class Solution {
    public String solution(String s) {
        String answer = "";
        String [] str = s.split("");
        int num = 0;
        
        for(int i=0; i<s.length(); i++) {
            if(str[i].equals(" ")) {
                num = 0;
            }else if(num % 2 == 0) {
                str[i] = str[i].toUpperCase();
                ++num;
            }else if(num % 2 != 0){
                str[i] = str[i].toLowerCase();
                ++num;
            }
            answer += str[i];
        }
        return answer;
    }
}
```

⭐문자열 배열을 선언해 문자열 s를 split()메소드를 이용해서 문자 한개씩 뽑아서 그 배열에 넣어준다. for문을 만들어서 문자열 s의 길이만큼 반복하고 그 전에 홀수, 짝수를 판별할 정수형 변수 num을 선언해준다. if-elseif 문을통해서 짝수인 경우에는 toUpperCase()메소드를 이용해서 대문자로 변환, 홀수인 경우에는 toLowerCase()메소드를 이용하여 소문자로 변환한다. 


**프로그래머스 Lv.1 Day 30 이상한 문자 만들기 - 자바(java)**