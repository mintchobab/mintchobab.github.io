---
title: "백준 2839번 : 설탕 배달 C# 문제풀이"

categories:
  - Algorithm Baekjoon
tags:
  - [Algorithm]

toc: true
toc_sticky: true

date: 2021-10-25
last_modified_at: 2021-10-25
---

## 문제

[문제링크](https://www.acmicpc.net/problem/2839)

<p align="center">
  <img src="/assets/images/algorithm/baekjoon/2893-1.JPG" title="그림 1" />
</p>

<br>

## 풀이

<br>

나올 수 있는 경우의 수는 총 4가지다.
1. 5kg, 3kg 봉지를 모두 사용한 경우
2. 5kg 봉지만 사용한 경우
3. 3kg 봉지만 사용한 경우
4. 나누어 떨어지지 않은 경우 (-1 출력)

1,2,3번의 경우 5kg이 3kg보다 많아야 하기 때문에 먼저 5로 나누어서 나머지가 0인 경우를 찾는다. 나머지가 0이라면 그대로 종료하고 0이 아니라면 3kg 봉지를 무조건 1개 이상을 사용하는 경우기 때문에 3kg 봉지의 개수를 1개씩 더해준다.<br>

반복해서 진행하다보면 5로 나누어 떨어질 때가 있는데 그 때의 몫이 5kg 봉지의 개수다. 만약 끝까지 나누어 떨어지지 않는다면 3kg 봉지만 사용한 경우가 된다.<br>

while문을 빠져나갔을 때 5로 나눠서 나머지가 0이거나 3을 계속해서 빼서 x값이 0이라면 1,2,3번 조건에 맞는 경우기 때문에 a+b를 출력했고, 0보다 작으면 나누어 떨어지지 않는 경우기 때문에 -1을 출력한다.


```c#
class Program
{
    static void Main(string[] args)
    {
        string input = Console.ReadLine();
        int x = int.Parse(input);

        int a = 0;
        int b = 0;

        while (x > 0)
        {
            if (x % 5 == 0)
            {
                a = x / 5;
                break;
            }

            x -= 3;
            b++;
        }

        if (x >= 0)
            Console.Write(a + b);
        else
            Console.Write(-1);
    }
}
```

