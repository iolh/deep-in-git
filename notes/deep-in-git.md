### 基础配置

1. 显示 config 的配置

   - git config --list

2. 配置用户信息

   - git config user.name 'xxx'
   - git config user.name 'xxx@xxx.com'

3. git config --scope 作用域设置

   - local 只对某个仓库有效
   - global 对当前用户所有仓库有效
   - system 对系统登录的所有用户有效

4. 清除配置

   git config --local --unset user.name

Linux 命令：

- pwd
- list -al
- cp

### 工作区和暂存区

文件提交：
git add <file> 添加文件到暂存区
git add -u 添加已跟踪的文件变更到暂存区，也就是说新增的未被 git 管理的除外
git add . 添加当前目录下所有的文件变更到暂存区
git add -A/-all 添加整个项目下所有的文件变更到暂存区

git commit -m'xxx' 提交到本地仓库

重置暂存区和工作区的所有变更

git reset --hard

文件重命名：

git mv <sourcefile> <destfile>

### 历史版本

git log
git log --oneline
git log --all
git log -n6
git log --graph

git checkout -b <branch>

### 探秘.git 目录

- HEAD 当前分支头指针

- config 本地配置

- refs

  - heads 开发分支头指针
  - tags 里程碑

- objects git 对象

git cat-file -p 查看文件内容
git cat-file -s 查看文件大小
git cat-file -t 查看文件类型

### commit,tree,blob 关系

commit,tree,blob 都是 git object

结构上

- commit
  - tree
    - blob

暂存文件会创建 blob 类型的 object
提交文件则会创建 tree 类型(即目录)的 object 以及 commit 类型(即快照)的 object

### 分离头指针

用途：实验代码，避免创建分支，删除分支

git checkout <xxxx>

git cherry-pick <commitHash>

### HEAD,branch 关系

HEAD 头指针，表示一次 commit，可能是某个 branch 上的 commit，也可能是单独的 commit

HEAD 特殊标识符

HEAD^ HEAD^^
HEAD~1 HEAD~2

### 删除分支

git branch -D <branch-name>
git branch -d <branch-name>

### 修改 commit 的 message

git commit --amend 最新 commit
git rebase -i <root|commitHash> 历史 commit
reword

### 合并 commit

- 连续的 commit
  git rebase -i <root|commitHash>
  squash
- 非连续的 commit
  git rebase -i <root|commitHash>
  调整位置
  squash

### 两次 commit 比较差异

git diff <commitHash> <commitHash> -- <file>

### 暂存区和 HEAD 比较差异

git diff --cached

### 工作区和暂存区比较差异

git diff

### 暂存区恢复

- 全部恢复
  git reset HEAD
- 部分恢复
  git reset HEAD -- <file>

### 工作区恢复到暂存区

git checkout -- <file>

### 清除 commit

git rest --hard <commitHash>

### 删除文件

git rm <file>

### 临时变更

git stash 贮藏变更
git stash pop 取出变更，不保留记录
git stash apply 取出变更，保留记录

### 忽略管理部分文件

.gitignore

git rm -- cached <file>

### 传输协议

- 哑协议
  - /path/to/repo.git
- 智能协议
  - file:///path/to/repo.git
  - http/https
  - ssh

### 备份

git clone --bare <filePath>
git remote add origin https://github.com/iolh/deep-in-git.git
git push --set-upstream origin main
