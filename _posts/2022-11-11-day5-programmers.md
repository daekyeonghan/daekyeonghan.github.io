---
title:  "프로그래머스 Lv.1 Day 5"
excerpt: "자바(java) - 자연수 뒤집어 배열로 만들기 "

categories:
  - 프로그래머스
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-11
last_modified_at: 2022-11-11
---

#### 5. 자연수 뒤집어 배열로 만들기


- **문제 설명** 

자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴해주세요. 예를들어 n이 12345이면 [5,4,3,2,1]을 리턴합니다.

- **제한 사항**

n은 10,000,000,000이하인 자연수입니다.

- **입출력 예**

|**n**|**return**|
|:---:|:---:|
|12345|[5,4,3,2,1]|



- **My Solution**

```java
class Solution {
    public int[] solution(long n) {
        int i=0;
        String str=""+n;
        
        int[] answer =new int[str.length()];
        
        while(n>0) {
            answer[i]=(int)(n%10); 
            n/=10;
             i++;
        }
        return answer;
    } 
}
```
n값을 문자열에 저장해주고 그 길이만큼 인덱스가 들어갈 배열을 만들어준다
n값을 10으로 나눈 나머지값들을 각 자릿수에 넣어준다
이미 넣은 자릿수는 없애주기 위해 10으로 나눠준다

⭐제한사항에도 나와있듯이 n 값의 자료형은 long이다
자료형에도 신경을 써줘야 한다. 


- **Other Solution**

```java
class Solution {
    public int[] solution(long n) {
        String str = String.valueOf(n); 
        int[] answer = new int[str.length()]; 
        int count = 0; 

        while (n > 0) {
            answer[count] = (int) (n % 10); 
            n /= 10;
            count++;
        }
        return answer;
    }
}
```

같은 방식이지만 valueOf로 형변환을 해주니 처리속도가 엄청 빨라졌다.

**프로그래머스 Lv.1 Day 5 자연수 뒤집어 배열로 만들기 - 자바(java)**