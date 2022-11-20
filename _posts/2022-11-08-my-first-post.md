---
title:  "프로그래머스 Lv.1 Day 1"
excerpt: "자바 - 짝수와 홀수 "

categories:
  - 프로그래머스
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-08
last_modified_at: 2022-11-08
---

#### 1. 짝수와 홀수


- **문제 설명** 

정수 num이 짝수일 경우 "Even"을 반환하고 홀수인 경우 "Odd"를 반환하는 함수, solution을 완성해주세요.

- **제한 조건**

num은 int 범위의 정수입니다.
0은 짝수입니다.

- **입출력 예**

|**num**|**return**|
|:---:|:---:|
|3|"Odd"|
|4|"Even"|

- **My Solution**

```java
class Solution {
    public String solution(int num) {
        
        if(num%2==0){
            String answer = "Even";
            return answer;
        }else {
            String answer = "Odd";
            return answer;
        }
    }
}
```
 if-else 문을 사용하여 num이 2로 나누었을 때 나머지가 0이되면  

**"Even" 짝수**, 0이 아니라면 **"Odd" 홀수**가 표시된다.

- **Other Solution**

```java
class Solution {
  public String solution(int num) {
    return num % 2 == 0 ? "Even" : "Odd";
  }
}
```

삼항 연산자를 사용하여 조건문(num % 2)이 **'참'이면 "Even"**  

**'거짓'이면 "Odd"** 가 표시된다.

   
   


삼항연산자를 사용시 코드가 조금 더 간결해질 수 있으나 if문에 비해서 속도가 빠른 것은 아니다. 가독성을 해치지 않으면서 코드가 간결해지는 경우에 사용하는 것이 바람직하다.