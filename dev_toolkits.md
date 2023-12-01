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
git push origin v1.0 #将本地v1.0的tag推送到远端服务器
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
