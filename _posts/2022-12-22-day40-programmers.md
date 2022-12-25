---
title:  "프로그래머스 Lv.1 Day 39"
excerpt: "자바(java) - 2016년"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-12-23
last_modified_at: 2022-12-23
---

#### 40. 2016년


- **문제 설명** 

2016년 1월 1일은 금요일입니다. 2016년 a월 b일은 무슨 요일일까요? 두 수 a ,b를 입력받아 2016년 a월 b일이 무슨 요일인지 리턴하는 함수, solution을 완성하세요. 요일의 이름은 일요일부터 토요일까지 각각 `SUN,MON,TUE,WED,THU,FRI,SAT`

입니다. 예를 들어 a=5, b=24라면 5월 24일은 화요일이므로 문자열 "TUE"를 반환하세요.


- **제한 사항**

2016년은 윤년입니다.
2016년 a월 b일은 실제로 있는 날입니다. (13월 26일이나 2월 45일같은 날짜는 주어지지 않습니다)


- **입출력 예**

|**a**|**b**|**b**|
|:---:|:---:|:---:|
|5|24|"TUE"|




- **My Solution**

```java
class Solution {
    public String solution(int a, int b) {
        String answer = "";
        
        String [] day = {"FRI", "SAT", "SUN", "MON", "TUE", "WED", "THU"};
        int [] lastday = {31,29,31,30,31,30,31,31,30,31,30,31};
        
        int date = 0;
        
        for(int i=0; i<a-1; i++) {
            date += lastday[i];
        }
        
        date += b-1;
        
        return answer = day[date%7];
    }
}
```

⭐2016년으로 연도가 정해져있으므로 요일, 매월 마지막일자를 배열로 선언해서 문제를 풀었다. 몇번째 날인지 저장할 변수를 선언하고 for문을 통해 월별 마지막 날 수의 합을 구해줬다. 그리고 a-1달까지의 일 수 + a달의 일 수를 해주고 일수%7로 요일을 구해서 리턴해줬다.


**프로그래머스 Lv.1 Day 40 2016년 - 자바(java)**