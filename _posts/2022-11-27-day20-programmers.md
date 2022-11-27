---
title:  "프로그래머스 Lv.1 Day 20"
excerpt: "자바(java) - 가운데 글자 가져오기 "

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-27
last_modified_at: 2022-11-27
---

#### 20. 가운데 글자 가져오기


- **문제 설명** 

단어 s의 가운데 글자를 반환하는 함수, solution을 만들어 보세요. 단어의 길이가 짝수라면 가운데 두글자를 반환하면 됩니다.

- **제한 사항**

s는 길이가 1 이상, 100이하인 스트링입니다.

- **입출력 예**

|**s**|**return**|
|:---:|:---:|
|"abcde"|"c"|
|"qwer"|"we"|



- **My Solution**

```java
class Solution {
    public String solution(String s) {
        String answer = "";
        int num = s.length() /2;
        
        if(s.length() % 2 == 0) {
            answer = s.substring(num-1, num+1);
        }else{
            answer = s.substring(num, num+1);
        }
        return answer;
    }
}
```

⭐문자열 s의 길이가 홀수인 경우에는 2로 나누었을 때 나눈 인덱스 값의 +1번째, 짝수인 경우에는 2로 나누었을 때 -1번째 값과 그 다음 값이 반환되는것으로 생각하고 문제를 풀었다. substring함수의 입력된 인자값이 2개이면 첫번째 값은 가져올 문자열의 처음 시작 부분을 지정하고, 두번째 값은 끝나는 값을 나타내며 만약 그 값이 12라면 11번째까지의 값을 가져올 수 있다.


**프로그래머스 Lv.1 Day 20 가운데 글자 가져오기 - 자바(java)**