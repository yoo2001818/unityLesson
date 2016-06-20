# Scene 전환 / 배포

Scene을 새로 만들어서 Button을 만들고, SceneManager과 새 컴포넌트를 추가해서
`changeToScene` 함수를 만든다.

```cs
public void ChangeToScene() {
  Application.LoadLevel ("Main");
}
```

그리고 버튼의 On Click에 SceneManager를 추가하고 changeToScene을 선택하면 된다.

그 뒤에는 Build Settings...에 들어가서 사용할 Scene들을 추가한다.
원하는 플랫폼을 선택해서 Build를 누르면 빌드할 수 있다.
