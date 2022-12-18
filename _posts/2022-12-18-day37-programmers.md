---
title:  "프로그래머스 Lv.1 Day 37"
excerpt: "자바(java) - 숫자 문자열과 영단어"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-12-18
last_modified_at: 2022-12-18
---

#### 37. 숫자 문자열과 영단어


- **문제 설명** 

![img1](https://user-images.githubusercontent.com/117332830/208301054-1cd77d10-adb6-479e-ab04-3db59ee79d8e.png)

네오와 프로도가 숫자놀이를 하고 있습니다. 네오가 프로도에게 숫자를 건넬 때 일부 자릿수를 영단어로 바꾼 카드를 건네주면 프로도는 원래 숫자를 찾는 게임입니다.

다음은 숫자의 일부 자릿수를 영단어로 바꾸는 예시입니다.

1478 → "one4seveneight"
234567 → "23four5six7"
10203 → "1zerotwozero3"
이렇게 숫자의 일부 자릿수가 영단어로 바뀌어졌거나, 혹은 바뀌지 않고 그대로인 문자열 s가 매개변수로 주어집니다. s가 의미하는 원래 숫자를 return 하도록 solution 함수를 완성해주세요.

참고로 각 숫자에 대응되는 영단어는 다음 표와 같습니다.

|**array**|**commands**|
|:---:|:---:|
|0|zero|
|0|zero|
|0|zero|
|0|zero|
|0|zero|
|0|zero|
|0|zero|
|0|zero|
|0|zero|




- **제한 사항**
|**array**|**commands**|**return**|
|:---:|:---:|:---:|
|[1, 5, 2, 6, 3, 7, 4]|[ [2, 5, 3], [4, 4, 1], [1, 7, 3] ]|[5, 6, 3]|


- **입출력 예**





- **My Solution**

```java
import java.util.Arrays;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
        
        for(int i=0; i<commands.length; i++) {
            int [] tmp = new int[commands[i][1] - (commands[i][0]-1)];
            for(int j=0; j<tmp.length; j++) {
                tmp[j] = array[j + (commands[i][0]-1)];
            }
            Arrays.sort(tmp);
            answer[i] = tmp[commands[i][2]-1];
        }
        return answer;
    }
}
```

⭐
입출력 예의 2차원 commands 배열을 보기쉽게 풀어써봤다.
```
[0][0], [0][1], [0][2]
2        5       3

[1][0], [1][1], [1][2]
4        4       1

[2][0], [2][1], [2][2]
1        7       3
```
2중 반복문을 만들어줬고, 반복문이 실행되는동안 값이 저장되어야 할 int형 배열을 하나 만들어준다. 이때 배열의 크기는 `commands[i][1] - (commands[i][0]-1)` 크기가된다.
만들어둔 tmp 배열에 array값을 조건대로 뽑아준 뒤 sort() 메소드로 정렬해주었다. 여기서 2차원배열의 `[0][2], [1][2], [2][2]`  번째 값이 가리키는 순서의 값을 뽑아줘 answer배열에 넣어주면된다.

- **Other Solution**

```java
import java.util.Arrays;
class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];

        for(int i=0; i<commands.length; i++){
            int[] temp = Arrays.copyOfRange(array, commands[i][0]-1, commands[i][1]);
            Arrays.sort(temp);
            answer[i] = temp[commands[i][2]-1];
        }

        return answer;
    }
}
```

⭐copyOfRange() 메소드를 사용하였다. `[ Arrays.copyOfRange(복사하고자하는 배열, 시작 위치, 배열크기); ]`로 선언해주면 되며, 주의할 점은 복사되는 배열은 시작 위치부터 배열크기 바로 전까지 복사된다는 점. 시작위치를 `commands[i][0]-1`로 해주고 배열의 크기를 `commands[i][1]`로 선언해줬다.


**프로그래머스 Lv.1 Day 36 K번째수 - 자바(java)**