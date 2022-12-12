---
title:  "프로그래머스 Lv.1 Day 33"
excerpt: "자바(java) - [1차] 비밀지도"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-12-12
last_modified_at: 2022-12-12
---

#### 33. [1차] 비밀지도


- **문제 설명** 

#### 비밀지도

네오는 평소 프로도가 비상금을 숨겨놓는 장소를 알려줄 비밀지도를 손에 넣었다. 그런데 이 비밀지도는 숫자로 암호화되어 있어 위치를 확인하기 위해서는 암호를 해독해야 한다. 다행히 지도 암호를 해독할 방법을 적어놓은 메모도 함께 발견했다.

지도는 한 변의 길이가 n인 정사각형 배열 형태로, 각 칸은 "공백"(" ") 또는 "벽"("#") 두 종류로 이루어져 있다.
전체 지도는 두 장의 지도를 겹쳐서 얻을 수 있다. 각각 "지도 1"과 "지도 2"라고 하자. 지도 1 또는 지도 2 중 어느 하나라도 벽인 부분은 전체 지도에서도 벽이다. 지도 1과 지도 2에서 모두 공백인 부분은 전체 지도에서도 공백이다.
"지도 1"과 "지도 2"는 각각 정수 배열로 암호화되어 있다.
암호화된 배열은 지도의 각 가로줄에서 벽 부분을 1, 공백 부분을 0으로 부호화했을 때 얻어지는 이진수에 해당하는 값의 배열이다.

<p align="center"><img src="https://user-images.githubusercontent.com/117332830/207055353-26364cf2-f856-4b3e-afd4-0f1d5bf83740.png" height="100%" width="300%"></p>


- **입력 형식**

입력으로 지도의 한 변 크기 n 과 2개의 정수 배열 arr1, arr2가 들어온다.

1 ≦ n ≦ 16
arr1, arr2는 길이 n인 정수 배열로 주어진다.
정수 배열의 각 원소 x를 이진수로 변환했을 때의 길이는 n 이하이다. 즉, 0 ≦ x ≦ 2n - 1을 만족한다.

- **출력 형식**

원래의 비밀지도를 해독하여 '#', 공백으로 구성된 문자열 배열로 출력하라.

<p align="center"><img src="https://user-images.githubusercontent.com/117332830/207056182-d033bfd8-eb51-4b9a-a4a7-e01627b86510.png" height="100%" width="300%"></p>


- **My Solution**

```java
class Solution {
    public String[] solution(int n, int[] arr1, int[] arr2) {
        String[] answer = new String[n];
        
        for(int i=0; i<n; i++) {
            String str1 = Integer.toBinaryString(arr1[i]);
            String str2 = Integer.toBinaryString(arr2[i]);
            String map = "";
            
            while(str1.length() < n) {
                str1 = "0"+str1;
            }
            
            while(str2.length() < n) {
                str2 = "0"+str2;
            }
            for(int j=0; j<n; j++) {
                if(str1.charAt(j) == '1' || str2.charAt(j) == '1') {
                    map += '#';
                }else {
                    map += " ";
                }
            }
            answer[i] = map;
        }
        
        return answer;
    }
}
```

⭐10진법 숫자로 주어진 배열을 각 값마다 2진법으로 변경해주고 새로운 문자열을 만들어 넣어준다. toBinaryString() 메소드를 사용하면 10진법 숫자를 2진법으로 변경해줄 수 있다. 2진법으로 변경했을 때 변의 길이보다 작다면 0을 추가해주어 변의 길이와 맞춰준다. 두 값을 비교해주고 #과 공백으로 바꾸어주고 바뀐 값들을 answer배열에 넣어주면 마무리된다.


**프로그래머스 Lv.1 Day 33. [1차] 비밀지도 - 자바(java)**