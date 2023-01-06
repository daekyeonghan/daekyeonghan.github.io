---
title:  "프로그래머스 Lv.1 Day 47"
excerpt: "자바(java) - 로또의 최고 순위와 최저 순위"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2023-01-06
last_modified_at: 2023-01-06
---

#### 47. 로또의 최고 순위와 최저 순위




- **문제 설명** 

로또 6/45(이하 '로또'로 표기)는 1부터 45까지의 숫자 중 6개를 찍어서 맞히는 대표적인 복권입니다. 아래는 로또의 순위를 정하는 방식입니다.

![20230106_225008_1](https://user-images.githubusercontent.com/117332830/211025436-77e76411-b484-4bf9-8290-d27e75766767.png)

로또를 구매한 민우는 당첨 번호 발표일을 학수고대하고 있었습니다. 하지만, 민우의 동생이 로또에 낙서를 하여, 일부 번호를 알아볼 수 없게 되었습니다. 당첨 번호 발표 후, 민우는 자신이 구매했던 로또로 당첨이 가능했던 최고 순위와 최저 순위를 알아보고 싶어 졌습니다.
알아볼 수 없는 번호를 0으로 표기하기로 하고, 민우가 구매한 로또 번호 6개가 `44, 1, 0, 0, 31 25`라고 가정해보겠습니다. 당첨 번호 6개가 `31, 10, 45, 1, 6, 1`9`라면, 당첨 가능한 최고 순위와 최저 순위의 한 예는 아래와 같습니다.

![20230106_225008_2](https://user-images.githubusercontent.com/117332830/211025422-b01f6cf5-d6b1-4d7a-b94d-29f67aab8992.png)

순서와 상관없이, 구매한 로또에 당첨 번호와 일치하는 번호가 있으면 맞힌 걸로 인정됩니다.
알아볼 수 없는 두 개의 번호를 각각 10, 6이라고 가정하면 3등에 당첨될 수 있습니다.
3등을 만드는 다른 방법들도 존재합니다. 하지만, 2등 이상으로 만드는 것은 불가능합니다.
알아볼 수 없는 두 개의 번호를 각각 11, 7이라고 가정하면 5등에 당첨될 수 있습니다.
5등을 만드는 다른 방법들도 존재합니다. 하지만, 6등(낙첨)으로 만드는 것은 불가능합니다.
민우가 구매한 로또 번호를 담은 배열 lottos, 당첨 번호를 담은 배열 win_nums가 매개변수로 주어집니다. 이때, 당첨 가능한 최고 순위와 최저 순위를 차례대로 배열에 담아서 return 하도록 solution 함수를 완성해주세요.


- **제한사항**

lottos는 길이 6인 정수 배열입니다.

lottos의 모든 원소는 0 이상 45 이하인 정수입니다.

0은 알아볼 수 없는 숫자를 의미합니다.

0을 제외한 다른 숫자들은 lottos에 2개 이상 담겨있지 않습니다.

lottos의 원소들은 정렬되어 있지 않을 수도 있습니다.

win_nums은 길이 6인 정수 배열입니다.

win_nums의 모든 원소는 1 이상 45 이하인 정수입니다.

win_nums에는 같은 숫자가 2개 이상 담겨있지 않습니다.

win_nums의 원소들은 정렬되어 있지 않을 수도 있습니다.

- **입출력 예**

![20230106_225008_3](https://user-images.githubusercontent.com/117332830/211025408-ee300120-c64b-45a2-a9c5-d324c166a832.png)

입출력 예 #1

문제 예시와 같습니다.

입출력 예 #2

알아볼 수 없는 번호들이 아래와 같았다면, 1등과 6등에 당첨될 수 있습니다.

![20230106_225008_4](https://user-images.githubusercontent.com/117332830/211025389-5fc2a9db-9d06-4117-970d-5235ba94ac90.png)

입출력 예 #3

민우가 구매한 로또의 번호와 당첨 번호가 모두 일치하므로, 최고 순위와 최저 순위는 모두 1등입니다.

- **My Solution**

```java
class Solution {
    public int[] solution(int[] lottos, int[] win_nums) {
        int[] answer = new int [2];
        int win = 0;
        int zero = 0;
        
        for(int i : lottos) {
            if(i == 0) {
                zero++;
            }else {
                for(int j : win_nums) {
                    if(i == j) {
                        win++;
                        break;
                    }
                }
            }
        }
        
        answer[0] = (win+zero) > 1 ? 7 - (win+zero) : 6;
        answer[1] = win > 1 ? 7-win : 6;
        return answer;
        
    }
}
```

⭐ 답을 맞춘 수의 갯수를 담을 변수 win과 알아볼 수 없는 수의 갯수를 담을 변수 zero를 선언해준다. for문으로 알아볼 수 없는 수의 갯수를 증가시켜줬고, 답과 맞는 수가 있을 경우에는 win을 증가시켜줬다. 그리고 최고 순위를 구하는 코드`(win+zero) > 1 ? 7 - (win+zero) : 6` 와 최저 순위를 구하는 코드 `win > 1 ? 7 - win : 6` 을 작성해주고 반환해주었다.

- **Other Solution**

```java
class Solution {
    public int[] solution(int[] lottos, int[] win_nums) {
        int zero = 0;
        int matched = 0;
        for (int l : lottos) {
            if (l == 0) {
                zero++;
            } else {
                for (int w : win_nums) {
                    if (l == w) {
                        matched++;
                        break;
                    }
                }
            }
        }
        int min = matched;
        int max = matched + zero;
        int[] answer = {Math.min(7 - max, 6), Math.min(7 - min, 6)};
        return answer;
    }
}
```

⭐ 최고순위와 최저순위를 Math.min() 메소드를 사용하여 구해주었다.

**프로그래머스 Lv.1 Day 47 로또의 최고 순위와 최저 순위 - 자바(java)**