# docker教程
将当前用户添加到docker用户组

为了避免每次使用docker命令都需要加上sudo权限，可以将当前用户加入安装中自动创建的docker用户组(可以参考官方文档)：
创建工作用户acs并赋予sudo权限

登录到新服务器。打开AC Terminal，然后：

ssh root@xxx.xxx.xxx.xxx  # xxx.xxx.xxx.xxx替换成新服务器的公网IP
创建acs用户：

adduser acs  # 创建用户acs
usermod -aG sudo acs  # 给用户acs分配sudo权限
配置免密登录方式

退回AC Terminal，然后配置acs用户的别名和免密登录，可以参考4. ssh——ssh登录。

配置新服务器的工作环境

将AC Terminal的配置传到新服务器上：

scp .bashrc .vimrc .tmux.conf server_name:  # server_name需要换成自己配置的别名
安装tmux和docker

登录自己的服务器，然后安装tmux：

sudo apt-get update
sudo apt-get install tmux
打开tmux。（养成好习惯，所有工作都在tmux里进行，防止意外关闭终端后，工作进度丢失）

然后在tmux中根据docker安装教程安装docker即可。

sudo usermod -aG docker $USER
执行完此操作后，需要退出服务器，再重新登录回来，才可以省去sudo权限。

镜像（images）

docker pull ubuntu:20.04：拉取一个镜像
docker images：列出本地所有镜像
docker image rm ubuntu:20.04 或 docker rmi ubuntu:20.04：删除镜像ubuntu:20.04
docker [container] commit CONTAINER IMAGE_NAME:TAG：创建某个container的镜像
docker save -o ubuntu_20_04.tar ubuntu:20.04：将镜像ubuntu:20.04导出到本地文件ubuntu_20_04.tar中
docker load -i ubuntu_20_04.tar：将镜像ubuntu:20.04从本地文件ubuntu_20_04.tar中加载出来
容器(container)

docker [container] create -it ubuntu:20.04：利用镜像ubuntu:20.04创建一个容器。
docker ps -a：查看本地的所有容器
docker [container] start CONTAINER：启动容器
docker [container] stop CONTAINER：停止容器
docker [container] restart CONTAINER：重启容器
docker [contaienr] run -itd ubuntu:20.04：创建并启动一个容器
docker [container] attach CONTAINER：进入容器
先按Ctrl-p，再按Ctrl-q可以挂起容器
docker [container] exec CONTAINER COMMAND：在容器中执行命令
docker [container] rm CONTAINER：删除容器
docker container prune：删除所有已停止的容器
docker export -o xxx.tar CONTAINER：将容器CONTAINER导出到本地文件xxx.tar中
docker import xxx.tar image_name:tag：将本地文件xxx.tar导入成镜像，并将镜像命名为image_name:tag
docker export/import与docker save/load的区别：
export/import会丢弃历史记录和元数据信息，仅保存容器当时的快照状态
save/load会保存完整记录，体积更大
docker top CONTAINER：查看某个容器内的所有进程
docker stats：查看所有容器的统计信息，包括CPU、内存、存储、网络等信息
docker cp xxx CONTAINER:xxx 或 docker cp CONTAINER:xxx xxx：在本地和容器间复制文件
docker rename CONTAINER1 CONTAINER2：重命名容器
docker update CONTAINER --memory 500MB：修改容器限制
实战

进入AC Terminal，然后：

scp /var/lib/acwing/docker/images/docker_lesson_1_0.tar server_name:  # 将镜像上传到自己租的云端服务器
ssh server_name  # 登录自己的云端服务器

docker load -i docker_lesson_1_0.tar  # 将镜像加载到本地
docker run -p 20000:22 --name my_docker_server -itd docker_lesson:1.0  # 创建并运行docker_lesson:1.0镜像

docker attach my_docker_server  # 进入创建的docker容器
passwd  # 设置root密码
去云平台控制台中修改安全组配置，放行端口20000。

返回AC Terminal，即可通过ssh登录自己的docker容器：

ssh root@xxx.xxx.xxx.xxx -p 20000  # 将xxx.xxx.xxx.xxx替换成自己租的服务器的IP地址
然后，可以仿照上节课内容，创建工作账户acs。

最后，可以参考4. ssh——ssh登录配置docker容器的别名和免密登录。

小Tips

如果apt-get下载软件速度较慢，可以参考清华大学开源软件镜像站中的内容，修改软件源。

作者：yxc
链接：https://www.acwing.com/blog/content/10878/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。