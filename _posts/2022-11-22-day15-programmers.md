---
title:  "프로그래머스 Lv.1 Day 15"
excerpt: "자바(java) - 핸드폰 번호 가리기"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-22
last_modified_at: 2022-11-22
---

#### 15. 핸드폰 번호 가리기




- **문제 설명** 

프로그래머스 모바일은 개인정보 보호를 위해 고지서를 보낼 때 고객들의 전화번호의 일부를 가립니다.
전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 *으로 가린 문자열을 리턴하는 함수, solution을 완성해주세요.

- **제한 사항**

phone_number는 길이 4 이상, 20이하인 문자열입니다.

- **입출력 예**

|**phone_number**|**return**|
|:---:|:---:|
|"01033334444"|"*******4444"|
|"027778888"|"*****8888"|


- **My Solution**

```java
class Solution {
    public String solution(String phone_number) {
        String answer = "";
        char [] arr = phone_number.toCharArray();
        
        for(int i=0; i<arr.length-4; i++) {
            arr[i] = '*';
        }
        
        return answer = String.valueOf(arr);
    }
}
```

⭐공통적으로 뒷번호 4자리를 제외하고 나머지 숫자가 *로 표시되고 있으니 전화번호의 -4위치 까지 *를 찍어준 후 하나씩 반환해줬다.


- **Other Solution**

```java
class Solution {
  public String solution(String phone_number) {
      String answer = "";

        for (int i = 0; i < phone_number.length() - 4; i++)
            answer += "*";

        answer += phone_number.substring(phone_number.length() - 4);

        return answer;
  }
}
```

⭐ substring()을 이용함 

**프로그래머스 Lv.1 Day 15 핸드폰 번호 가리기- 자바(java)**