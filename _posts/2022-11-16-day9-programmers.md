---
title:  "프로그래머스 Lv.1 Day 9"
excerpt: "자바(java) - x만큼 간격이 있는 n개의 숫자
 "

categories:
  - Blog
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-16
last_modified_at: 2022-11-16
---

#### 9. x만큼 간격이 있는 n개의 숫자



- **문제 설명** 

함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다. 다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.

- **제한 사항**

x는 -10000000 이상, 10000000 이하인 정수입니다.
n은 1000 이하인 자연수입니다.

- **입출력 예**

|**x**|**n**|**answer**|
|:---:|:---:|:---:|
|2|5|[2,4,6,8,10]|
|4|3|[4,8,12]|
|-4|2|[-4, -8]|



- **My Solution**

```java
class Solution {
    public long[] solution(int x, int n) {
        
        long[] answer =new long[n];
        long num = x;
        
        for(int i=0; i<n; i++) {
            
            answer[i] = num*(i+1);
            
        }
        
        return answer;
    }
}
```
배열을 선언해 0번 인덱스 부터 x부터 시작해 x씩 증가하는 값들을 담아줬다.
0번 인덱스부터 값을 넣어야되서 i값은 0부터 시작해줬다. 0과 값을 곱하면 0이 되기때문에 i+1한 값을 num값과 곱해주면서 배열에 담아줬다.


⭐

**프로그래머스 Lv.1 Day 9 x만큼 간격이 있는 n개의 숫자 - 자바(java)**