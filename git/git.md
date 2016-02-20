### 文件状态说明
输入`git status -s`或者`git status --short`命令，状态报告类似如下：
```
git status -s
 M READMNE
MM Rakefile
A  lib/git.rb
M  lib/s.rb
?? LICENSE.txt
```

`??`标记表示新添加的未跟踪的文件，`A`标记表示新添加到暂存区的文件，右边的`M`表示该文件被修改了但是还没放入暂存区，左边的`M`表示该文件被修改了并放入了暂存区