---
title:  "프로그래머스 Lv.1 Day 29"
excerpt: "자바(java) - 같은 숫자는 싫어 "

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-12-07
last_modified_at: 2022-12-07
---

#### 29. 같은 숫자는 싫어


- **문제 설명** 

배열 arr가 주어집니다. 배열 arr의 각 원소는 숫자 0부터 9까지로 이루어져 있습니다. 이때, 배열 arr에서 연속적으로 나타나는 숫자는 하나만 남기고 전부 제거하려고 합니다. 단, 제거된 후 남은 수들을 반환할 때는 배열 arr의 원소들의 순서를 유지해야 합니다. 예를 들면,

arr = [1, 1, 3, 3, 0, 1, 1] 이면 [1, 3, 0, 1] 을 return 합니다.
arr = [4, 4, 4, 3, 3] 이면 [4, 3] 을 return 합니다.
배열 arr에서 연속적으로 나타나는 숫자는 제거하고 남은 수들을 return 하는 solution 함수를 완성해 주세요.

- **제한 사항**

배열 arr의 크기 : 1,000,000 이하의 자연수
배열 arr의 원소의 크기 : 0보다 크거나 같고 9보다 작거나 같은 정수

- **입출력 예**

|**arr**|**answer**|
|:---:|:---:|
|[1,1,3,3,0,1,1]|[1,3,0,1]|
|[4,4,4,3,3]|[4,3]|

입출력 예 #1,2
문제의 예시와 같습니다.


- **My Solution**

```java
import java.util.*;

public class Solution {
    public int[] solution(int []arr) {
        List<Integer> arrlist = new ArrayList<Integer>();
        int value = -1;
        
        for(int num : arr) {
            if(value != num){
                arrlist.add(num);
            }
            value = num;
        }
        int[] answer = new int[arrlist.size()];
        for(int i=0; i<answer.length; i++) {
            answer[i] = arrlist.get(i);
        }
        
        return answer;
    }
}
```

⭐리스트를 만들어주고 정수형 변수를 선언하여 첫번째 값으로 의미없는 숫자를 넣어줬습니다. 이제 첫번째 배열에서는 arr배열의 모든 값과 비교하여 겹치지 않는 숫자를 list에 추가해줍니다. 두번째 배열에서는 list길이만큼의 answer배열에 값을 차례대로 추가해주었습니다.


**프로그래머스 Lv.1 Day 29 같은 숫자는 싫어 - 자바(java)**