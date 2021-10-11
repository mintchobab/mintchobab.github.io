---
title: "[Unity] 오브젝트의 높이 계산하기"

categories:
  - Unity Make Practice
tags:
  - [Unity]

toc: true
toc_sticky: true

date: 2021-10-03
last_modified_at: 2021-10-03
---

> 목표 : 오브젝트 높이를 구해보자!

<br>

### 정점 구하기

[Mesh.vrtices](https://docs.unity3d.com/kr/530/ScriptReference/Mesh-vertices.html)에서 오브젝트의 정점 정보들을 가져올 수 있다. <br>
먼저 큐브를 하나 생성해서 vertice 값을 출력해보자.

~~~c#
MeshFilter mf = GetComponent<MeshFilter>();

Vector3[] vertices = mf.mesh.vertices;

foreach (var vertice in vertices)
{
    Debug.LogWarning(vertice);
}
~~~

<br>

해당 코드를 실행하면 아래와 같이 Vector3의 형태로 정점들의 포지션 값이 나온다.
<p align="center">
  <img src="/assets/images/unity/make practice/calculate height/1.png" title="그림 1" />
</p>

<br>

하지만 이 상태에서 오브젝트의 scale값을 변경한 후 다시 실행해봐도 값이 변하지 않는다. 그리고 오브젝트의 위치가 바뀌더라도 값은 동일하다.<br>
왜 그런지 찾아보니 [참고자료](https://forum.unity.com/threads/vertex-positions-on-a-scaled-gameobject.434657/) vertice 값은 오브젝트의 원본 데이터를 반환하기 때문에 position, rotation, scale 값에 영향을 받지 않는다는 것 같다. 그래서 이 값을 바로 사용할 수는 없고 한번 더 변환을 거쳐야 한다.

<br>

### 정점의 world 좌표 구하기
[transform.TransformPoint](https://docs.unity3d.com/kr/530/ScriptReference/Transform.TransformPoint.html) 함수를 사용하면 오브젝트의 world 공간 좌료를 얻을 수 있다.<br>

~~~c#
MeshFilter mf = GetComponent<MeshFilter>();

Vector3[] vertices = mf.mesh.vertices;

foreach (var vertice in vertices)
{
    Debug.LogWarning(transform.TransformPoint(vertice));
}
~~~

<br>

위에서 구한 vertice 값들을 `transform.TransformPoint`를 통해 world 좌표로 변경한다.
<p align="center">
  <img src="/assets/images/unity/make practice/calculate height/2.png" title="그림 2" />
</p>

position과 scale 값이 변하면 출력되는 값들도 변하는 것을 알 수 있다.

<br>

### 오브젝트의 높이 구하기

vertice의 world 좌표를 구했기 때문에 높이를 구하는 것은 간단하다. vertice들의 y좌표를 비교해서 값이 가장 큰 vertice가 높이가 된다.

~~~c#
MeshFilter mf = GetComponent<MeshFilter>();

Vector3[] vertices = mf.mesh.vertices;

float height = 0f;

foreach (var vertice in vertices)
{
    Vector3 pos = transform.TransformPoint(vertice);

    if (pos.y > height)
    {
        height = pos.y;
    }
}

Debug.LogWarning(height);
~~~

<br>

<p align="center">
  <img src="/assets/images/unity/make practice/calculate height/3.png" title="그림 3" width="761" height="497"/>
</p>