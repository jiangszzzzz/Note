# 使用git push 失败

# 1 错误1     OpenSSL SSL_read: Connection was reset, errno 10054

貌似是网络波动的原因，过一会就好了。

# 2 错误2     Failed to connect to github.com port 443 after 21057 ms: Timed out

时间 2022.4.10

网上有很多方法都不行。。

无需修改host文件。

直接修改git ，走代理。

不同版本端口号可能不同。

在git bash中运行以下命令。

    git config --global http.proxy http://127.0.0.1:10809 
    git config --global https.proxy http://127.0.0.1:10809

![1asdsdas](.\\imgs\\img.png)