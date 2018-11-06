### 디렉터리 파일 카운트

```python
import os
import glob
import csv
```

```python
f = open('test.csv', 'w', newline='')
wr = csv.writer(f)
```

```python
folders = glob.glob('*\')
```

```python
for folder in folders:
    for root, dirs, files in os.walk(folder):
        wr.writerow([folder[:-1], len(files)])
```

```python
f.close()
```

