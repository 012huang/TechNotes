# docker 入门


## 基本命令

- 创建一个名叫dev的虚拟机

```
$ docker-machine create -d virtualbox dev
```

```
imaygou@Matrix-MacBook-Pro:~[18:13] $ docker-machine create -d virtualbox dev
Creating CA: /Users/imaygou/.docker/machine/certs/ca.pem
Creating client certificate: /Users/imaygou/.docker/machine/certs/cert.pem
Running pre-create checks...
Creating machine...
(dev) Copying /Users/imaygou/.docker/machine/cache/boot2docker.iso to /Users/imaygou/.docker/machine/machines/dev/boot2docker.iso...
(dev) Creating VirtualBox VM...
(dev) Creating SSH key...
(dev) Starting the VM...
(dev) Check network to re-create if needed...
(dev) Found a new host-only adapter: "vboxnet0"
(dev) Waiting for an IP...
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with boot2docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env dev
```

- 查看所有的 VM

```
$ docker-machine ls
```

- 启动（关闭）一个名叫 default 的虚拟机

```
$ docker-machine start default
$ docker-machine stop default
```

- 查看 dev 环境的信息

```
$ docker-machine env dev
```

- export 虚拟机 dev 的环境变量

```
$ eval "$(docker-machine env dev)"
```

- 运行一个 hello-world 的容器

```
$ docker run hello-world
```

- 运行一个带标签镜像的容器：

```
# -t 标示在新容器内指定一个伪终端或终端，-i 标示允许我们对容器内的 STDIN 进行交互在我们的容器内还指定了一个新的命令：/bin/bash。这将在容器内启
# 动 bash shell，当你完成你的命令的时候，你退出这个容器，你可以输入 exit。一旦你的 Bash shell 退出之后，你的容器就停止了
$ docker run -t -i ubuntu:14.04 /bin/bash
```




