# 총알 충돌 검사하기

총알 충돌 검사는 [4강](./4-enemy-collision.md)에서 했던 것 처럼 그대로 구현하면 된다.

```cs
void OnTriggerEnter2D(Collider2D col) {
  if (col.gameObject.tag == "Laser") {
    Instantiate (explosionPrefab, transform.position, Quaternion.identity);
    Destroy (col.gameObject);
    Destroy (this.gameObject);
  }
}
```

그런데 총알이 화면 밖으로 나가도 삭제되지 않고 계속 돌아다닌다. Unity에서는 화면 밖으로
객체가 나갔을 때 호출되는 함수를 제공한다. 이 함수가 호출되면 총알을 제거하면 된다.

```cs
void OnBecameInvisible() {
  Destroy (this.gameObject);
}
```
