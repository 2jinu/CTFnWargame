# [목차]
**1. [Description](#Description)**

**2. [Write-Up](#Write-Up)**

**3. [FLAG](#FLAG)**


***


# **Description**

```asp
<%
    str = Request("str")

    If not str = "" Then
        result = Replace(str,"a","aad")
        result = Replace(result,"i","in")
        result1 = Mid(result,2,2)
        result2 = Mid(result,4,6)
        result = result1 & result2
        Response.write result
        If result = "admin" Then
            pw = "????????"
        End if
    End if
%>
```


# **Write-Up**

a가 있으면 aad로, i가 있으면 in으로, 그 결과의 2번째 부터 2글자를 추출하고, 4번째부터 6글자를 추출하고 병합하여 admin을 만들어야한다.

ami를 입력하여 FLAG를 얻자.

    Authkey : k09rsogjorejv934u592oi


# **FLAG**

**k09rsogjorejv934u592oi**