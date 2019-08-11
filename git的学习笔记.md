# git 的学习笔记

## windows上的powershell命令

- 合适的位置$mkdir learngit.... cd 进入文件夹 pwd

- 通过git init 把文件夹变为git可以管理的仓库

- 写一个README.txt文件保存在目录下，然后命令行输入git add README.txt （没任何显示，Unix的哲学是“没有消息就是好消息”）

- 通过命令 git commit -m "add reademe file"添加本次更新的信息

- 改变readme内容后利用git status查看状态，利用git diff readme.txt查看不同

- 通过git log 查看更改的记录，用cat 文件名来抓取内容

- 利用git reset --hard HEAD^ 来回退一个版本（悔棋）

- 只要还记得回退之前版本的commit id还可以返回（悔了自己的悔棋 :laughing:)具体为 git reset --hard 848728(只需部分id)

- 通过git reflog可以查阅历史命令，每次更改的commit id（不怕关电脑之后找不到时光机了:+1:)

- git add操作将文件添加到暂存区，git commit将暂存区文件提交至版本库，git commit只负责把暂存区文件提交如果某个文件为add过，则不会提交。

- 利用git checkout -- README.txt来把未add（工作区中）的文件改动撤销。

- 利用git reset HEAD README.txt来把已经add到暂存区的文件改动回退到工作区中，之后可以用上一步进行撤销。

- 利用前面的回退来撤销版本库即commit后的改动（仅限本地，远程就没办法了:cry:)

- 利用git rm test1.txt 来删除文件（已经提交到版本库的） 另外还可以通过git checkout --test1.txt 来恢复删除的文件但是只能恢复到删除前的最新版本。

- 远程仓库,通过命令ssh-keygen -t rsa -C “704849342@qq.com"然后一路回车生成ssh

- 在administrator目录的.ssh中可以cat id_rsa.pub获取公钥然后添加到github的ssh中就添加了远程仓库。

- 在github上创建新的仓库，然后可以在本地上对仓库下命令。

  git remote add origin git@github.com:Gozera/learngit.git

- 把本地内容推送到远程库上：git push -u origin master(如有报错直接选yes即可)只要本地作了提交利用这条命令就可以把最新修改提交到github

- 克隆仓库，利用git clone 加上仓库右上角的http。

- 创建分支命令 git checkout -b dev 通过git branch查看当前名字为dev的分支（此命令把创建与切换到dev分支命令合一）

  通过git checkout master来切回master分支

  最后通过git merge dev来合并dev分支到master上

  再用git branch -d dev来删除dev分支

- 未合并分支前在master上进行修改然后再合并会造成冲突必须先手动解决冲突后才可以进行合并。解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

- 合并分支时，加 --no-ff 参数在merge之后就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

- 利用git stash把当前工作现场储存起来。此时工作区就会干净适合创建新的分支，当想要继续储存的分支时利用命令 git stash apply （不把stash内容删除，还需要git stash drop 来删除）或者git stash pop 在恢复同时把stash内容删除。多个stash时先利用 git stash list查看再用git stash apply stash@{对应的number}。

- 利用git branch -D 分支名来对为合并的分支进行强行删除。通过git push origin dev 可以进行分支的推送，可以通过git checkout -b dev origin/dev来创建远程origin的dev分支到本地，并可以把修改push到远程。

- 利用git pull 可以把最新的抓取下来，如果pull失败可以根据提示来设置git branch --set-upstream-to=origin/dev dev(其中的dev均为分支名可根据实际情况进行替换)origin/dev为远程分支 dev为本地分支。

- rebase操作可以把本地未push的分叉提交历史整理成直线（git rebase命令）

- 创建标签以及编辑标签，可以为文件打上版本号。创建标签之前先切换到想要打标签的分支，利用 git tag V1.0就打上标签V1.0了，利用git tag命令可以查看标签。

- 对于历史的要打上标签可以用git log --pretty=oneline --abbrev-commit 查看commit id 然后利用git tag 内容 加上commit id 就可以打上同时打上标签后我们就可以快速提高标签来浏览内容了，如git show V1.0

- 还可以创建带有说明的标签，用-a 指定标签名，-m 指定说明文字：

  git tag -a V1.0 -m "version 1.0 released" 1094adb

  git tag -d V0.1删除标签V0.1

- 推送单个标签到远程 git push origin V1.0

  推送多个标签到远程 git push origin --tags

  删除远程标签，先本地删除，然后git push origin :refs/tags/V1.0

  注意origin后有一个空格。