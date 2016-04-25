# 폭발 효과음 내기

일단 폭발 효과음을 구현하려면 폭발 사운드를 Asset에 추가해야 한다.

추가하고 나면 빈 GameObject를 새로 만든다. 그 뒤 AudioSource 오브젝트를 추가하고,
새 스크립트 (`SoundManager`)를 추가한다.

스크립트에는 다름과 같은 내용을 넣는다.

```cs
using UnityEngine;
using System.Collections;

public class SoundManager : MonoBehaviour {

	public AudioClip soundExplosion;
	AudioSource myAudio;
	public static SoundManager instance;
	void Awake () {
		if (SoundManager.instance == null) {
			SoundManager.instance = this;
		}
	}
	// Use this for initialization
	void Start () {
		myAudio = this.GetComponent<AudioSource> ();
	}

	public void PlaySound() {
		myAudio.PlayOneShot (soundExplosion);
	}

	// Update is called once per frame
	void Update () {
	}
}
```

그 뒤 soundExplosion에 폭발 사운드를 설정한다. 이제 원하는 부분에서

```cs
SoundManager.instance.PlaySound ();
```

를 통해 폭발 사운드를 발생시키면 된다. 플레이어가 죽을 때나 적이 죽을 때 등등 원하는 곳에서
사용하면 된다.
