# view path

一个log file,里面文件是这种格式：person+tweet id

```text
'@Biz,T1',
'@Jack,T7',
'@Biz,T2',
'@Jack,T8',
'@Biz,T3',
'@Biz,T3',
'@Biz,T2',
'@Biz,T1',
'@Biz,T2',
'@Jack,T9',
'@Jack,T7',
'@Jack,T8',
'@Jack,T9',
'@Biz,T3',
'@Biz,T7',
'@Biz,T8',
'@Biz,T9'
```

3个tw eet id是一个view path。 所以一个tweet id list，每三个结合成一个path

输出most frequent的view path

```text
import collections
import sys
import re


class FindMostCommonTweetViewPath:
    # TODO implement your solution to find the most common tweet view path
    def __init__(self):
        self.user2tid = collections.defaultdict(list)
        self.view2cnt = collections.defaultdict(int)
        self.maxCnt = 0
        self.mostCommonTweetViewPath = None

    def updateViewPaths(self, user, tid):
        self.user2tid[user.strip()].append(tid.strip())

    def getMostCommonTweetViewPath(self):
        for k, v in self.user2tid.items():
            n = len(v)
            if n >= 3:
                for i in range(n - 2):
                    curViewPath = ','.join(v[i:i + 3])
                    self.view2cnt[curViewPath] += 1
                    if self.view2cnt[curViewPath] == self.maxCnt:
                        self.mostCommonTweetViewPath.add(curViewPath)
                    elif self.view2cnt[curViewPath] > self.maxCnt:
                        self.mostCommonTweetViewPath = {curViewPath}
                        self.maxCnt = self.view2cnt[curViewPath]


if __name__ == '__main__':
    # TODO Read input from stdin
    # TODO Call the FindMostCommonTweetViewPath to find results
    # TODO Print results
    f = FindMostCommonTweetViewPath()
    pattern = '^@\w+,T\d+'
    for line in sys.stdin:
        if not line or not re.match(pattern, line):
            sys.stdout.write('Log malformed!')
            continue

        user, tid = line.split(',')
        f.updateViewPaths(user, tid)

    f.getMostCommonTweetViewPath()

    if not f.mostCommonTweetViewPath:
        sys.stdout.write('No tweet path found!')
    else:
        for i in sorted(list(f.mostCommonTweetViewPath)):
            sys.stdout.write(i + '\n')

arr = ['@Biz,T1',
'@Jack,T7',
'@Biz,T2',
'@Jack,T8',
'@Biz,T3',
'@Biz,T3',
'@Biz,T2',
'@Biz,T1',
'@Biz,T2',
'@Jack,T9',
'@Jack,T7',
'@Jack,T8',
'@Jack,T9',
'@Biz,T3',
'@Biz,T7',
'@Biz,T8',
'@Biz,T9']
if __name__ == '__main__':
    # TODO Read input from stdin
    # TODO Call the FindMostCommonTweetViewPath to find results
    # TODO Print results
    f = FindMostCommonTweetViewPath()
    for line in arr:
        if not line or not line.strip():
            sys.stdout.write('Log malformed')
            continue

        x = line.split(',')
        if len(x) != 2 or x[0].strip()[0] != '@':
            sys.stdout.write('Log malformed!')
        else:
            f.getviewPaths(x[0], x[1])

    f.getMostCommonTweetViewPath()

    if not f.mostCommonTweetViewPath:
        sys.stdout.write('No Tweet path found!')
    else:
        temp = ','.join(sorted(f.mostCommonTweetViewPath.split(',')))
        sys.stdout.write(temp)

# if __name__ == '__main__':
#     # TODO Read input from stdin
#     # TODO Call the FindMostCommonTweetViewPath to find results
#     # TODO Print results
#     import fileinput
#
#     f = FindMostCommonTweetViewPath()
#     arr = ['@Biz,T1',
# '@Jack,T7',
# '@Biz,T2',
# '@Jack,T8',
# '@Biz,T3',
# '@Biz,T3',
# '@Biz,T2',
# '@Biz,T1',
# '@Biz,T2',
# '@Jack,T9',
# '@Jack,T7',
# '@Jack,T8',
# '@Jack,T9',
# '@Biz,T3',
# '@Biz,T7',
# '@Biz,T8',
# '@Biz,T9']
#     for line in arr:
#         a,b = line.split(',')
#         f.getMostCommonTweetViewPath(a,b)
#
#     print(f.mostCommonTweetViewPath)

```



