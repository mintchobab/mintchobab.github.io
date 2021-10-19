---
title: "[Unity] 태그를 스크립트로 추가해보자"

categories:
  - Unity Make Practice
tags:
  - [Unity]

toc: true
toc_sticky: true

date: 2021-10-18
last_modified_at: 2021-10-18
---

> 목표 : 태그를 에디터에서 추가하는것이 아닌 스크립트를 통해 추가할 수 있는 기능을 만든다.

<br>

### TagManager
<br>
유니티 에디터 상단의 `[`Edit`]` - `[`Project Settings...`]`로 들어가면 해당 프로젝트에 대한 설정들이 정의되어있다.<br>
이번에 변경할 `Tag`도 Project Settings의 `Tag and Layers`라는 탭으로 들어가면 확인할 수 있다.

<p align="center">
  <img src="/assets/images/unity/make practice/tag auto create/1.JPG" title="그림 1" />
</p>

<br>

Project Settings에서 정의된 값들은 유니티 프로젝트 폴더의 `ProjectSettings`에 저장되어 있다. 해당 폴더는 프로젝트를 처음 생성할 때 자동으로 생성되므로 따로 추가할 필요는 없다.

<p align="center">
  <img src="/assets/images/unity/make practice/tag auto create/2.JPG" title="그림 2" />
</p>

<br>

폴더 안으로 들어가면 여러가지 ~.asset 파일들이 있는데 `TagManager.asset` 파일을 열어보면 해당 프로젝트에 정의된 Tag와 Layer들을 확인할 수 있다. 지금은 추가한 Tag나 Layer가 없기 때문에 기본상태이다.

<p align="center">
  <img src="/assets/images/unity/make practice/tag auto create/3.JPG" title="그림 3" />
</p>

<br>

### 스크립트 작성

<br>

스크립트로 태그를 추가하기 위해서는 `TagManager.asset` 파일에 접근해야 한다. `LoadAllAssetsAtPath` 함수를 사용하면 해당 경로에 있는 파일들을 Object의 형태로 가져온다.
.asset 파일은 serialize화 된 데이터기 때문에 Unity에서 다루기위해 SerializedObject화 하여 사용한다.
직렬화에 대한 자세한 설명은 [링크]((https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=hammerimpact&logNo=220770624015)) 참고.

```c#
SerializedObject tagManager = new SerializedObject(AssetDatabase.LoadAllAssetsAtPath("ProjectSettings/TagManager.asset")[0]);
SerializedProperty tags = tagManager.FindProperty("tags");
```

<br>

그 다음은 Tag의 이름을 확인한 후 해당 Tag가 존재하면 다음 Tag로 넘어가고, Tag가 존재하지 않는다면 태그의 마지막 인덱스를 하나 추가하고 새로운 Tag를 부여한다.

```c#
private string[] tagNames = new string[] { "TagA", "TagB", "TagC" };

private void Start()
{
    CreateTag();
}

public void CreateTag()
{
    SerializedObject tagManager = new SerializedObject(AssetDatabase.LoadAllAssetsAtPath("ProjectSettings/TagManager.asset")[0]);
    SerializedProperty tags = tagManager.FindProperty("tags");

    foreach (string tagName in tagNames)
    {
        bool isExist = false;

        // Tag가 존재하는지 확인
        for (int i = 0; i < tags.arraySize; i++)
        {
            SerializedProperty existingTag = tags.GetArrayElementAtIndex(i);
            if (existingTag.stringValue.Equals(tagName))
            {
                isExist = true;
                Debug.Log($"{tagName}는 이미 존재합니다.");
                break;
            }
        }

        // 이미 Tag가 있다면 다음 Tag를 확인
        if (isExist)
            continue;

        // 새로운 Tag를 추가
        int index = tags.arraySize;

        tags.InsertArrayElementAtIndex(index);
        tags.GetArrayElementAtIndex(index).stringValue = tagName;

        tagManager.ApplyModifiedProperties();
        tagManager.Update();
    }
}
```

<br>

여기까지 작성하면 Play 버튼을 눌렀을 때 새로운 태그를 추가할 수 있다. 하지만 Play 상태가 아닐 때 태그를 추가하기 위해서는 한가지 작업을 더 해야한다. 여러가지 방법이 있겠지만 여기서는 인스펙터에 버튼을 하나 만들어서 해당 버튼이 눌리면 태그가 추가 될 수 있도록 한다.

```c#
[CustomEditor(typeof(TagCreator))]
    public class CreateTagButton : Editor
    {
        public override void OnInspectorGUI()
        {
            base.OnInspectorGUI();
            TagCreator creator = (TagCreator)target;

            if (GUILayout.Button("Create Tag"))
            {
                creator.CreateTag();
            }
        }
    }
```

<br>

### 전체 스크립트

```c#
public class TagCreator : MonoBehaviour
{
    private string[] tagNames = new string[] { "TagA", "TagB", "TagC" };

    private void Start()
    {
        CreateTag();
    }

    public void CreateTag()
    {
        SerializedObject tagManager = new SerializedObject(AssetDatabase.LoadAllAssetsAtPath("ProjectSettings/TagManager.asset")[0]);
        SerializedProperty tags = tagManager.FindProperty("tags");

        foreach (string tagName in tagNames)
        {
            bool isExist = false;

            for (int i = 0; i < tags.arraySize; i++)
            {
                SerializedProperty existingTag = tags.GetArrayElementAtIndex(i);
                if (existingTag.stringValue.Equals(tagName))
                {
                    isExist = true;
                    Debug.Log($"{tagName}는 이미 존재합니다.");
                    break;
                }
            }

            if (isExist)
                continue;

            int index = tags.arraySize;

            tags.InsertArrayElementAtIndex(index);
            tags.GetArrayElementAtIndex(index).stringValue = tagName;

            tagManager.ApplyModifiedProperties();
            tagManager.Update();
        }
    }

    [CustomEditor(typeof(TagCreator))]
    public class CreateTagButton : Editor
    {
        public override void OnInspectorGUI()
        {
            base.OnInspectorGUI();
            TagCreator creator = (TagCreator)target;

            if (GUILayout.Button("Create Tag"))
            {
                creator.CreateTag();
            }
        }
    }
}
```


