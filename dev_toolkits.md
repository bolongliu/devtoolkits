# dev toolkits
## 1. git workflow

### 1.1 git and git lfs workflow
```shell
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
```

### 1.2 git base

**create a new repository on the command line**
```shell
echo "# readme" >> README.md
  git init
  git add README.md
  git commit -m "first commit"
  git branch -M main
  git remote add origin git@github.com:xxx/xxx.git
  git push -u origin main
```

**push an existing repository from the command line**
```shell
git remote add origin git@github.com:xxx/xxx.git
  git branch -M main
  git push -u origin master
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

```
