#### Unity Video Player

##### Video Player Control
``videoPlayer.Play()``, ``videoPlayer.Stop()``, ``videoPlayer.Pause()`` 

##### 특정 오브젝트에 동영상 재생 (MaterialOverride)
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Video;

public class video_play : MonoBehaviour {
    
    [SerializeField]
	private GameObject player_material = null;                  // 동영상이 재생될 오브젝트
	[SerializeField]
	private Renderer target_renderer = null;                    // player_material 의 renderer
	private VideoPlayer videoPlayer;
	
	void Start() {
	    GameObject camera = GameObject.Find("ARCamera");        // ARCamera GameObject에 Video player 추가
	    
	    videoPlayer = camera.AddComponent<UnityEngine.Video.VideoPlayer>();
	    videoPlayer.playOnAwake = false;
	    videoPlayer.renderMode = UnityEngine.Video.VideoRenderMode.MaterialOverride;
	    videoPlayer.targetMaterialRenderer = target_renderer;
	    videoPlayer.url = "Assets/SampleVideo.mp4";
	    videoPlayer.frame = 100;
	    videoPlayer.isLooping = true;
	}
}
```

##### 전체 화면 동영상 재생 (CameraNearPlane, CameraFarPlane)
위의 코드에서 player_material(GameObject) 관련 설정 제외 및 renderMode 수정.
```cs
videoPlayer.renderMode = UnityEngine.Video.VideoRenderMode.CameraNearPlane;
videoPlayer.targetCameraAlpha = 0.8F;                           // 동영상 투명도
```