---
title: "[Algorithm] 백준 1193번 : 분수찾기 C# 문제풀이"

categories:
  - Algorithm Baekjoon
tags:
  - [Algorithm]

toc: true
toc_sticky: true

date: 2021-10-24
last_modified_at: 2021-10-24
---

## 문제

[문제링크](https://www.acmicpc.net/problem/1193)

<p align="center">
  <img src="/assets/images/algorithm/baekjoon/1193-1.jpg" title="그림 2" />
</p>

<br>

## 풀이

<br>

문제에 적힌 순서를 따라가다보면 규칙을 발견할 수 있다. 아래 그림과 같이 대각선 방향으로 순서가 정해지는데, 홀수번째 대각선은 분자가 1씩증가 분모는 1씩 감소, 짝수번째 대각선은 분자가 1씩감소 분모는 1씩 증가한다. 따라서 입력받는 숫자가 몇번째 대각선에 포함되는지와 해당 대각선에서 몇번째에 위치한 값인지만 알 수 있다면 결과를 출력할 수 있다.

<p align="center">
  <img src="/assets/images/algorithm/baekjoon/1193-2.jpg" title="그림 2" />
</p>

<br>

```c#
class Program
{
    static void Main(string[] args)
    {
        string X = Console.ReadLine();
        int x = int.Parse(X);

        int lineCount = 0;
        int sum = 0;

        // 몇번째 대각선에 있는지 계산
        while (x > sum)
        {
            lineCount++;
            sum += lineCount;
        }

        // 해당 줄에 몇번째인지 계산
        int index = x - (sum - lineCount);

        // 홀수
        if (lineCount % 2 == 1)
            Console.Write($"{lineCount - index + 1}/{index}");
        // 짝수
        else
            Console.Write($"{index}/{lineCount - index + 1}");
    }
}
```

<br>

## 수정

풀이에서 index를 구하는 부분이 이상해서 수정했다. index를 추가로 한번 더 구하지 않고 while문에서 x를 이용해서 index와 sum을 대신할 수 있을 것 같았다.

```c#
class Program
{
    static void Main(string[] args)
    {
        string X = Console.ReadLine();
        int x = int.Parse(X);

        int lineCount = 1;

        while (x > lineCount)
        {
            x -= lineCount;
            lineCount++;
        }

        if (lineCount % 2 == 1)
            Console.Write($"{lineCount - x + 1 }/{x}");
        else
            Console.Write($"{x}/{lineCount - x + 1}");
    }
}
```





