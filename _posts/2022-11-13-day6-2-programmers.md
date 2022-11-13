---
title:  "프로그래머스 Lv.1 Day 6"
excerpt: "자바(java) - 문자열 내 p와 y의 개수 "

categories:
  - Blog
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-13
last_modified_at: 2022-11-13
---

#### 6. 문자열 내 p와 y의 개수


- **문제 설명** 

대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True, 다르면 False를 return 하는 solution를 완성하세요. 'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다. 단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.

예를 들어 s가 "pPoooyY"면 true를 return하고 "Pyy"라면 false를 return합니다.

- **제한 사항**

문자열 s의 길이 : 50 이하의 자연수
문자열 s는 알파벳으로만 이루어져 있습니다.


- **입출력 예**

|**s**|**answer**|
|:---:|:---:|
|"pPoooyY"|true|
|"Pyy"|false|

입출력 예 설명
입출력 예 #1
'p'의 개수 2개, 'y'의 개수 2개로 같으므로 true를 return 합니다.

입출력 예 #2
'p'의 개수 1개, 'y'의 개수 2개로 다르므로 false를 return 합니다.



- **My Solution**

```java
class Solution {
    boolean solution(String s) {
        boolean answer = true;
        int pcnt = 0;
        int ycnt = 0;
        
        for(int i=0; i<s.length(); i++) {
            if(s.charAt(i)=='y' || s.charAt(i)=='Y') {
                ycnt++;
            }else if(s.charAt(i)=='p' || s.charAt(i)=='P') {
                pcnt++;
            }
        }
        if(pcnt == ycnt) {
            answer = true;
        }else {
            answer = false;
        }
        return answer;
    }
}
```
문자열의 길이만큼 반복문을 실행해 문자열의 처음부터 끝까지를 탐색할 수 있게 했고 주어진 문자열s에 'p'와 'y'가 있을 때 카운트를 증가시켜줬다.

**프로그래머스 Lv.1 Day 6 문자열 내 p와 y의 개수 - 자바(java)**