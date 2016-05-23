# 적 스폰하기

적을 스폰하려면 일단 적을 Prefab으로 만들어서 적을 복제할 수 있게 해야 한다.
그리고 스폰을 담당하는 객체를 만들어서 거기서 스폰을 수행해야 한다.

SpawnManager라는 객체에 똑같은 이름의 스크립트를 만들어서 컴포넌트로 추가한다.

스폰되는 위치는 5개로 정해지는데, 각각 화면의 1/6 위치, 2/6 위치, .... 5/6 위치가 된다.
즉, 화면 기준으로 좌표를 설정해줘야 하는 것이다. 유니티에서는 화면 좌표를 월드 좌표로
변환하는 유틸리티 함수를 제공해준다. `Camera.ViewportToWorldPoint` 이다.

즉, 카메라 기준으로 1/6, .... 위치를 만들어서 월드 좌표로 변환하면 되는 것이다.

SpawnManager가 처음 실행될 때 이 좌표를 미리 캐싱해서 저장해 놓는다.

```cs
Vector3[] positions = new Vector3[5];

void Start () {
  CreatePositions ();
}

void CreatePositions() {
  float viewPosY = 1.2f;
  float viewPosX = 0f;
  float gapX = 1f / 6f;
  for (int i = 0; i < positions.Length; i++) {
    viewPosX = gapX + gapX * i;
    Vector3 viewPos = new Vector3 (viewPosX, viewPosY, 0);
    Vector3 worldPos = Camera.main.ViewportToWorldPoint (viewPos);
    worldPos.z = 0f;
    positions [i] = worldPos;
  }
}
```

저장한 뒤에는 거기에 맞춰 적을 소환하면 된다.

```cs
public bool isSpawn = false;
public float spawnDelay = 1.5f;
float spawnTimer = 0f;

void SpawnEnemy() {
  if (isSpawn == true) {
    if (spawnTimer > spawnDelay) {
      // ...
      int index = Random.Range (0, positions.Length);
      Instantiate (enemyPrefab, positions [index], Quaternion.identity);
      spawnTimer = 0f;
    }
    spawnTimer += Time.deltaTime;
  }
}

// Update is called once per frame
void Update () {
  SpawnEnemy ();
}
```

중간의 Instantiate에 positions의 인덱스에 따라 적이 소환되는 위치를
설정할 수 있다.

```cs
for (int i = 0; i < positions.Length; i++) {
  Instantiate (enemyPrefab, positions [i], Quaternion.identity);
}
```

이렇게 하면 화면의 가로방향 전체에 적이 소환된다.
