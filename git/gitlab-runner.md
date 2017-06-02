# gitlab runner 配置
## for docker
### 安装，运行runner
runner负责编译、测试、打包、发布，可以把runner和代码库部署在一起，不过通常runner和代码库会分开部署。我们把代码push到gitlab后，gitlab就会触发runner构建我们的项目。使用docker安装runner，可以直接运行命令：
```
docker run -d --name gitlab-runner --restart always \
-v /var/run/docker.sock:/var/run/docker.sock \
-v /srv/gitlab-runner/config:/etc/gitlab-runner \
gitlab/gitlab-runner:latest
```
如果本地还没有`gitlab/gitlab-runner:latest` 的docker包，docker会先拉取，然后再运行你指定的包。我们也可以先手动拉取要安装的包：
```
docker pull gitlab/gitlab-runner:latest
```
查看本地的包：
```
docker images
```
`-d` 表示以守护进程的方式运行，`--name` 为运行的docker容器命名，`--restart` 出错的时候自动重启。查看运行的容器命令：
```
docker ps -a
```
`-a` 表示查看所有的容器，不管是正在运行的还是停止的。

### 注册runner
```
docker exec -it gitlab-runner gitlab-runner register
```
`-i` 打开标准IO，`-t` 终端交互的方式运行，`gitlab-runner` 容器的名称，也可以用容器id，`gitlab-runner register` 执行命令。

注册时会提示填入CI地址和token，在gitlab的CI配置界面找到CI url和token填入即可

### 通过内网拉取docker镜像
通常在`/etc/docker`下，有配置文件，添加配置：
```
{
    "registry-mirrors": ["http://docker.gf.com.cn/"]
}
```