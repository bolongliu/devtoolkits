# dev toolkits
# git分支命名规范与工作流程
## 快速预览

| 分支           | 命名               | 说明                                                       |
| -------------- | ------------------ | :--------------------------------------------------------- |
| 主分支         | **master**         | 主分支，所有提供给用户使用的正式版本，都在这个主分支上发布 |
| 预发布分支     | **release/v1.0.0** | 发布正式版本之前，最终确认的分支                           |
| 开发主分支     | **develop/v1.0.0** | 开发主分支，永远是功能最新最全的分支                       |
| 功能开发分支   | **feature/xxx**    | 新功能分支，某个功能点正在开发阶段                         |
| 紧急bugfix分支 | **hotfix/xxx**     | 修复线上代码的 bug                                         |

## 详解
**master**：主分支，永远是可用的、稳定的、可直接发布的版本，不能直接在该分支上开发
**release/v1.0.0** (bugfix)：预发布分支，预发布分支是从 develop 分支上面分出来的。【**预发布环境**，该分支修复bug，稳定后合并进 develop 和 master 分支】
**develop/v1.0.0**：开发主分支，代码永远是最新，所有新功能以这个分支来创建自己的开发分支，该分支只做只合并操作，不能直接在该分支上开发。【**测试环境**，feature分支修复bug后，再合入】

**feature/xxx** (bugfix)：功能开发分支，在 develop 上创建分支，以自己开发功能模块命名，开发完成或修复bug后合并到 develop 分支

**hotfix/xxx**：紧急bug修改分支，项目上线之后可以会遇到一些环境问题需要紧急修复，在对应版本的release 分支上创建，流程跟 release 分支相似，修复完成后合并 release 分支，根据情况判断需不需要再合并到 develop 和 master 分支

## 注意事项

- 一个分支尽量开发一个功能模块，不要多个功能模块在一个分支上开发。
- 开发过程中，如果组员A开发的功能依赖组员B正在开发的功能，可以待组员B开发好相关功能之后，组员A直接 pull 组员B的分支下来开发，不需要先将组员B的分支 merge 到 **develop** 分支。
- **feature** 分支在申请合并之前，最好是先 pull 一下 **develop** 主分支下来，看一下有没有冲突，如果有就先解决冲突后再申请合并。

## 工作流程
1. 克隆项目
2. 迁出并创建dev分支，使其跟踪远程的origin/dev分支
3. 在dev分支基础上创建自己的分支member
4. 在自己的分支上添加文件
5. 在自己的分支上修改文件
6. 合并到dev分支
7. 推送dev分支到origin/dev分支
8. 更新.gitignore文件。从dev新建一个分支ignore
如果预测变更频繁就建立一个远程分支,现在一般都有模板,偶尔有个没有忽略的直接在dev分支上修改就可以了
忽略更新文件尽快合并推送到origin/dev分支（避免两个组员同时更改该文件造成冲突）

## git提交记录规范
每个git commit记录都需要按照固定格式，具体格式为：
- 第一行：作者，功能模块名称或者 功能模块ID
- 第二行：提交描述。中英文均可
  - ： + 增加代码
  - ： * 修改代码
  - ： - 删除代码

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

# 打错tag并推送后修改
删除远程标签
git push origin --delete v1.1
删除本地标签
git tag -d v1.1

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


### 1.4 代码仓库管理

1. 提交经过测试好的dev分支到github

```shell
git add .
git commit -m "ARUCFv2.1.0.20320619.dev"
git tag v2.1.0 dev
git push origin dev
```

2. 合并经过测试好的dev分支到master分支上面 

```shell
git checkout master
git merge dev
git add .
git tag v2.1.0
git commit -m "ARUCFv2.1.0.20320619"
git push -f
git push --tags
```

**版本更新checklist**

1. 在dev分支上测试代码，完全没问题后再等一天后提交到git暂存区
2. 将dev分支的代码合并到master分支上
3. 修改代码中头文件中的版本号:Version: v2.0.x
4. 切换过到master分支，打上发布标签 git tag v2.0.x
5. 提交master分支
6. 将master分支推送到远程仓库

**常用指令**

| num  | git comand                              | Description                        |
| :--: | :-------------------------------------- | :--------------------------------- |
|  1   | git checkout dev                        | 切换为dev分支                      |
|  2   | git checkout master                     | 切换为master分支                   |
|  2   | git merge dev                           | 将dev分支合并到master分支上        |
|  3   | git tag v2.0.x                          | 将当前分支打上v2.0.x的tag          |
|  4   | git push                                | 将本地仓库推送到远程仓库           |
|  5   | git push --tags                         | 将本地所有tag推送到远程            |
|  6   | git tag -d v2.0.x                       | 删除本地v2.0.x tag                 |
|  7   | git push origin :refs/tags/v2.0.x       | 删除远程标签v2.0.x                 |
|  8   | git branch -d dev                       | 删除分支 dev                       |
|  9   | git branch                              | 查看本地所有分支                   |
|  10  | git status                              | 查看当前状态                       |
|  11  | git merge <branch>                      | 合并指定分支到当前分支，保留两个   |
|  12  | git rebase <branch>                     | 合并指定分支到当前分支，只保留一个 |
|  13  | git rm --cached <file>                  | 停止跟踪文件，不会从磁盘中删除     |
|  14  | git rm -r <directory>                   | 递归删除指定目录下的文件           |
|  15  | git rm <file>                           | 删除文件（将从磁盘中删除文件）     |
|  16  | git branch --no-merged                  | 查看所有分支未合并到当前分支的分支 |
|  17  | git checkout -b dev                     | 从当前分支拉copy开发分支           |
|  18  | git push origin dev                     | 把新建的dev分支push到远端          |
|  19  | git branch --set-upstream-to=origin/dev | 关联远程dev分支                    |



