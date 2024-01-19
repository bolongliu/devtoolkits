# Docker 常用命令

## 1.容器操作：
- 基本指令
```
docker ps -aq：列出所有容器的 ID，包括正在运行的和已停止的。
docker ps -q：列出正在运行的容器的 ID。
```

- 启动容器
```
docker run -it -p 0.0.0.0:7860:7860 -v $PWD:/project_x <docker_name or docker_ID> /bin/bash /project_x/scripts/run.sh
```
- 停止容器
```
docker stop container ID
docker stop $(docker ps -q) #停止所有容器
```

- 删除容器
```
docker rm $(dcoker ps -aq)
```


# docker compose:容器和镜像编排工具

## 1.docker compose基本操作
- 启动
```
docker-compose up -d
```

- 停止
```
docker-compose down
```
- 示例
```
docker-compose up -d db #启动 Docker Compose 中定义的 "db" 服务。
docker-compose run --rm flaskapp /bin/bash -c "cd /opt/services/flaskapp/src && python -c  'import database; database.init_db()'"

- docker-compose run: 在 Docker Compose 服务中运行一个命令。
- --rm: 在运行完命令后自动删除容器。这有助于保持系统的清洁，不留下不必要的容器实例。
- flaskapp: 这是要运行的服务名称，即 Flask 应用的服务名称。
- /bin/bash -c "cd /opt/services/flaskapp/src && python -c 'import database; database.init_db()'": 这是在容器中执行的命令。解释如下：
- /bin/bash -c: 运行 bash 并执行后面的命令。
- cd /opt/services/flaskapp/src: 切换到指定的工作目录，这里是 Flask 应用的源代码目录。
- python -c 'import database; database.init_db()': 使用 Python 解释器运行一个短的脚本，这个脚本可能是负责初始化数据库的脚本。
```
