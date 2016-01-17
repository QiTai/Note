#Note
 + Reverting Working Copy to Most Recent Commit
  * git reset --hard HEAD
  * where HEAD is the last commit in your current branch. Refer to [Revert&Reset](http://stackoverflow.com/questions/4114095/revert-git-repo-to-a-previous-commit)
 + 用户信息
  * git config --global user.name "QiTai"
  * git config --glabal user.email "qitai1993@163.com"
 + 差异分析工具：
  * git config --global merge.tool vimdiff
 + 在工作目录中初始化新仓库
  * git init 
 + 对文件进行跟踪
  * git add *.c
 + 取消对某个文件的跟踪
  * git rm --cached -r FILENAME
 + 从现有仓库中克隆(ssh协议)
  * git clone git@github.com:QiTai/my_code.git 
  * （实际是自动创建了本地master的分支用于跟踪远程仓库中的master分支）
 + 检查当前文件的状态
  * git status 
 + 追踪新文件
  * git add README
 + 从暂存区域移除某个文件
  * git rm grit.gemspec
 + 移动文件
  * git mv file_from file_to
 + 查看提交历史
  * git log
 + 提交
  * git commit -m ' '
 + 修改最后一次提交
  * git commit -amend
 + 检出某个分支的某个版本
  * git checkout master
## 远程仓库
 + 显示对应的克隆地址
  * git remote -v
 + 从远程仓库抓取数据
  * git fetch [remote-name] 有一点需要记住：fetch命令只是将远端的数据拉到本地仓库，并不自动合并到当前工作分支。必须手动合并到当前分支(git meger origin/serverfix)，或者
git checkout -b serverfix origin/serverfix;创建一个本地的新的分支。
如果设置了某个分支用于跟踪某个远端仓库的分支（git checkout -b sf orgin/server)或者用简化命令（git checkout --track origin/serverfix)，可以用git pull命令自动抓取数据下来，然后将远端分支自动合并到本地仓库中的当前分支。

 + 将远程仓库的数据更新到当前clone的目录下：
  * git pull(但是要注意：如果本地clone目录下已经做了修改，要先commit）
 + 推送数据到远程仓库
  * git push origin master
 + 查看远程仓库
  * git remote show origin
 + 远程仓库的删除和重命名
  * git remote rename pb paul
  * git remote rm paul
 + 分支的创建和切换
  * git branch iss153
  * git checkout iss153
  * git checkout -b iss53
 + 分支合并
  * git checkout master
  * git merge hotfix
 + 忽略某些文件  
  * 创建.gitignore文件，列出要忽略的文件模式
