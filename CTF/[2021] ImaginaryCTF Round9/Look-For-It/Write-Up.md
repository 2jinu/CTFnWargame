# [목차]
**1. [Description](#Description)**

**2. [Write-Up](#Write-Up)**

**3. [FLAG](#FLAG)**


***


# **Description**

![](images/2022-05-18-17-13-47.png)

첨부파일

http://lookforit.epizy.com

# **Write-Up**

해당 주소로 들어가보면 page라는 값에 데이터를 GET방식으로 넘기는 것 말고는 특별한 것이 없다.

![](images/2022-05-18-17-14-51.png)

하지만 directory traversal공격을 통해 flag를 획득할 수 있다.s

    http://lookforit.epizy.com/?page=../flag.txt

![](images/2022-05-18-17-15-06.png)


# **FLAG**

**FLAG{...}**