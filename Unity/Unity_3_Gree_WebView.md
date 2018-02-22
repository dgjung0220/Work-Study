#### Unity Gree WebView

##### 일반 Web link view
```cs
public class webView_event : MonoBehaviour {
    
    private WebViewObject webViewObject;
    
    void Start() {
        // Example
        StartWebView("http://www.naver.com");
    }
    
    public void StartWebView(string url) {
        
        webViewObject = (new GameObject ("WebViewObject")).AddComponent<WebViewObject>();
        webViewObject.Init ((msg) => {
			Debug.Log(string.Format("CallFromJS[{0}]", msg));
		});

		webViewObject.LoadURL(url);
		webViewObject.SetVisibility (true);
		webViewObject.SetMargins (50, 200, 50, 200);
    }
}
```

##### pdf view
pdf 의 경우 html 로컬 변환하여 확인 필요.
```cs
public class webView_event : MonoBehaviour {
    
    private WebViewObject webViewObject;
    
    void Start() {
        // Example
        StartCoroutine(HtmlWebView("test.html"));
    }
    
    IEnumerator HtmlWebView(string path) {
        string filePath = System.IO.Path.Combine(Application.streamingAssetsPath, path);
        string storagePath = Application.persistentDataPath + "/" + path;

        if (filePath.Contains("://")) {
            WWW www = new WWW(filePath);
            yield return www;

            if (string.IsNullOrEmpty(www.error)) {
                System.IO.File.WriteAllBytes(storagePath, www.bytes);
            }
            StartWebView("file://" + storagePath);
        } else {
            StartWebView(filePath);
        }
    }
}
```
Enumerator의 경우, [StartCoroutine()](https://docs.unity3d.com/kr/current/Manual/Coroutines.html) 을 사용하여 실행 필요.  
UnityScript의 경우 yield 구문을 포함하면 자동으로 코루틴으로 인식되며, IEnumerator 반환 타입은 명시적으로 선언할 필요가 없다. 또한 일반 함수처럼 호출하여 시작할 수 있다.