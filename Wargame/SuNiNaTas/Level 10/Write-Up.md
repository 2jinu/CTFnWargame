# [목차]
**1. [Description](#Description)**

**2. [Write-Up](#Write-Up)**

**3. [FLAG](#FLAG)**


***


# **Description**

![](images/2022-01-03-02-33-32.png)


# **Write-Up**

압축파일을 다운로드할 수 있다. 압축되어있는 실행 파일의 기본적인 정보를 확인해보자.

![](images/2022-01-03-02-33-43.png)

.NET Framework로 만들어져있다. dotpeek으로 디컴파일한다.

![](images/2022-01-03-02-33-47.png)

Main을 보면 Form1을 생성한다.

![](images/2022-01-03-02-33-51.png)

Form1을 보면 FLAG와 비밀번호를 알 수 있다.

![](images/2022-01-03-02-33-55.png)


# **FLAG**

**Did U use the Peid?**