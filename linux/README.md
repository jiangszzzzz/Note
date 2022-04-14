# 常用linux命令

#### 查看当前文件夹中文件个数。

    ls|wc - l

### 产看当前文件夹下所有子文件中文件个数。

    for dir in `ls`; do ls $dir |wc -l; done

### 远程传输 scp -r 跨机传输,很快。。。
    
    ##   scp -p source target

    ## 服务器之间传输文件

    scp -r -p 443 /home/dataset/ jack@172.12.13.12:/home/tmp/

    ##   win下 拉服务器上 Linux的文件 
    
    ### **注意下面这条命令是在 cmd 中运行的 ha ha ha，要不会报 ‘no such file’ **  

    scp -P 443 /home/dataset/hello.txt C:/Users/1/Desktop/
    
    ## 然后输密码 有的服务器会修改默认的 22 端口
    

### mv 移动，修改名称. 将/a目录移动到/b下，并重命名为c

    #  改名
    mv A B

    # 移动加改名 
    mv /a /b/c 

### 查看硬件信息  显卡型号查询<http://pci-ids.ucw.cz/mods/PC/10de?action=help?help=pci>
   
    # 硬盘
    df -h 

    # 内存
    cat /proc/meminfo
    free -h 

    # CPU    
    lscpu 

    # GPU
    lspci | grep NVIDIA 
    nvidia-smi










