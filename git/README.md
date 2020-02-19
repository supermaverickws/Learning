
# Learning git  

> [git init] 初始化git项目  

目录下会自动创建 [.git] 文件夹。[ls -ah]可以查看

> [ git add {file} ] 添加文件到git

>[ git commit -a -m "{commit info}" ] 批量添加文件到仓库 并会生成一个快照和版本号

> 修改add后的文件需要再次add，或者添加 -a 才能commit成功，可以用【git status】 测试
因为git监视的是文件的修改。每次修改都需要 add,才能 commit

> [ git status ] 查看本地仓库修改状态

* 如果新建的文件没有 [git add] 是不会纳入 [git status]统计中的

> [ git diff {file} ] 查看文件修改

> [ git log ] 查看历史commit记录  

> [ git reset --hard HEAD^ / {5ca3226} ] 回退到最近一个版本 或某个版本

> [ git checkout -- {file} ] 覆盖本地文件。丢掉本次修改  

> [ git reset HEAD {file} ] 可以把文件从暂存区撤销(就是把文件 add 到暂存区后，reset 到工作区)  

> [ git rm {file} ]  rm 删除文件后，[git rm] 然后 [git commit] 删除文件，误删可以[git checkout]

> [ git remote add origin git@github.com:{supermaverickws/Learning.git} ] 将本地仓库与远程仓库关联

> [ git push origin master ] 提交代码到git  

* [ssh-keygen -t rsa -b 4096 -C "youremailname@example.com"]在用户目录下生成 [.ssh]文件夹并cd到此目录内。用[more id_rsa.pub]查看公钥详情。把公钥详情添加到 git 账户中

> [ git clone {url}] 克隆远程仓库

# 分支

* [git branch {mybranch}] 创建分支
* [git checkout {mybranch}] 或者 [git switch {mybranch}] 切换分支
* [git checkout -b {mybranch}] 或者 [git switch -c {mybranch}]创建并切换分支
* [git branch] 查看当前分支
  * [git branch -a] a = all 查看本地和远程所有分支
  * [git branch -r] r=remote 查看远程所有分支
* [git merge --no-ff -m "{merge info}"{branch}] 合并分支。切换到master分支 合并到master分支上
* [git branch -d {branch}] 删除分支
* [git stash] 保存现场
* [git stash list] 保存现场的列表
* [git stash apply stash@{0}] 恢复现场
* [git stash pop ] 恢复线程并删除记录, 当前在哪个分支，就会恢复最新的保存到当前分支下，非必须原来的分支
* [git cherry-pick {4c805e2}] 复制修改 先在改动分支 commit 后得到版本号，然后切换到要复制的分支，执行 cherry-pick 命令 复制修改。
* [ git push origin {dev} ] 分支推送的远程
* [ git push origin --delete dev ] 删除远程分支
* [ git pull origin {dev} ] 拉取分支代码
* [git checkout -b branch-name oqrigi,
n/branch-name ] 例如[git checkout -b dev origin/dev] 在本地创建和远程分支对应的分支
* [ git branch --set-upstream branch-name origin/branch-name ] 建立本地分支和远程分支的关联
* [git log --graph --pretty=oneline --abbrev-commit] 查看远程提交日志

# 标签

* [ git tag ] 查看标签
* [ git tag {v0.1}] 打标签
* [ git tag {v0.1} {ads}] 给分支打标签
* [ git show {v0.1} ] 查看标签
* [ git tag -d {v0.2}] 删除一个标签
* [ git push origin :refs/tags/<tagname> ]删除一个远程标签
* [ git push origin <tagname> ] 远程推送一个标签
* [ git push origin --tags ] 推送全部标签

# git Flow  

```
Git Flow 的常用分支
Production 分支
也就是我们经常使用的Master分支，这个分支最近发布到生产环境的代码，最近发布的Release， 这个分支只能从其他分支合并，不能在这个分支直接修改
Develop 分支
这个分支是我们是我们的主开发分支，包含所有要发布到下一个Release的代码，这个主要合并与其他分支，比如Feature分支
Feature 分支
这个分支主要是用来开发一个新的功能，一旦开发完成，我们合并回Develop分支进入下一个Release
Release分支
当你需要一个发布一个新Release的时候，我们基于Develop分支创建一个Release分支，完成Release后，我们合并到Master和Develop分支
Hotfix分支
当我们在Production发现新的Bug时候，我们需要创建一个Hotfix, 完成Hotfix后，我们合并回Master和Develop分支，所以Hotfix的改动会进入下一个Release
```
