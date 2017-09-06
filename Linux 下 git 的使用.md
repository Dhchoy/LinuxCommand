# Linux 下 git 的使用

## 1. git 和 github 环境的搭建

1. 创建 ssh key

   为了能够让 github 识别上传文件的用户，需要创建 ssh key

   ```shell
   ssh-keygen -t rsa -C "your_email@youremail.com" 
   # 其中 your_enmail@youremail.com 根据需要更改
   # 输入后会询问时候设置密码，直接回车则不设置
   # 提示 ssh key 已经创建好了
   ```

2. 将生成的 ssh 写入 github

   在创建好本地的 ssh key 后，需要让 github 知道这个 ssh key 是我们自己的，则在 github 中点击 ---> 设置 ---> SSH and GPS keys，创建一个 new ssh key，将刚才生成的 ssh key 填入即可，其中 ssh key 位于 `~/.ssh/id_rsa.pub`。

3. 验证是否成功

   ```shell
   ssh -T git@github.com # 就是 git@github.com，不要改为别的

   # 如果成功，会出来 Hi...
   ```

4. 设置 username 和email

   ```shell
   # 每次把项目上传的时候，github 每次 commit 都会记录下面的信息
   git config --global user.name "your name" #your name 可更改
   git config --global user.email "your_email@youremail.com"

   # --global 配置的文件会位于 ~/.gitconfg
   ```

## 2. 创建或者克隆一个项目

1. 初始化 git，

   ```shell
   # 进入项目

   cd Project

   # 初始化 git

   git init
   ```

2. 如果是克隆，则使用

   ```shell
   git clone https://github.com/Dhchoy/PAT
   # 即 git clone [url]
   ```

## 3. 上传项目

1. 更新项目

   ```shell
   git status # 查看上传的文件时候正确

   git add file # 或者 git add . 添加所有来更新文件

   git commit -m "注释" # 提交更新，其中注释部分可以根据需要填写
   ```

2. 添加远程链接

   ```shell
   git remote add origin git@github:yourname/youRepo.git

   # 其中 yourname 是个人的github 名字，yourRepo 是仓库 repository 名字

   # 如果提示出错信息 fatal:remote origin already exists
   # 则可以先输入 git remote rm origin
   # 再输入 git remote add origin git@github:yourname/youRepo.git 则可
   ```

3. 合并项目

   ```shell
   git push origin master 
   # 将本地项目更新到 github 上去
   # 这里 master 是主分支名，如果是其他分支，填写对应分支名字
   ```

4. 其他提交指令

   ```shell
   # 提交暂存区的文件到仓库区
   git commit [file1] [file2] ... -m [message]

   # 提交工作区自自上次 commit 之后的变化，直接到仓库区
   git commit -a

   # 提交时显示所有diff 信息
   git commit -v

   # 使用一次新的 commit，代替上一次 commit
   # 如果代码没有任何新变化，则用来改写上一次 commit 的提交信息
   git commit --amend -m [message]

   # 重做上一次 commit，并包括指定文件的新变化
   git commit --amend [file1] [file2] ...
   ```

## 4. 增加/删除文件

```shell
# 添加文件到暂存区
git add [file1] [file2] ...

# 添加目录到暂存区，包括子目录
git add [dir]

# 添加当前目录的所有文件到暂存区
git add .

# 添加每个变化前，都会要求确认
# 对于同一个文件的多处变化，可以实现分次提交
git add -P

# 删除工作区文件，并且将这次删除放入暂存区
git rm [file1] [file2]

# 停止追踪指定文件，但该文件会保留在工作区
git rm --cached [file]

# 改名文件，并且将改名放入暂存区
git mv [file-original] [file-renamed]
```

## 5. 分支

```shell
# 列出所有本地分支
git branch

# 列出所有远程分支
git branch -r

# 列出所有本地分支和远程分支
git branch -a

# 新建一个分支，但依然停留在当前分支
git branch [branch-name]

# 新建一个分支，并切换到该分支
git checkout -b [branch]

# 新建一个分支，指向指定 commit
git branch [branch] [commit]

# 新建一个分支，与指定的远程分支建立追踪关系
git branch --track [branch] [remote-branch]

# 切换到指定分支，并更新工作区
git checkout [branch-name]

# 切换到上一个分支
git checkout -

# 建立追踪关系，在现有分支与指定的远程分支之间
git branch --set-upstream [branch] [remote-branch]

# 合并指定分支到当前分支
git merge [branch]

# 选择一个 commit，合并进当前分支
git cherry-pick [commit]

# 删除分支
git branch -d [branch-name]

# 删除远程分支
git push origin --delete [branch-name]
git branch -dr [remote-branch]
```

## 6. 标签

## 7. 查看信息

```shell
# 显示有变更的文件
git status

# 显示当前分支的版本历史
git log

# 显示commit历史，以及每次commit发生变更的文件
git log --stat

# 搜索提交历史，根据关键词
git log -S [keyword]

# 显示某个commit之后的所有变动，每个commit占据一行
git log [tag] HEAD --pretty=format:%s

# 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
git log [tag] HEAD --grep feature

# 显示某个文件的版本历史，包括文件改名
git log --follow [file]
git whatchanged [file]

# 显示指定文件相关的每一次diff
git log -p [file]

# 显示过去5次提交
git log -5 --pretty --oneline

# 显示所有提交过的用户，按提交次数排序
git shortlog -sn

# 显示指定文件是什么人在什么时间修改过
git blame [file]

# 显示暂存区和工作区的差异
git diff

# 显示暂存区和上一个commit的差异
git diff --cached [file]

# 显示工作区与当前分支最新commit之间的差异
git diff HEAD

# 显示两次提交之间的差异
git diff [first-branch]...[second-branch]

# 显示今天你写了多少行代码
git diff --shortstat "@{0 day ago}"

# 显示某次提交的元数据和内容变化
git show [commit]

# 显示某次提交发生变化的文件
git show --name-only [commit]

# 显示某次提交时，某个文件的内容
git show [commit]:[filename]

# 显示当前分支的最近几次提交
git reflog
```

## 8. 远程同步

```shell
# 下载远程仓库的所有变动
git fetch [remote]

# 显示所有远程仓库
git remote -v

# 显示某个远程仓库的信息
git remote show [remote]

# 增加一个新的远程仓库，并命名
git remote add [shortname] [url]

# 取回远程仓库的变化，并与本地分支合并
git pull [remote] [branch]

# 上传本地指定分支到远程仓库
git push [remote] [branch]

# 强行推送当前分支到远程仓库，即使有冲突
git push [remote] --force

# 推送所有分支到远程仓库
git push [remote] --all
```

## 9. 撤销

```shell
# 恢复暂存区的指定文件到工作区
git checkout [file]

# 恢复某个commit的指定文件到暂存区和工作区
git checkout [commit] [file]

# 恢复暂存区的所有文件到工作区
git checkout .

# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
git reset [file]

# 重置暂存区与工作区，与上一次commit保持一致
git reset --hard

# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
git reset [commit]

# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
git reset --hard [commit]

# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
git reset --keep [commit]

# 新建一个commit，用来撤销指定commit
# 后者的所有变化都将被前者抵消，并且应用到当前分支
git revert [commit]

# 暂时将未提交的变化移除，稍后再移入
git stash
git stash pop
```

## 10. 其他

```shell
# 生成一个可供发布的压缩包
git archive
```

