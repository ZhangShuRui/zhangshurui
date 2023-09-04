# branch

1.列出分支，-a参数是列出所有分支，包括远程分支 git branch [-a]

2.创建一个本地分支 git branch branchname

3.创建一个分支，并切换到该分支 git checkout -b branchname

4.删除一个本地分支 git branch -d branchname

5.删除一个远程分支 git push origin --delete branchname

6.删除一个远程分支，通过push一个空的分支来覆盖原来的分支，以达到删除远程分支的目的 git push origin :branchname

7.更新本地git分支与远程分支同步（保留本地存在的分支） git remote update origin --prune

8.删除本地多余分支（即远程已经不存在的分支） git remote prune origin

8.查看本地分支和追踪情况 git remote show origin

# tag

1.列出所有tag git tag

2.列出远程所有tag，注意git版本1.7（包括1.7）一下后边需要加上git仓库地址 git ls-remote --tags

3.创建一个tag git tag -a tagname

4.创建一个加描述的tag git tag -a tagname [-m <msg>]

5.删除本地tag git tag -d tagname

6.删除远程tag git push origin --delete tag tagname

7.删除远程tag，与6不同的是，这是推送一个空的tag覆盖掉原来的tag，以达到删除tag的目的 git push origin :refs/tags/<tagname>
8.推送tag git push origin tagName

# git命令

1. 取消暂存文件（将文件从add的暂存中删掉） git restore --stage xxx
或

git reset HEAD xxx (若HEAD后边未指定文件，则取消所有文件的暂存)