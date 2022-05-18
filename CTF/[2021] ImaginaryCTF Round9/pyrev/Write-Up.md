# [목차]
**1. [Description](#Description)**

**2. [Write-Up](#Write-Up)**

**3. [FLAG](#FLAG)**


***


# **Description**

![](images/2022-05-18-19-38-01.png)

첨부파일

[out.txt](https://github.com/2jinu/CTFnWargame/blob/main/CTF/%5B2021%5D%20ImaginaryCTF%20Round9/pyrev/file/out.txt)


# **Write-Up**

dis.dis()를 검색하면 python에서 [역어셈블하는 모듈](https://docs.python.org/ko/3.8/library/dis.html)을 찾을 수 있다.

out.txt에서 첫번째로 FOR_ITER를 보아 for문으로 예측하고 dis 모듈을 사용하여 결과를 확인해본다.

```py
import dis
def myfunc():
    for x in ((0, 6, -17, 14, -21, 25, -23, 5, 15, 2, -12, 11, -1, 6, -4, -12, -6, 9, 8, 5, -3, -3, 6, -6, 4, -18, -6, 26, -2, -18, 20, -17, -9, -4)):
        print(x)
print(dis.dis(myfunc))

[Output]
  3           0 SETUP_LOOP              20 (to 22)
              2 LOAD_CONST              39 ((0, 6, -17, 14, -21, 25, -23, 5, 15, 2, -12, 11, -1, 6, -4, -12, -6, 9, 8, 5, -3, -3, 6, -6, 4, -18, -6, 26, -2, -18, 20, -17, -9, -4))
              4 GET_ITER
        >>    6 FOR_ITER                12 (to 20)
              8 STORE_FAST               0 (x)
...
```

out.txt에서 다음으로는 LOAD_FAST n과 LOAD_FAST x를 SUBTRACT하고 이를 STORE_FAST n하는 것을 보아 다시 예측하고 결과를 확인해본다.

```py
import dis
def myfunc():
    n=0
    for x in ((0, 6, -17, 14, -21, 25, -23, 5, 15, 2, -12, 11, -1, 6, -4, -12, -6, 9, 8, 5, -3, -3, 6, -6, 4, -18, -6, 26, -2, -18, 20, -17, -9, -4)):
        n = n-x
print(dis.dis(myfunc))

[Output]
  3           0 LOAD_CONST               1 (0)
              2 STORE_FAST               0 (n)

  4           4 SETUP_LOOP              20 (to 26)
              6 LOAD_CONST              39 ((0, 6, -17, 14, -21, 25, -23, 5, 15, 2, -12, 11, -1, 6, -4, -12, -6, 9, 8, 5, -3, -3, 6, -6, 4, -18, -6, 26, -2, -18, 20, -17, -9, -4))
              8 GET_ITER
        >>   10 FOR_ITER                12 (to 24)
             12 STORE_FAST               1 (x)

  5          14 LOAD_FAST                0 (n)
             16 LOAD_FAST                1 (x)
             18 BINARY_SUBTRACT
             20 STORE_FAST               0 (n)
             22 JUMP_ABSOLUTE           10
        >>   24 POP_BLOCK
        >>   26 LOAD_CONST               0 (None)
             28 RETURN_VALUE
```

이때, n을 함수내에서 선언하면 LOAD_CONST, STORE_FAST가 먼저 나오지만, out.txt에서는 나오지 않았다. 따라서 함수의 파라미터로 넣고 확인해본다.

```py
import dis
def myfunc(n):
    for x in ((0, 6, -17, 14, -21, 25, -23, 5, 15, 2, -12, 11, -1, 6, -4, -12, -6, 9, 8, 5, -3, -3, 6, -6, 4, -18, -6, 26, -2, -18, 20, -17, -9, -4)):
        n = n-x
print(dis.dis(myfunc))

[Output]
3           0 SETUP_LOOP              20 (to 22)
            2 LOAD_CONST              39 ((0, 6, -17, 14, -21, 25, -23, 5, 15, 2, -12, 11, -1, 6, -4, -12, -6, 9, 8, 5, -3, -3, 6, -6, 4, -18, -6, 26, -2, -18, 20, -17, -9, -4))
            4 GET_ITER
       >>   6 FOR_ITER                12 (to 20)
            8 STORE_FAST               1 (x)
...
```

out.txt에서 다음으로는 print, chr, n, '', end와 print None으로 보아 다음과 같이 작성하여 결과를 확인해본다.

```py
import dis
def myfunc(n):
    for x in ((0, 6, -17, 14, -21, 25, -23, 5, 15, 2, -12, 11, -1, 6, -4, -12, -6, 9, 8, 5, -3, -3, 6, -6, 4, -18, -6, 26, -2, -18, 20, -17, -9, -4)):
        n = n-x
        print(chr(n), end='')
    print()
print(dis.dis(myfunc))  

[Output]
  3           0 SETUP_LOOP              36 (to 38)
              2 LOAD_CONST              41 ((0, 6, -17, 14, -21, 25, -23, 5, 15, 2, -12, 11, -1, 6, -4, -12, -6, 9, 8, 5, -3, -3, 6, -6, 4, -18, -6, 26, -2, -18, 20, -17, -9, -4))
              4 GET_ITER
        >>    6 FOR_ITER                28 (to 36)
              8 STORE_FAST               1 (x)

  4          10 LOAD_FAST                0 (n)
             12 LOAD_FAST                1 (x)
             14 INPLACE_SUBTRACT
             16 STORE_FAST               0 (n)

  5          18 LOAD_GLOBAL              0 (print)
             20 LOAD_GLOBAL              1 (chr)
             22 LOAD_FAST                0 (n)
             24 CALL_FUNCTION            1
             26 LOAD_CONST              21 ('')
             28 LOAD_CONST              22 (('end',))
             30 CALL_FUNCTION_KW         2
             32 POP_TOP
             34 JUMP_ABSOLUTE            6
        >>   36 POP_BLOCK

  6     >>   38 LOAD_GLOBAL              0 (print)
             40 CALL_FUNCTION            0
             42 POP_TOP
             44 LOAD_CONST               0 (None)
             46 RETURN_VALUE
```

for문이 다 돌고 나오게되는 문자열은 ictf가 될 것을 감안하여 n-0 = 105(ascii 10진법으로 i)가 되어야 하므로 n에 105를 넣고 실행하면 flag를 획득할 수 있다.

```py
def myfunc(n):
    for x in ((0, 6, -17, 14, -21, 25, -23, 5, 15, 2, -12, 11, -1, 6, -4, -12, -6, 9, 8, 5, -3, -3, 6, -6, 4, -18, -6, 26, -2, -18, 20, -17, -9, -4)):
        n = n-x
        print(chr(n), end='')
    print()

myfunc(105)

[Output]
ictf{bytecode_could_be_easy_as_py}
```


# **FLAG**

**ictf{bytecode_could_be_easy_as_py}**