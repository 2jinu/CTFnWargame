# [목차]
**1. [Description](#Description)**

**2. [Write-Up](#Write-Up)**

**3. [FLAG](#FLAG)**


***


# **Description**

![](images/2022-05-18-19-32-17.png)

첨부파일

[dragon.pdf](https://github.com/2jinu/CTFnWargame/raw/main/CTF/%5B2021%5D%20dCTF/Don't%20let%20it%20run/file/dragon.pdf)


# **Write-Up**

[peepdf.py](https://github.com/2jinu/CTFnWargame/raw/main/CTF/%5B2021%5D%20dCTF/Don't%20let%20it%20run/file/peepdf_0.3.zip)으로 dragon.pdf를 열어보면 javascript가 object 3에 존재한다는 것을 확인할 수 있다.

![](images/2022-05-18-19-33-06.png)

object 3을 입력하면 javascript code가 나타난다.

![](images/2022-05-18-19-33-14.png)

해당 code를 실행하면 flag를 획득할 수 있다.

![](images/2022-05-18-19-33-22.png)

# **FLAG**

**dctf{pdf_1nj3ct3d}**