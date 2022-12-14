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

|**숫자**|**영단어**|
|:---:|:---:|
|0|zero|
|1|one|
|2|two|
|3|three|
|4|four|
|5|five|
|6|six|
|7|seven|
|8|eight|
|9|nine|




- **제한 사항**
1 ≤ s의 길이 ≤ 50
s가 "zero" 또는 "0"으로 시작하는 경우는 주어지지 않습니다.
return 값이 1 이상 2,000,000,000 이하의 정수가 되는 올바른 입력만 s로 주어집니다.


- **입출력 예**

|**s**|**result**|
|:---:|:---:|
|"one4seveneight"|1478|
|"23four5six7"|234567|
|"2three45sixseven"|234567|
|"123"|123|

입출력 예 설명
입출력 예 #1

문제 예시와 같습니다.
입출력 예 #2

문제 예시와 같습니다.
입출력 예 #3

"three"는 3, "six"는 6, "seven"은 7에 대응되기 때문에 정답은 입출력 예 #2와 같은 234567이 됩니다.
입출력 예 #2와 #3과 같이 같은 정답을 가리키는 문자열이 여러 가지가 나올 수 있습니다.
입출력 예 #4

s에는 영단어로 바뀐 부분이 없습니다.


- **My Solution**

```java
class Solution {
    public int solution(String s) {
        int answer = 0;
        String [] words = {"zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine"};
        
        for(int i=0; i<words.length; i++) {
            
            s = s.replaceAll(words[i], Integer.toString(i));
        }
        
        return answer = Integer.parseInt(s);
    }
}
```

⭐ replaceAll() 메소드를 이용하여 숫자를 나타내는 영단어를 숫자로 바꾸어줬다.
Integer.toString() 메소드로 정수형 i값을 문자형으로 변경해줬고, 다시 answer 반환에서 Integer.parseInt() 메소드로 정수형으로 변경해줬다.

`String replaceAll(String regex, String replacement)`
문자열 내에 있는 정규식 regex와 매치되는 모든 문자열을 replacement 문자열로 바꾸고
그 문자열이 반환된다.

`String replace(char oldChar, char newChar)`
문자열내에 있는 모든 oldChar를 newChar로 바꾼 문자열을 반환한다.

- 숫자 -> 문자 변환

|**자료형**|**메소드**|
|:---:|:---:|
|Int|Integer.toString|
|Float|Float.toString|
|Double|Double.toString|
|Long|Long.toString|

- 문자 -> 숫자 변환

|**자료형**|**메소드**|
|:---:|:---:|
|Int|Integer.parseInt|
|Float|Float.parseFloat|
|Double|Double.parseDouble|
|Long|Long.parseLong|

**프로그래머스 Lv.1 Day 37 숫자 문자열과 영단어 - 자바(java)**