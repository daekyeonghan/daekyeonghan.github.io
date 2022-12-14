---
title:  "프로그래머스 Lv.1 Day 31"
excerpt: "자바(java) - 3진법 뒤집기"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-12-09
last_modified_at: 2022-12-09
---

#### 31. 3진법 뒤집기


- **문제 설명** 

자연수 n이 매개변수로 주어집니다. n을 3진법 상에서 앞뒤로 뒤집은 후, 이를 다시 10진법으로 표현한 수를 return 하도록 solution 함수를 완성해주세요.

- **제한 사항**

n은 1 이상 100,000,000 이하인 자연수입니다.

- **입출력 예**

|**n**|**result**|
|:---:|:---:|
|45|7|
|125|229|

입출력 예 #1

답을 도출하는 과정은 다음과 같습니다.

|**n(10진법)**|**n(3진법)**|**n(3진법)**|**n(3진법)**|
|:---:|:---:|:---:|:---:|
|45|1200|0021|7|

따라서 7을 return 해야 합니다.


입출력 예 #2

답을 도출하는 과정은 다음과 같습니다.

|**n(10진법)**|**n(3진법)**|**n(3진법)**|**n(3진법)**|
|:---:|:---:|:---:|:---:|
|125|11122|22111|229|

따라서 229를 return 해야 합니다.


- **My Solution**

```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        String three = "";
        
        while(n != 0) {
            three += n%3;
            n /= 3;
        }
        return answer = Integer.parseInt(three,3);
    }
}
```

⭐ n 값이 0이 아닐때까지 반복 계산하여 3진수로 만들어준다. Integer.parseInt 메소드를 사용하면 10진수로 변환된다.


**프로그래머스 Lv.1 Day 31 3진법 뒤집기 - 자바(java)**