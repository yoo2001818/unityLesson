# 적 캐릭터 충돌하기

적 캐릭터와 캐릭터가 충돌하면 둘 모두 사라지게 만들려고 한다. 먼저 적 캐릭터를 선택해서
`Enemy` 태그를 붙인다. 없으면 만들어서 붙이면 된다. 그 뒤 캐릭터에도 마찬가지로
`Player` 태그를 붙인다.

캐릭터에 CircleCollider2D와 RigidBody2D를 붙이고 CircleCollider2D의 충돌 영역을 알맞게
조정한 뒤 `Is Trigger`를 체크한다. RigidBody2D에서는 `Is Kinematic`을 체크한다.

적 캐릭터에서도 BoxCollider2D와 RigidBody2D를 붙이고 마찬가지로 수정한다.

그 뒤에 캐릭터에 충돌 트리거를 처리하는 함수를 넣는데, Unity에서는 충돌 트리거가 일어나면
`OnTriggerEnter2D` 함수가 호출된다. 아까 붙인 `Enemy` 태그를 확인해서 만약 적이라면
둘 모두 사라지게 만들면 될 것이다.

```cs
void OnTriggerEnter2D(Collider2D col) {
	if (col.gameObject.tag == "Enemy") {
		Destroy (col.gameObject);
		Destroy (this.gameObject);
	}
}
```
