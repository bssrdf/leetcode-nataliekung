# No k consecutive repeated char



```text
给一个字符串，要求删减最少的字符，使得字符串中不会出现连续三个一样的字符，比如 bbbbbbaccccc 要为bbacc。
```

 

```text
def solution(S):
    # write your code in Python 3.6
    size = len(S)
    s = e = 0
    counter = 0
    toDelete = set()
    while e < size:
        if S[s] == S[e]:
            counter += 1
        else:
            counter = 0
            s = e + 1
        e += 1
        while counter >=3:
            toDelete.add(s)
            s += 1
            counter -= 1
    return ''.join(x for i,x in enumerate(S) if i not in toDelete)

print(solution('bbbbbbaccccc'))
#xxtxx
```

