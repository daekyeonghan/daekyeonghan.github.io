---
title:  "프로그래머스 Lv.1 Day 16"
excerpt: "자바(java) - 나누어 떨어지는 숫자 배열"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-23
last_modified_at: 2022-11-23
---

#### 16. 나누어 떨어지는 숫자 배열


- **문제 설명** 

array의 각 element 중 divisor로 나누어 떨어지는 값을 오름차순으로 정렬한 배열을 반환하는 함수, solution을 작성해주세요.
divisor로 나누어 떨어지는 element가 하나도 없다면 배열에 -1을 담아 반환하세요.

- **제한 사항**


arr은 자연수를 담은 배열입니다.
정수 i, j에 대해 i ≠ j 이면 arr[i] ≠ arr[j] 입니다.
divisor는 자연수입니다.
array는 길이 1 이상인 배열입니다
{: .notice--info} 



- **입출력 예**

|**phone_number**|**return**|**return**|
|:---:|:---:|:---:|
|[5, 9, 7, 10]"|5|[5, 10]|
|[2, 36, 1, 3]|1|[1, 2, 3, 36]|
|[3,2,6]|10|[-1]|


- **My Solution**

```java
import java.util.Arrays;

class Solution {
    public int[] solution(int[] arr, int divisor) {
        int cnt = 0;
        int num = 0;
        
        for(int i=0; i<arr.length; i++) {
            if(arr[i]%divisor == 0) {
                cnt++;
            }
        }
        
        if(cnt==0) {
            int[] answer = {-1};
            return answer;
        }
        
        int [] answer = new int[cnt];
        
        for(int i=0; i<arr.length; i++) {
            if(arr[i]%divisor == 0) {
                answer[num] = arr[i];
                num++;
                }
            }
        
        Arrays.sort(answer);
        return answer;
    }
}
```

⭐


- **Other Solution**

```java

```

⭐ 

**프로그래머스 Lv.1 Day 16 나누어 떨어지는 숫자 배열 - 자바(java)**