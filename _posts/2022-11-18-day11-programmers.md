---
title:  "프로그래머스 Lv.1 Day 11"
excerpt: "자바(java) - 나머지가 1이 되는 수 찾기"

categories:
  - 프로그래머스
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-18
last_modified_at: 2022-11-18
---

#### 11. 나머지가 1이 되는 수 찾기




- **문제 설명** 

자연수 n이 매개변수로 주어집니다. n을 x로 나눈 나머지가 1이 되도록 하는 가장 작은 자연수 x를 return 하도록 solution 함수를 완성해주세요. 답이 항상 존재함은 증명될 수 있습니다.

- **제한 사항**

3 ≤ n ≤ 1,000,000

- **입출력 예**

|**n**|**return**|
|:---:|:---:|
|10|3|
|12|11|



- **My Solution**

```java
class Solution {
    public int solution(int n) {
        int [] arr = new int[n];
        int answer = 0;
        
        for(int x=1; x<=n; x++) {
            if(n%x == 1) {
                arr[x-1] = x;
                answer = arr[x-1];
                break;
            }
        }
        return answer;
    }
}
```
배열을 만들어 n값을 x로 나누었을 때 나머지가 1인 x 중에서 가장 작은 값이 가장 먼저 배열에 들어갈 것이기 때문에 배열의 가장 첫번째 값을 리턴해줬다.

⭐

- **Other Solution**

```java
class Solution {
    public int solution(int n) {
        int answer = 0;

        for(int i =1; i<n; i++) {
            if(n%i==1) {
                answer = i;
                break;
            }
        }
        return answer;
    }
}

```


⭐

**프로그래머스 Lv.1 Day 11 나머지가 1이 되는 수 찾기 - 자바(java)**