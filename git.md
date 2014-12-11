## GIT cheatsheet

从这里学来的 哈哈 可以直接来这里看 图形化界面非常棒 https://try.github.io/levels/1/challenges/1

**初始化 会生成一个隐藏的.git文件**

```bash
git init
```

**查看 当前repo下面文件的状态**

```bash
git status
```

**添加有变化或者新建的文件 这个.命令 很给力**


```bash
git add .
```

**将变更提交到本地**

```bash
git commit -m "something"
```

**看看commit的历史记录**

```bash
git log
```
*log更多用法*

* --stat更多信息

```bash
git log --stat

commit 75072d01391571574b1d31d72118dcd4c9d16a00
Author: zhangxuan06 <vikingmute@gmail.com>
Date:   Fri Nov 21 17:48:44 2014 +0800

    update list pages

 List/comprehension.md | 11 +++++++++++
 List/loop.md          |  9 +++++++++
 2 files changed, 20 insertions(+)
```

**添加一个remote url，可以将本地push到线上地址啦**

```bash
git remote add origin https://github.com/try-git/try_git.git
```

*remote的更多用法*

* 不加参数 看看现在有什么url alais
* remote rm 删除一个url
* remote reset-url 更新一个url

```bash
$ git remote
origin
$ git remote -v
origin	git@github.com:github/git-reference.git (fetch)
origin	git@github.com:github/git-reference.git (push)
```

**push 到线上 我们用的url 是origin这个alais，分支是master**

```bash
git push -u origin master
```

**branch 分支管理**

* 查看当前branch

```bash
git branch

* master

```

* 新建branch

```bash
git branch testing
```

* 切换branch

```bash
git checkout testing
git branch
  master
* testing
```

* 删除branch

```bash
git branch -d testing
```

典型的场景是这样的 主干上稳定版 已经上线 分支开发新功能 测试好了 然后主干上线

**merge功能**

```bash
$ git branch
  master
* testing

$ ls
README   hello.rb more.txt test.txt

$ git merge removals
Updating 8bd6d8b..8f7c949
Fast-forward
 more.txt |    1 -
 test.txt |    1 -
 2 files changed, 0 insertions(+), 2 deletions(-)
 delete mode 100644 more.txt
 delete mode 100644 test.txt
 
$ ls
README   hello.rb

```
