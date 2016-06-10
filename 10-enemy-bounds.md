# 몬스터와 캐릭터 빠져나가지 않게 하기

몬스터의 충돌을 처리하려면 `OnBecameInvisible`을 사용해도 되지만 화면 끝에 투명한
객체를 두고 그 객체와 충돌검사를 해서 부딪히면 삭제할 수도 있다.
`RemoveZone`이라는 빈 객체를 만들고 Rigidbody 2D와 Box Colider 2D를 추가하고
`is Kinematic`과 `on Trigger`를 체크한 뒤 부딪히면 삭제하는 코드를 넣으면 된다.

```cs
void OnTriggerEnter2D(Collider2D col) {
  // print (col.gameObject.name);
  if (col.gameObject.tag == "Enemy") {
    Destroy(col.gameObject);
  }
}
```

플레이어가 빠져나가지 않게 하려면 플레이어의 좌표를 clamp해서 일정 범위 이상으로
나가지 못하도록 하면 된다. 플레이어의 좌표를 이동하는 부분 뒤에 카메라 기준으로 좌표를
변경한 뒤 clamp해서 다시 돌리면 된다.

```cs
Vector3 viewPos = Camera.main.WorldToViewportPoint (transform.position);
viewPos.x = Mathf.Clamp(viewPos.x, 0.1f, 0.9f);
viewPos.y = Mathf.Clamp(viewPos.y, 0.1f, 0.9f);
transform.position = Camera.main.ViewportToWorldPoint(viewPos);
```
