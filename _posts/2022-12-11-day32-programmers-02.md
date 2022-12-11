---
title:  "프로그래머스 Lv.1 Day 32"
excerpt: "자바(java) - 시저 암호"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-12-11
last_modified_at: 2022-12-11
---

#### 32. 시저 암호


- **문제 설명** 

어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다. 예를 들어 "AB"는 1만큼 밀면 "BC"가 되고, 3만큼 밀면 "DE"가 됩니다. "z"는 1만큼 밀면 "a"가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.

- **제한 사항**

공백은 아무리 밀어도 공백입니다.
s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.
s의 길이는 8000이하입니다.
n은 1 이상, 25이하인 자연수입니다.

- **입출력 예**


|**s**|**n**|**result**|
|:---:|:---:|:---:|
|"AB"|1|"BC"|
|"z"|1|"a"|
|"a B z"|4|"e F d"|


- **My Solution**

```java
class Solution {
    public String solution(String s, int n) {
        String answer = "";
        char [] ch = s.toCharArray();
        
        for(int i=0; i<ch.length; i++) {
            
            if(ch[i]>='a' && ch[i]<='z') {
                ch[i] += n;
                if(ch[i]>'z') {
                    ch[i] -= 26;
                }
            }else if(ch[i]>='A' && ch[i]<='Z') {
                ch[i] += n;
                if(ch[i]>'Z') {
                    ch[i] -= 26;
                }
            }
            answer += ch[i];
        }
        return answer;
    }
}
```

⭐문자형 배열을 하나 만들어서 문자열 s의 값들을 넣어준다. for문에서는 소문자, 대문자인 경우 n단계에 맞춰 n칸 밀려진 값이 저장된다. 'z'와 'Z'를 넘어갈 경우에는 -26을 해주었다. 'z'와 'Z'를 넘어가면 각각 91, 122 값이니 -26을 해주면 다시 'a'와 'A'가 된다.


**프로그래머스 Lv.1 Day 32 시저 암호 - 자바(java)**