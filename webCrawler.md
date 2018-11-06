### 웹크롤러

[나만의 웹 크롤러 만들기 with Requests/BeautifulSoup | Beomi's Tech Blog](https://beomi.github.io/2017/01/20/HowToMakeWebCrawler/)

#### requests 모듈
``pip install requests``

```python
import requests

req = requests.get('http://www.google.com')
html = req.text
header = req.headers
status = req.status_code
is_ok = req.ok
```

#### BeautifulSoup
``pip install bs4``

```python
import requests
from bs4 import BeautifualSoup

# HTTP GET Request
req = requests.get('http://www.google.com')

# Get html source
html = req.text
soup = BeautifulSoup(html, 'html.parser')
```

