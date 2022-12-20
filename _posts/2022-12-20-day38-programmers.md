---
title:  "프로그래머스 Lv.1 Day 38"
excerpt: "자바(java) - 두 개 뽑아서 더하기"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-12-20
last_modified_at: 2022-12-20
---

#### 38. 두 개 뽑아서 더하기


- **문제 설명** 

정수 배열 numbers가 주어집니다. numbers에서 서로 다른 인덱스에 있는 두 개의 수를 뽑아 더해서 만들 수 있는 모든 수를 배열에 오름차순으로 담아 return 하도록 solution 함수를 완성해주세요.

- **제한 사항**

numbers의 길이는 2 이상 100 이하입니다.  
numbers의 모든 수는 0 이상 100 이하입니다.


- **입출력 예**

입출력 예 #1

2 = 1 + 1 입니다. (1이 numbers에 두 개 있습니다.)  
3 = 2 + 1 입니다.  
4 = 1 + 3 입니다.  
5 = 1 + 4 = 2 + 3 입니다.  
6 = 2 + 4 입니다.  
7 = 3 + 4 입니다.  
따라서 `[2,3,4,5,6,7]` 을 return 해야 합니다.  

입출력 예 #2

2 = 0 + 2 입니다.  
5 = 5 + 0 입니다.  
7 = 0 + 7 = 5 + 2 입니다.  
9 = 2 + 7 입니다.  
12 = 5 + 7 입니다.  
따라서 `[2,5,7,9,12]` 를 return 해야 합니다.  


- **My Solution**

```java
import java.util.ArrayList;
import java.util.Collections;

class Solution {
    public int[] solution(int[] numbers) {
        int[] answer = {};
        ArrayList<Integer> arrList = new ArrayList<>();
        
        for(int i=0; i<numbers.length; i++) {
            for(int j=i+1; j<numbers.length; j++) {
                if(!arrList.contains(numbers[i]+numbers[j])) {
                    arrList.add(numbers[i]+numbers[j]);
                }
            }
        }
        
        Collections.sort(arrList);
        
        int cnt = 0;
        answer = new int[arrList.size()];
        for(int arr : arrList) {
            answer[cnt++] = arr;
        }
        return answer;
    }
}
```

⭐ArrayList와 Collections를 사용하였다.
contains()메소드를 사용하여 중복된 값을 걸러주고 add()메소드로 리스트에 더한 값들을 넣어줬다. 오름차순정렬해주고 answer배열에 넣어주고 리턴해줬다.

⭐ArrayList
일반 배열과 동일하게 연속된 메모리 공간을 사용하며 인덱스는 0부터 시작한다.
배열은 크기가 고정인 반면 ArrayList는 크기가 가변적으로 변한다.  

기본적인 ArrayList 생성 형태
`ArrayList<Integer> arrList = new ArrayList<Integer>();`

`add()` 메소드로 생성한 List에 값을 추가할 수 있다.
기본적으로 리스트의 가장 끝에 값을 추가한다, 별도로 인덱스를 지정하면 해당 인덱스에 값이 추가되고 그 인덱스부터의 값들이 1칸씩 밀려난다.

`set()` 기존에 리스트에 추가돼있는 값을 변경할 때 사용하는 메소드

`remove()` 기존에 리스트에 추가돼있는 값을 삭제할 때 사용하는 메소드

`clear()` ArrayList 안의 내용을 전체 삭제할 때 사용하는 메소드

`get()` 각 인덱스의 값을 순차적으로 탐색할 때 사용하는 메소드

`contains()` 값이 존재하는지 확인할 때 사용하는 메소드
값이 있는 경우 true, 값이 없는 경우 false를 리턴한다.

`indexOf()` 값이 어느 위치에 존재하는지 , 인덱스값을 리턴하는 메소드
값이 존재하지 않을 경우에는 -1을 리턴한다.

⭐ArrayList 정렬

`Collections.sort(list)`
ArrayList를 오름차순으로 정렬할 때

`Collections.sort(list, Collections.reverseOrder())`
ArrayList를 내림차순으로 정렬할 때


**프로그래머스 Lv.1 Day 38 두 개 뽑아서 더하기 - 자바(java)**