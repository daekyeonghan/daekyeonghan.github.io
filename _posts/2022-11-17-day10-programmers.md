---
title:  "프로그래머스 Lv.1 Day 10"
excerpt: "자바(java) - 정수 내림차순으로 배치하기"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-17
last_modified_at: 2022-11-17
---

#### 10. 정수 내림차순으로 배치하기




- **문제 설명** 

함수 solution은 정수 n을 매개변수로 입력받습니다. n의 각 자릿수를 큰것부터 작은 순으로 정렬한 새로운 정수를 리턴해주세요. 예를들어 n이 118372면 873211을 리턴하면 됩니다.

- **제한 사항**

`n`은 1이상 8000000000 이하인 자연수입니다.

- **입출력 예**

|**n**|**return**|
|:---:|:---:|
|118372|873211|



- **My Solution**

```java
class Solution {
    public long solution(long n) {
        long answer = 0;
        char temp = 0;
        String str = Long.toString(n);
        char [] arr = str.toCharArray();
        
        for(int i=0; i<arr.length; i++) {
            for(int j=0; j<arr.length; j++) {
                if(arr[j] < arr[i]) {
                    temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
        }
        String str2 = new String();
        for(int i=0; i<arr.length; i++) {
            str2 += arr[i];
        }
        return answer = Long.parseLong(str2);
    }
}
```
long n값을 문자열로 먼저 변경해주고 다시 그 문자열을 문자형 배열에 넣어줬다. 그 배열의 첫번째 값과 바로 그 옆 인덱스의 값과 서로 비교해주면서 큰 값이 쪽으로 오게 정렬해줬다. 다시 정렬된 배열을 문자열로 만들고 그 문자열을 long형으로 변환해주고 리턴해줬다.


⭐

- **Other Solution**

```java
import java.util.*;

class Solution {
    public long solution(long n) {
        String[] arr = Long.toString(n).split("");
        
        Arrays.sort(arr, Collections.reverseOrder());
        
        StringBuilder sb = new StringBuilder();
        
        for(String i : arr) {
            sb.append(i);
        }
        
        return Long.parseLong(sb.toString());
    }
}
```
n값을 split을 이용해 하나씩 배열에 저장, 컬렉션 리버스오더를 이용해 내림차순으로 정렬함, StringBuilder를 사용해 하나씩 넣어주고 다시 long 형으로 변환해준다.

⭐

**프로그래머스 Lv.1 Day 10 정수 내림차순으로 배치하기 - 자바(java)**