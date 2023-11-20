# dev toolkits
## 1. git

### create a new repository on the command line
```shell
echo "# readme" >> README.md
  git init
  git add README.md
  git commit -m "first commit"
  git branch -M main
  git remote add origin git@github.com:xxx/xxx.git
  git push -u origin main
```

### push an existing repository from the command line
```shell
git remote add origin git@github.com:xxx/xxx.git
  git branch -M main
  git push -u origin main
```
