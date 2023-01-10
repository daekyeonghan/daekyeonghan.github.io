---
title:  "프로그래머스 Lv.1 Day 51"
excerpt: "자바(java) - 키패드 누르기"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2023-01-08
last_modified_at: 2023-01-08
---

#### 50. 콜라 문제


- **문제 설명** 

스마트폰 전화 키패드의 각 칸에 다음과 같이 숫자들이 적혀 있습니다.
![keypad](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/4b69a271-5f4a-4bf4-9ebf-6ebed5a02d8d/kakao_phone1.png)

이 전화 키패드에서 왼손과 오른손의 엄지손가락만을 이용해서 숫자만을 입력하려고 합니다.
맨 처음 왼손 엄지손가락은 * 키패드에 오른손 엄지손가락은 # 키패드 위치에서 시작하며, 엄지손가락을 사용하는 규칙은 다음과 같습니다.

1. 엄지손가락은 상하좌우 4가지 방향으로만 이동할 수 있으며 키패드 이동 한 칸은 거리로 1에 해당합니다.

2. 왼쪽 열의 3개의 숫자 `1, 4, 7`을 입력할 때는 왼손 엄지손가락을 사용합니다.

3. 오른쪽 열의 3개의 숫자 `3, 6, 9`를 입력할 때는 오른손 엄지손가락을 사용합니다.

4. 가운데 열의 4개의 숫자 `2, 5, 8, 0`을 입력할 때는 두 엄지손가락의 현재 키패드의 위치에서 더 가까운 엄지손가락을 사용합니다.

4-1. 만약 두 엄지손가락의 거리가 같다면, 오른손잡이는 오른손 엄지손가락, 왼손잡이는 왼손 엄지손가락을 사용합니다.

순서대로 누를 번호가 담긴 배열 numbers, 왼손잡이인지 오른손잡이인 지를 나타내는 문자열 hand가 매개변수로 주어질 때, 각 번호를 누른 엄지손가락이 왼손인 지 오른손인 지를 나타내는 연속된 문자열 형태로 return 하도록 solution 함수를 완성해주세요.

- **제한사항**

numbers 배열의 크기는 1 이상 1,000 이하입니다.

numbers 배열 원소의 값은 0 이상 9 이하인 정수입니다.

hand는 "left" 또는 "right" 입니다.

"left"는 왼손잡이, "right"는 오른손잡이를 의미합니다.

왼손 엄지손가락을 사용한 경우는 L, 오른손 엄지손가락을 사용한 경우는 R을 순서대로 이어붙여 문자열 형태로 return 해주세요.

- **입출력 예**

|**numbers**|**hand**|**result**|
|:---:|:---:|:---:|
|[1, 3, 4, 5, 8, 2, 1, 4, 5, 9, 5]|"right"|"LRLLLRLLRRL"|
|[7, 0, 8, 2, 8, 3, 1, 5, 7, 6, 2]|"left"|"LRLLRRLLLRR"|
|[1, 2, 3, 4, 5, 6, 7, 8, 9, 0]|"right"|"LLRLLRLLRL"|



<table class="table">
        <thead><tr>
<th>numbers</th>
<th>hand</th>
<th>result</th>
</tr>
</thead>
        <tbody><tr>
<td>[1, 3, 4, 5, 8, 2, 1, 4, 5, 9, 5]</td>
<td><code>&quot;right&quot;</code></td>
<td><code>&quot;LRLLLRLLRRL&quot;</code></td>
</tr>
<tr>
<td>[7, 0, 8, 2, 8, 3, 1, 5, 7, 6, 2]</td>
<td><code>&quot;left&quot;</code></td>
<td><code>&quot;LRLLRRLLLRR&quot;</code></td>
</tr>
<tr>
<td>[1, 2, 3, 4, 5, 6, 7, 8, 9, 0]</td>
<td><code>&quot;right&quot;</code></td>
<td><code>&quot;LLRLLRLLRL&quot;</code></td>
</tr>
</tbody>
      </table>
<h5><strong>입출력 예에 대한 설명</strong></h5>

<p><strong>입출력 예 #1</strong></p>

<p>순서대로 눌러야 할 번호가 [1, 3, 4, 5, 8, 2, 1, 4, 5, 9, 5]이고, 오른손잡이입니다.</p>
<table class="table">
        <thead><tr>
<th>왼손 위치</th>
<th>오른손 위치</th>
<th>눌러야 할 숫자</th>
<th>사용한 손</th>
<th>설명</th>
</tr>
</thead>
        <tbody><tr>
<td>*</td>
<td>#</td>
<td>1</td>
<td>L</td>
<td>1은 왼손으로 누릅니다.</td>
</tr>
<tr>
<td>1</td>
<td>#</td>
<td>3</td>
<td>R</td>
<td>3은 오른손으로 누릅니다.</td>
</tr>
<tr>
<td>1</td>
<td>3</td>
<td>4</td>
<td>L</td>
<td>4는 왼손으로 누릅니다.</td>
</tr>
<tr>
<td>4</td>
<td>3</td>
<td>5</td>
<td>L</td>
<td>왼손 거리는 1, 오른손 거리는 2이므로 왼손으로 5를 누릅니다.</td>
</tr>
<tr>
<td>5</td>
<td>3</td>
<td>8</td>
<td>L</td>
<td>왼손 거리는 1, 오른손 거리는 3이므로 왼손으로 8을 누릅니다.</td>
</tr>
<tr>
<td>8</td>
<td>3</td>
<td>2</td>
<td>R</td>
<td>왼손 거리는 2, 오른손 거리는 1이므로 오른손으로 2를 누릅니다.</td>
</tr>
<tr>
<td>8</td>
<td>2</td>
<td>1</td>
<td>L</td>
<td>1은 왼손으로 누릅니다.</td>
</tr>
<tr>
<td>1</td>
<td>2</td>
<td>4</td>
<td>L</td>
<td>4는 왼손으로 누릅니다.</td>
</tr>
<tr>
<td>4</td>
<td>2</td>
<td>5</td>
<td>R</td>
<td>왼손 거리와 오른손 거리가 1로 같으므로, 오른손으로 5를 누릅니다.</td>
</tr>
<tr>
<td>4</td>
<td>5</td>
<td>9</td>
<td>R</td>
<td>9는 오른손으로 누릅니다.</td>
</tr>
<tr>
<td>4</td>
<td>9</td>
<td>5</td>
<td>L</td>
<td>왼손 거리는 1, 오른손 거리는 2이므로 왼손으로 5를 누릅니다.</td>
</tr>
<tr>
<td>5</td>
<td>9</td>
<td>-</td>
<td>-</td>
<td></td>
</tr>
</tbody>
      </table>

- **My Solution**

```java
class Solution {
    public String solution(int[] numbers, String hand) {
        String answer = "";
        StringBuilder sb = new StringBuilder();
        
        int left = 10;
        int right = 12;
        
        for(int i = 0; i < numbers.length; i++) {
            int n = numbers[i];
            
            if(n == 1 || n == 4 || n == 7) {
                left = n;
                sb.append("L");
            }
            if(n == 3 || n == 6 || n == 9) {
                right = n;
                sb.append("R");
            }
            if(n == 2 || n == 5 || n == 8 || n == 0) {
                if(n == 0)
                    n = 11;
                
                int leftDiff = (Math.abs(n-left) / 3) + (Math.abs(n-left) % 3);
                int rightDiff = (Math.abs(n-right) / 3) + (Math.abs(n-right) % 3);
                
                if(leftDiff == rightDiff) {
                    if(hand.equals("right")) {
                        right = n;
                        sb.append("R");
                    }else{
                        left = n;
                        sb.append("L");
                    }  
                }else if(leftDiff > rightDiff) {
                    right = n;
                    sb.append("R");
                }else {
                    left = n;
                    sb.append("L");
                }
            }
        }
        return answer = sb.toString();
    }
}
```

⭐ 문자열을 계속 추가해주는 연산이 필요한데 String과 String을 계속 연산하게 되면 성능저하를 일으킬 수 있어서 StringBuilder를 활용하였다.

처음에 왼손은 *, 오른손은 #에 위치하고 있기 때문에 각각 10, 12로 초기화한다.

number가 0일 때는 11로 변환 후 시작한다.

number % 3 한 값이 1이면 왼손으로 누르고, 2이면 가까운 손 그리고 0이면 오른손으로 눌러준다.

왼손 - 1 또는 오른손 - 0 의 경우에는 손의 위치를 초기화한 후 왼손이면 L, 오른손이면 R을 append 한다. 

`번호와의 거리 =((현재번호-누를번호) % 3) + ((현재번호-누를번호) / 3)`

**프로그래머스 Lv.1 Day 51 키패드 누르기 - 자바(java)**