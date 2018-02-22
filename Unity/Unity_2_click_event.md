#### Unity Click Event

##### 특정 키 이벤트
```cs
void Update () {
    
   if (Input.GetKey (KeyCode.Escape)) {         // ESC의 경우.
        // Do something
	}
}
```

##### Mouse button event
```cs
void Update() {
    
    if (Input.GetMouseButtonDown (0)) {         
        // 클릭 시작
    } else if (Input.GetMouseButton (0) {       
        // 클릭 중
    } else if (Input.GetMouseButtonUp (0) {
        // 클릭 끝
    }
}
```

##### Mouse button Double Click event
```cs
private float lastClickedTime;
private float catchTime = 0.25f;

void Update() {
    if (Input.GetMouseButtonDown (0)) {
        if (Time.time - lastClickedTime < catchTime) {
            // Double Click, do something
        }
    }
    
    lastClickedTime = Time.time;
}
```

##### Mouse Long press Click event
```cs
private int timer = 0;

void Update() {
    
    if (Input.GetMouseButtonDown (0)) {         
        timer = 0;
    } else if (Input.GetMouseButton (0) {       
        timer += 1;
        
        if  (timer > 30) {      // Long press
            // Do something
        }
    } 
}
```

##### 특정 오브젝트 클릭 (Raycast)
```cs
private GameObject target;

private GameObject GetClickedObject() {
    RaycastHit hit;
    GameObject target = null;
    
    Ray ray = Camera.main.ScreenPointToRay (Input.mousePosition);
    
    if (true == (Physics.Raycast (ray.origin, ray.direction * 10, out hit))) {
        target = hit.collider.gameObject;
    }
    
    return target;
}
```