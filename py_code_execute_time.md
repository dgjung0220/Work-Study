#### 코드 실행 시간 측정

```python
import time

start_time = time.time()
# ----------------

실제 사용

#-----------------
print("start_time", start_time)
print("--------%s---------", %(time.time() - start_time))
```
```python
from time import strftime
now = strftime("%y%m%d-%H%M%S")
print(now)
```