### GIT命令
```
git init		初始化git仓库				
git status		查看文件状态				
git add .		将当前文件夹提交至暂存区				
git commit -m 'modify'		提交文件至版本库				
git log --pretty=oneline		查看文件版本列表				
git reset --hard HEAD^		回退至上一版本				
git reset --hard 07279E6		根据commit id回退版本				
git reflog		查看文件修改的commit id				
cat index.html		查看文件				
git diff HEAD -- index.html		查看当前工作区与版本库区别				
git checkout -- index.html		撤销文件修改恢复至暂存区或版本库状态				
git reset HEAD index.html		把暂存区的修改回退到工作区				
rm test.txt		删除工作区文件				
git rm test.txt		删除暂存区文件				
用户主目录		我的电脑C盘---->用户/user---->Administrator/自定义用户名文件夹				
"ssh-keygen -t rsa -C "971770324@qq.com""			创建ssh key			
链接本地仓库和github远程库						
		git remote add origin 远程clone地址				
		git push -u origin master				
git checkout -b dev		创建分支并切换至此分支				
						
git branch		查看分支列表带*号的就是当前分支				
git checkout master		切换至master分支				
git merge dev		合并dev分支到当前分支				
git branch -d dev		删除dev分支				
git log --graph --pretty=oneline --abbrev-commit			查看分支合并图			
git merge --no-ff -m 'note' dev		禁用fast forward模式合并分支				
git stash		暂存工作区				
git stash pop 		回到工作现场并删除stash				
git stash list 		查看stash列表				
git stash apply 某某stash		回到某个stash现场				
git stash drop		删除stash				
git branch -D dev		强行删除没有合并过的分支dev(D得大写)				
git remote	查看远程库信息					
git remote -v	查看远程库详细信息					
git push origin master		把本地的master分支推送到远程库相应分支				
git checkout -b dev origin/dev		创建远程origin的dev分支到本地				
git branch --set-upstream-to=origin/dev dev			git pull失败时指定本地dev分支与远程origin/dev分支的链接			
git rebase		把本地未push的分叉提交历史整理成直线				
git tag v0.1		为最新的commit打标签				
git tag v0.1 f52c633		为commitid是f52c633的提交打标签				
git tag -a v0.1 -m 'this is a new version' f52c633			创建带有说明的标签			
git tag		查看标签				
git show v0.9		查看标签信息				
git tag -d v0.1		删除标签				
git push origin :refs/tags/v0.1		删除已推送到的标签				
git push origin v0.1		推送本地标签到远程				
git push origin tags		推送全部未推送过的本地标签到远程				
						
创建.gitignore文件将不想上传的文件的文件名加入gitignore里,然后将.gitignore文件上传至版本库，可以让Git忽略此文件的修改						
window下无法直接创建.gitignore文件，可以建个文件另存为.gitignore						
git add -f abc.txt		强行添加.gitignore里的文件至版本库				
git check-ignore -v abc.txt		查看.gitignore文件的哪条规则忽略了abc.txt文件
Git提交记住用户名和密码  git config --global credential.helper store		
```
