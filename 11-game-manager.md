# 게임 매니저 구현하기
게임 매니저는 게임을 총괄하는 객체이다. 일단 SpawnManager를 싱글톤 모양으로 만들어서
다른 클래스에서 참조할 수 있게 만든다.

```cs
public static SpawnManager instance;

void Awake() {
  if (SpawnManager.instance == null) {
    SpawnManager.instance = this;
  }
}
```
그리고 Player와 SpawnManager의 canShoot과 isShoot를 해제한다.

그 뒤, 빈 객체를 만들어서 GameManager 스크립트를 추가한다.

```cs
using UnityEngine;
using System.Collections;

public class GameManager : MonoBehaviour {
	public static GameManager instance;

	GameObject player;
	int score = 0;

	void Awake() {
		if (GameManager.instance == null) {
			GameManager.instance = this;
		}
	}
	// Use this for initialization
	void Start () {
		player = GameObject.FindWithTag ("Player");
		Invoke ("StartGame", 3.0f);
	}

	void StartGame() {
		player.GetComponent<PlayerMover> ().canShoot = true;
		SpawnManager.instance.isSpawn = true;
	}

	// Update is called once per frame
	void Update () {

	}
}
```

총알과 적이 나타나지 않다가 3초 뒤부터 나오는 것을 볼 수 있다.

그럼 점수는 어떻게 구현할까? GameManager 안에 `AddScore` 함수를 구현한다.

```cs
public void AddScore(int enemyScore) {
	score += enemyScore;
}
```

이제 Enemy에서 적이 삭제될 때 해당 함수를 호출하면 된다.

```cs
public int killScore = 100;

void OnTriggerEnter2D(Collider2D col) {
  // ...
	GameManager.instance.AddScore (killScore);
  // ...
}
```

점수를 표시하는건 어떻게 할까? GameObject -> UI -> Text를 눌러 새 텍스트를 만들고
적절하게 배치한다.

해당 텍스트 객체를 GameManager에서 참조해서 값을 바꾸면 된다.

```cs
using UnityEngine.UI;

public Text scoreText;

public void AddScore(int enemyScore) {
  score += enemyScore;
  scoreText.text = "Score: " + score;
}

```
