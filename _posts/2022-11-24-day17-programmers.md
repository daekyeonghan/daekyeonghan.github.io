---
title:  "프로그래머스 Lv.1 Day 17"
excerpt: "자바(java) - 제일 작은 수 제거하기"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-24
last_modified_at: 2022-11-24
---

#### 17. 제일 작은 수 제거하기



- **문제 설명** 

정수를 저장한 배열, arr 에서 가장 작은 수를 제거한 배열을 리턴하는 함수, solution을 완성해주세요. 단, 리턴하려는 배열이 빈 배열인 경우엔 배열에 -1을 채워 리턴하세요. 예를들어 arr이 [4,3,2,1]인 경우는 [4,3,2]를 리턴 하고, [10]면 [-1]을 리턴 합니다.

- **제한 사항**

arr은 길이 1 이상인 배열입니다.
인덱스 i, j에 대해 i ≠ j이면 arr[i] ≠ arr[j] 입니다.




- **입출력 예**

|**arr**|**return**|
|:---:|:---:|
|[4,3,2,1]|[4,3,2]|
|[10]|[-1]|


- **My Solution**

```java
class Solution {
    public int[] solution(int[] arr) {
        int num = arr.length;
        int[] answer = new int[num - 1];
        int j = 0;

        if (arr.length < 2) {
            return new int[]{-1};
        }

        for (int i = 1; i < num; i++) {
            if (arr[j] > arr[i]) {
                j = i;
            }
        }

        for (int i = 0; i < num - 1; i++) {
            if (i < j) {
                answer[i] = arr[i];
            }else {
                answer[i] = arr[i + 1];
            }
        }

        return answer;
    }
}
```

⭐배열의 길이가 1인경우 -1을 리턴하는 조건을 먼저 써주고 첫번째 for문을 통해 바로 다음 순서의 값과 비교하여 최솟값을 찾아 j에 저장해준다. 두번째 for문에서는 최솟값이 나오기 전까지는 그대로 값을 넣어주고 최솟값이 나오게되면 그때부터는 다음번의 인덱스 값부터 값을 넣어준다.



**프로그래머스 Lv.1 Day 17 제일 작은 수 제거하기 - 자바(java)**