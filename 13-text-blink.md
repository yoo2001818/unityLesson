# 글자 깜빡이기

Game Scene 중간에 READY가 몇 초동안 깜빡이게 만들려고 한다. Text 객체를 추가하고
Canvas에 GameTextControl 컴포넌트를 만들어 추가한다.

```cs
public class GameTextControl : MonoBehaviour {

	public GameObject readText;

	public static GameTextControl instance;
	void Awake () {
		if (GameTextControl.instance == null) {
			GameTextControl.instance = this;
		}
	}

	// Use this for initialization
	void Start () {
		readText.SetActive (false);
		StartCoroutine (ShowReady ());
	}

	IEnumerator ShowReady() {
		int count = 0;
		while (count < 3) {
			readText.SetActive (true);
			yield return new WaitForSeconds (0.5f);
			readText.SetActive (false);
			yield return new WaitForSeconds (0.5f);
			count++;
		}
	}

	// Update is called once per frame
	void Update () {

	}
}
```

그 뒤 텍스트를 설정하면 글자가 깜빡이는 걸 볼 수 있다. 코루틴은 yield를 사용해서 코드
실행을 잠시 멈출 수 있다.
