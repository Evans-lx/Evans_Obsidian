## Common Command

+ `ls` ：是一个常用的命令，用于列出当前目录中的文件和目录。
+ `ls -force` ：用于查看当前目录中的隐藏文件和目录。
+ `echo > filename` ：用于在当前目录创建新的空文件。
+ `mkdir foldername` ：用于在当前目录创建新的空文件夹。
+ `rm` / `del` ：用于删除当前目录中的文件。
+ `rd` ：用于删除当前目录的文件夹。
+ `git config list` ：用于查看 Git 配置的命令。执行这个命令会列出当前用户和当前仓库的所有 Git 配置选项及其对应的值。
+ `git help <verb>` ：用来查看特定 Git 命令的手册页的命令。
+ `git init` ：用于在当前目录下创建一个新的 Git 仓库。
+ `git status` ：用于查看当前工作目录的状态。
+ `.gitignore` 文件是用来指定 Git 忽略的文件和目录的规则文件。
```
# 忽略所有以 .log 结尾的文件
*.log

# 忽略 build 目录及其下所有内容
/build/

# 忽略 temp 目录下的所有 .tmp 文件
/temp/*.tmp

# 忽略 node_modules 目录
node_modules/

```
 
 ![[git_repository.png]]
+ `git add -A` ：用于将所有修改的文件和所有未跟踪的文件添加到暂存区。
	 + `git add filename` ：用于将指定的文件添加到 Git 的暂存区中。
+ `git reset` ：用于撤销之前的提交或暂存区的修改。
+ `git commit -m "description"` ：用于提交暂存区的修改并附带一个简短的提交描述。
+ `git log` ：用于显示当前分支的提交历史。
+ `git clone <url> <where to clone>` ：用于克隆远程仓库的命令。执行这个命令会从指定的 `<url>` 克隆远程仓库，并将其复制到指定的 `<where to clone>` 目录中。如果不指定目录，`git clone` 命令会默认将远程仓库克隆到当前目录下的一个新目录中，该目录的名称将与远程仓库的名称相同。
+ `git remote -v` ：用于查看当前 Git 仓库配置的远程仓库信息。执行这个命令会列出所有远程仓库的名称及其对应的 URL。
+ `git branch -a`：用于列出所有的本地分支和远程分支。执行这个命令会显示当前 Git 仓库中存在的所有分支，包括本地分支和远程分支。本地分支以绿色字体显示，而远程跟踪分支则以红色字体显示。
	+ `git branch` ：用于列出当前 Git 仓库中所有的分支，并显示当前所在的分支。执行这个命令会列出所有本地分支，并在当前所在的分支前面标记一个星号 `*`。
	+ `git branch -r` ：用于列出远程仓库中的所有分支。
+ `git diff`：用于比较工作区和暂存区之间的差异。执行这个命令会显示当前工作目录中已修改但尚未暂存的更改。
+ `git pull` 是一个 Git 命令，用于从远程仓库拉取(fetch)最新的修改，并将其合并(merge)到当前分支。执行这个命令会从远程仓库获取最新的提交，并尝试将这些提交合并到当前分支。具体来说，`git pull` 命令等价于执行了两个操作：`git fetch` 和 `git merge`。首先，它会使用 `git fetch` 命令从远程仓库获取最新的提交。然后，它会使用 `git merge` 命令将获取的提交合并到当前分支。
+ `git branch newbranch`：用于创建一个新的分支。执行这个命令会在当前所在的提交上创建一个新的分支
+ `git checkout` ：用于切换分支或恢复文件。
	1. **切换分支** ：如果你想要切换到已存在的分支，可以使用 `git checkout <branch>` 命令，其中 `<branch>` 是你想要切换到的分支的名称。
	2. **创建并切换到新分支**：如果你想要创建一个新的分支并立即切换到它，可以使用 `git checkout -b <new_branch>` 命令，其中 `<new_branch>` 是你想要创建的新分支的名称。
+ `git push -u origin branch` ：用于将本地分支推送到远程仓库，并将本地分支与远程分支关联起来。执行这个命令后，你就可以使用简单的 `git push` 命令来推送本地分支的修改到远程仓库。
+ `git merge newbranch` ：用于将另一个分支 `<newbranch>` 的修改合并到当前分支。
+ `git branch --merged` ：用于列出已经合并到当前分支的所有其他分支。
+ `git branch -d newbranch` ：用于删除指定的本地分支 `newbranch`。执行这个命令会删除指定的分支，但是只有在该分支的所有修改都已经合并到其他分支后才能执行成功。
+ `git branch origin --delete newbranch` ：删除远程跟踪分支。
## Common Workflow

#### Create new repository remotely and locally

1. Create a new repository in Github
2. Choose a local folder to clone the repository, a local repository is built as well
```
   $ git clone <url>
```
#### Connect new remote repository with a local project

1. Create a new repository in Github
2. Create a local repository in the project folder
```
   $ git init
   $ git add -A
   $ git commit
```
3. Connect them together and upload data
```
   $ git remote set-url --add <url>
   $ git push -u --all origin
```
#### Merge branch to change the master

1. Create a branch for desired feature
   ```
   $ git branch newbranch
   $ git checkout newbranch
	```
2. Commit local changes
```
   $ git status
   $ git add -A
   $ git commit -m "changes"
```
3. After commit push to remote
```
   $ git push -u origin newbranch
   $ git branch -a
```
4. Merge a branch
```
   $ git checkout master
   $ git pull origin master
   $ git merge newbranch
   $ git push origin master
```
5. Delete a branch
```
   $ git branch --merged
   $ git branch -d newbranch
   $ git branch -a
   $ git branch origin --delete newbranch
```
