# docker实验环境配置
---
---
## 1 docker 

### docker pull

docker hub 可能会出现404，退出登录当前账号可解决。

* 通过查看images的哈希值，查找镜像版本


    docker images --digests
    docker rmi ID # 删除镜像

### docker run

docker image: pytorch latest

    docker images
    docker run -dit --gpus all --name container_name --shm-size 5G -p 7022:22 -v /mnt/nvme/dataset:/dataset dockerimageID /bin/bash

创建docker的时候默认shm大小为64M，不够用！

”--shm-size 5g“ 共享内存坑

-d 后台运行容器 返回容器ID 
-it 分配伪终端，交互模式


### docker stop/rm
    docker ps -a
    docker stop container_ID
    docker rm container_ID

docker 退出后重启

    docker container start 2fcfa4078e7c


### 进入容器
    docker exec -it container_name bash
    nvidia-smi # 查看GPU

3090 GPU 查看torch版本

    import torch
    torch.cuda.is_available() # 查看是否为GPU版本torch
    print(torch.__version__)
    
    ---- 1.8.1+cu102
    
    torch.zeros(1).cuda()
        
    ---- Out[5]: tensor([0.], device='cuda:0')

## 2 配置 ssh
进入容器后。

    apt-get update
    apt-get upgrade
    apt-get install vim
    apt-get install openssh-server

设置密码

    passwd

    vim /etc/ssh/sshd_config

修改 

    #PermitRootLogin prohibit-password
    PermitRootLogin yes

    /etc/init.d/ssh restart
    * Restarting OpenBSD Secure Shell server sshd

* docker 重启容器时，需要重启ssh服务。

root远程连接

    ssh root@172.28.6.71 -p 7888:22

## 3 环境变量
* 通过ssh连接后，无法使用conda pip等命令，原因是ssh连接没有配置环境变量。
docker exec 进入容器

    env > path.txt

ssh 连接到远程服务器，path 复制到 /etc/profile 后面

    source /etc/profile



## 4 ping github

    apt-get install inetutils-ping

    vim /etc/hosts

加入一行 140.82.114.3 github.com

## 5 建立软连接

    ln -s /opt/conda/bin/python3.7 /usr/bin/python

## 6 docker 打包

使用 docker commit containerID REPOSITORY:TAG

    docker commit 8819fa22d013 pytorch/s1.0

完成后会出现sha256 哈希值，使用 docker images 可以看到





使用 docker save -o IMAGE [IMAGE...]

    docker save -o my_pytroch_s.tar pytorch/s1.0

将打包好的压缩包传到目标服务器上 使用docker load

    docker load --input my_pytroch_s.tar

完成后可以docker image 看到。

---









    


