---
title:  "프로그래머스 Lv.1 Day 26"
excerpt: "자바(java) - 행렬의 덧셈 "

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-12-04
last_modified_at: 2022-12-04
---

#### 26. 행렬의 덧셈


- **문제 설명** 

행렬의 덧셈은 행과 열의 크기가 같은 두 행렬의 같은 행, 같은 열의 값을 서로 더한 결과가 됩니다. 2개의 행렬 arr1과 arr2를 입력받아, 행렬 덧셈의 결과를 반환하는 함수, solution을 완성해주세요.

- **제한 사항**

행렬 arr1, arr2의 행과 열의 길이는 500을 넘지 않습니다.

- **입출력 예**

|**arr1**|**arr2**|**arr2**|
|:---:|:---:|:---:|
|[1,2],[2,3]|[3,4],[5,6]|[4,6],[7,9]|
|[1],[2]|[3],[4]|[4],[6]|



- **My Solution**

```java
class Solution {
    public int[][] solution(int[][] arr1, int[][] arr2) {
        int[][] answer = new int[arr1.length][arr1[0].length];
        
        for(int i=0; i<arr1.length; i++) {
            for(int j=0; j<arr1[0].length; j++) {
                answer[i][j] = arr1[i][j] + arr2[i][j];
            }
        }
        
        return answer;
    }
}
```

⭐이중 for문으로 같은 인덱스의 값끼리 더해줬습니다

- **Other Solution**

```java
class Solution {
    public int[][] solution(int[][] arr1, int[][] arr2) {
        int[][] answer = {};
        answer = arr1;
        for(int i=0; i<arr1.length; i++){
            for(int j=0; j<arr1[0].length; j++){
                answer[i][j] += arr2[i][j];
            }
        }
        return answer;
    }
}
```

⭐ 두 배열의 길이가 같기때문에 answer을 arr1로 해줘도 될것같다. 합부분 코드도 좀 더 간단해진다.


**프로그래머스 Lv.1 Day 26 행렬의 덧셈 - 자바(java)**