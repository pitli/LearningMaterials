### Git常用命令总结



`git config`：配置git的相关信息

- 设置用户名

  ```shell
  git config --global user.name "name"
  ```

- 设置用户邮箱

  ```shell
  git config --global user.email "email"
  ```

- 查看git所有配置信息

  ```shell
  git config --list
  ```

- 查看配置的用户名

  ```shell
  git config user.name
  ```

- 查看配置的用户邮箱

  ```shell
  git config user.email
  ```

- 定义命令别名

  ```shell
  git config --global alias.br branch
  #则git branch可用 git br代替(也可自定义其他命令的别名，主要合理方便即可)
  ```

`git init`：在当前目录初始化仓库，并创建.git的子目录，该目录包含初始化Git仓库所必须的文件

`git status`：显示文件状态，红色表示文件已修改但没提交到暂存区，绿色表示已提交到暂存区

`git add`：将文件从工作目录添加至暂存区

- 把所有修改的信息添加到暂存区

  ```
  git add .
  ```

- 把所有跟踪文件中被修改过或已删除的文件信息添加至暂存区，不处理那些没有被跟踪的文件

  ```
  git add -u或git add -- update
  ```

- 把所有跟踪文件中被修改过或已删除文件和所有未跟踪的文件信息添加到暂存区

  ```
  git add -A或git add --all
  ```

- 已经被提交到暂存区的文件，通过该命令撤销提交

  ```
  git reset HEAD -- fileName
  ```

`git commit`：将暂存区的修改提交到本地仓库，同时生成commit-id

- 将暂存区的修改提交到本地仓库，并添加注释

  ```
  git commit -m "message"
  ```

- 将本地工作区中修改后还未使用`git add .`命令添加到暂存区中的文件也提交到本地仓库

  ```
  git commit -a -m "message"或 git commit -am "message"
  ```

- 修改最后一次提交（可用于漏掉某个文件的提交或重新编辑信息）

  ```
  git commit --amend
  ```

`git pull`：获取远程仓库某个分支的更新，再与本地指定分支合并`git pull <远程仓库名><远程分支名>:<本地分支名>`

- 取回远程仓库上的dev分支与本地的master分支合并(origin代表远程仓库的标识，在添加远程仓库时设置)

  ```
  git pull origin dev:master
  ```

- 取回远程仓库上的dev分支与当前分支合并

  ```
  git pull origin dev
  ```

`git fetch`：将远程仓库上所有分支的更新取回本地，并记录在`.git/FETCH_HEAD`中

- 获取远程仓库上master分支的代码

  ```
  git fetch origin
  ```

- 在本地新建test分支，并将远程仓库上master分支代码下载到本地test分支

  ```
  git fetch origin master:test
  ```

`git push`：将本地分支的更新推送到远程仓库上

- 将本地`master`分支的更新推送到远程主机上

  ```
  git push origin master
  ```

- 删除远程dev分支

  ```
  git push origin --delete dev
  ```

`git branch`：主要做分支管理操作，以下命令针对本地仓库，不影响远程仓库

- 查看本地分支

  ```
  git branch
  ```

- 查看本地和远程分支

  ```
  git branch -a
  ```

- 新建名字为test的分支

  ```
  git branch test
  ```

- 将test分支名字改为dev

  ```
  git branch -m test dev
  ```

- 删除名字为dev的分支

  ```
  git branch -d dev
  ```

- 强制删除名字为dev的分支

  ```
  git branch -D dev
  ```

`git checkout`：常用于创建和切换分支以及撤销工作区的修改

- 切换到tag为v1.0.0时对应的代码

  ```
  git checkout v1.0.0
  ```

- 在tag为v1.0.0的基础上创建分支名为test的分支

  ```
  git checkout -b test v1.0.0
  ```

- 把当前目录所有修改的文件从HEAD中移除并且把它恢复成未修改时的样子

  ```
  git checkout .
  ```

- 撤销工作目录中文件的修改（文件有改动但还未`git add`）

  ```
  git checkout -- fileName
  ```

`git tag`：主要对项目标签进行管理

- 查看已有的标签历史记录

  ```
  git tag
  ```

- 给当前最新的commit打上标签

  ```
  git tag <标签的定义>
  ```

- 给对应的commit id打上标签

  ```
  git tag <标签定义> <commit id>
  ```

`git log`：查看历史提交记录

- 查看历史提交记录

  ```
  git log
  ```

- 将每条历史提交记录展示成一行

  ```
  git log --oneline
  ```

- 查看某个人的提交记录

  ```
  git log --author="name"
  ```

- 显示ASCII图形表示的分支合并历史

  ```
  git log --graph
  ```

- 显示前n条记录

  ```
  git log -n
  ```

- 显示某个日期之后的记录

  ```
  git log --after="2018-10-1"
  ```

- 显示某个日期之前的记录

  ```
  git log --before="2018-10-1"
  ```

- 显示某两个日期之间的记录

  ```
  git log --after="2018-10-1" --before="2018-10-7"
  ```

`git reset`：撤销暂存区的修改或本地仓库的提交

- 撤销已经提交到暂存区的文件

  ```
  git reset HEAD fileName或git reset --mixed HEAD fileName
  ```

- 撤销所有提交

  ```
  git reset HEAD .或git reset --mixed HEAD .
  ```

- 将头指针恢复，已经提交到暂存区以及工作区的内容都不变

  ```
  git reset --soft commit-id或git reset --soft HEAD~1
  ```

- 将头指针恢复并且撤销暂存区的提交，但是工作区的内容不变

  ```
  git reset --mixed commit-id或git reset --mixed HEAD~1
  ```

- 将所有内容恢复到指定版本 (commit-id通过`git log`查看，取前六位，HEAD~1表示前一次提交)

  ```
  git reset --hard commit-id或git reset --hard HEAD~1
  ```

`git remote`：管理远程仓库

- 查看关联的远程仓库的名称

  ```
  git remote
  ```

- 查看关联的远程仓库的详细信息

  ```
  git remote -v
  ```

- 添加远程仓库的关联

  ```
  git remote add origin <远程仓库地址>
  ```

- 删除远程仓库的关联

  ```
  git remote remove <远程仓库名称>
  ```

- 修改远程仓库的关联

  ```
  git remote set-url origin <新的远程仓库地址>
  ```

- 更新远程仓库的分支

  ```
  git remote update origin --prune
  ```

`git merge`：分支的合并

- 如果当前是master分支，需要合并dev分支

  ```
  git merge dev
  ```

`git stash`：如果当前分支所做的修改你还不想提交，但又需要切换到其他分支去查看，就可以使用`git stash`保存当前的修改

- 保存当前进度

  ```
  git stash
  ```

- 查看已经保存的历史记录

  ```
  git stash list
  ```

- 重新应用某个已经保存的进度，并且删除进度记录

  ```
  git stash pop <历史进度id>
  ```

- 重新应用某个已经保存的进度，但不删除进度记录

  ```
  git stash apply <历史进度id>
  ```

- 删除某个历史进度

  ```
  git stash drop <历史进度id>
  ```

- 删除所有的历史进度

  ```
  git stash clear
  ```

`gitignore`：忽略那些没必要的提交，比如系统环境或程序运行时产生的文件。GitHub为我们提供了各个语言的gitignore合集[github/gitignore](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fgithub%2Fgitignore)，其中也包括[Android.gitignore](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fgithub%2Fgitignore%2Fblob%2Fmaster%2FAndroid.gitignore)

## 将本地新建项目提交到远程仓库的步骤

- 初始化本地仓库`git init`
- 将本地内容添加至git本地暂存区中`git add .`
- 将暂存区添加至本地仓库中`git commit -m "first commit"`
- 添加远程仓库路径`git remote add origin git@github.com:pitli/git-tutorial.git`
- 将本地内容push至远程仓库中`git push -u origin master`

## 秘钥配置

生成新的秘钥：`ssh-keygen -t rsa -C "eamil"`

完成后会有如下显示：

```
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/gybguohao/.ssh/id_rsa。
Your public key has been saved in /Users/gybguohao/.ssh/id_rsa.pub。
The key fingerprint is:
SHA256:5V6ZCQNS/3bVdl0GjGgQpWMFLazxTslnKbW2B1mbC+E eamil
```

如果服务器端需要公钥, 直接复制`C:\Users\用户名\.ssh`目录下的id_rsa.pub内容即可。