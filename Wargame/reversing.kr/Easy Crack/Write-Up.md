# [목차]
**1. [Description](#Description)**

**2. [Write-Up](#Write-Up)**

**3. [FLAG](#FLAG)**


***


# **Description**

![](images/2022-01-28-15-00-43.png)

# **Write-Up**

파일 정보를 확인하자.

![](images/2022-01-28-15-03-06.png)

문자열에 "Congratulation !!"와 "Incorrect Password"가 있다.

![](images/2022-01-28-15-13-59.png)

해당 부분을 보면 GetDlgItemTextA이후 분기문들이 존재한다.

![](images/2022-01-28-15-19-19.png)

입력 후 스택을 보면 esp + 4부터 들어간다. 즉, esp + 5와 0x61이 같아야 하므로 2번째 글자는 a가 되어야 한다.

![](images/2022-01-28-15-32-36.png)

다음으로, push이후 esp + 0xA이기 때문에 3번째 글자부터와 5y랑 비교한다.

![](images/2022-01-28-15-42-52.png)

다음으로, 5글자 부터 R3versing과 비교한다.

![](images/2022-01-28-15-45-47.png)

마지막으로 첫번째 글자와 E랑 비교한다.

![](images/2022-01-28-15-48-14.png)

따라서, Password는 Ea5yR3versing이다.

![](images/2022-01-28-15-49-08.png)


# **FLAG**

**Ea5yR3versing**