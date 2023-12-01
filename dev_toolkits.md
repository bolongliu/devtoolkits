# dev toolkits
## 1. git workflow

### 1.1 git and git lfs workflow
```shell
# 将本地项目提交github远程仓库
git lfs install
git lfs track "*.psd"
git init
git add .
git commit -m "first commit"
git push -u origin master

# 打tag后推送
git tag v1.0.1
git commit -m "add tag v1.5.2"
# push单个tag，命令格式为：git push origin [tagname]
git push origin v1.0.1 #将本地v1.0的tag推送到远端服务器
# push所有tag，命令格式为：git push [origin] --tags
git push --tags
git push origin --tags

# 分支管理
git checkout -b dev #创建dev分支，然后切换到dev分支
git branch #查看当前分支,星号(*)表示当前所在分支
# dev分支的工作成果合并到master分支上
git checkout master #切换回master分支
git merge dev #git merge命令用于合并指定分支到当前分支。
git branch -d dev #删除dev分支

# 把新建的本地分支push到远程服务器，远程分支与本地分支同名（当然可以随意起名）：
git push origin dev:dev

# 删除远程分支
git push origin :dev #推送一个空分支到远程分支，其实就相当于删除远程分支
git push origin --delete dev

# 修改提交记录
想要合并1-3条，有两个方法
0. git log --oneline

1.从HEAD版本开始往过去数3个版本
git rebase -i HEAD~3

2.指名要合并的版本之前的版本号
git rebase -i 3a4226b
请注意3a4226b这个版本是不参与合并的，可以把它当做一个坐标
执行了rebase命令之后，会弹出一个窗口，头几行如下：
pick 3ca6ec3   '注释**********'
pick 1b40566   '注释*********'
pick 53f244a   '注释**********'

2.将pick改为squash或者s,之后保存并关闭文本编辑窗口即可。
pick 3ca6ec3   '注释**********'
s 1b40566   '注释*********'
s 53f244a   '注释**********'

3.然后保存退出，Git会压缩提交历史，如果有冲突，需要修改，修改的时候要注意，保留最新的历史，不然我们的修改就丢弃了。修改以后要记得敲下面的命令：
git add .  
git rebase --continue  

4.如果你想放弃这次压缩的话，执行以下命令：
git rebase --abort 

一种极端情况是想从当前分支的第一个提交开始rebase，可以使用以下命令
git rebase -i --root
```


### 1.2 git base

**1.2.1 create a new repository on the command line**
```shell
echo "# readme" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:xxx/xxx.git
git push -u origin main

# 查看提交记录
git log
# 找到提交前的commit,重置
git reset xxxxx
```

**1.2.2 push an existing repository from the command line**
```shell
git remote add origin git@github.com:xxx/xxx.git
git branch -M main
git push -u origin master
```

**1.2.3 git branch**

Git鼓励大量使用分支：
```shell
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>或者git switch <name>
创建+切换分支：git checkout -b <name>或者git switch -c <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>
```
**常用操作**

1. 彻底清除git所有历史提交记录使其为“新”库

- 开发中未制定、遵循 git 管理项目标准，随意(不规范)的提交 严重“污染了”提交历史，使开发主线 “脏乱”;
- 基于以前的仓库重新开发，这样可保留以前的配置等文件，但是需要删除全部的历史记录、tag、分支等;
- 由于自己或其他方面特殊需求，需要保留仓库的部分属性(创建时间，说明，主页等)，但需要清除历史记录，使其为“新库”。
基于以上3方面的需求，需要提供一个 在不删除原仓库的前提下，清除原仓库的所有历史提交记录(包含：分支、tag) 解决方案。

```shell
1.创建新分支
git checkout --orphan latest_branch

2.添加所有文件
git add .
# 或 git add -A

3.commit代码
git commit -m "init"

4.删除原来的主分支(master)
git branch -D master

5.把当前分支重命名为master
git branch -m master

6.最后把代码推送到远程仓库
注意： 有些仓库有 master 分支保护，不允许强制 push，需要在远程仓库项目里暂时把项目保护关掉才能推送。
git push -f origin master

7.从远程库拉取更新代码(测试)
git pull
如果别人pull不下来可以敲
git pull -r

8.确定清除历史记录的结果
# 1.查看提交日志
git log --pretty=oneline

# 2.查看分支信息
# 列出所有本地分支
git branch
# 列出所有远程分支
git branch -r
# 列出所有本地分支和远程分支
git branch -a

# 3.查看 tag 信息
# 查看本地标签
git tag
# 查看远程标签
git ls-remote --tags
```

### 1.3 git lfs workflow

Use git lfs for large file size of 100MB

**install**
```shell
# apt/deb: 
sudo apt-get install git-lfs
# yum/rpm: 
sudo yum install git-lfs
```
**workflow**
```shell
git lfs install
git lfs track "*.psd"
git add .
git commit -m "Use git lfs for large file size of 100MB"
git push origin master
```
