# Ubuntu本地安装Docker

> 官方文档：[Install Docker Engine on Ubuntu | Docker Docs](https://docs.docker.com/engine/install/ubuntu/#install-from-a-package)

- [Ubuntu18.04 Docker安装包](https://github.com/gy8801/DockerPackage---1804)
- [Ubuntu20.04 Docker安装包](https://github.com/gy8801/DockerPackage---2004)

## 查看Ubuntu系统版本代号

**常见版本代号**

| 版本  | 代号 Codename |
| ----- | ------------- |
| 18.04 | bionic        |
| 20.04 | focal         |
| 22.04 | jammy         |
| 24.04 | noble         |

**手动查看**

```sh
lsb_release -a
# 或
lsb_release -c
```

`Codename`为版本代号，24.04此处为`noble`

![img1](assets\1.png)



## 安装

1. **将对应版本代号下的包上传至服务器的某个文件夹**

<img src="assets\2.png" alt="" />

2. **服务器进入该文件夹执行命令**

   安装顺序可以为：containerd、docker-ce-cli、docker-buildx-plugin、docker-ce、docker-compose-plugin，遇到安装失败的情况可以改变下安装顺序

   ```bash
   # 注意：xxx.deb指的是包文件，请自行指定本地包文件名，逐个进行安装
   sudo dpkg -i xxx.deb
   ```

3. **启动**

   ```bash
   sudo service docker start
   # 设置自启动
   sudo systemctl enable docker
   ```

   

## 修改镜像源

Docker镜像源配置文件在`/etc/docker/daemon.json`

```bash
sudo vim  /etc/docker/daemon.json
```

编辑json文件，将镜像源地址写进json数组中，请将`https://yourhub.com`替换为真实的镜像源地址

```json
{
    "registry-mirrors": [
        "https://yourhub.com"
    ]
}
```

重启生效

```bash
#重启daemon进程
sudo systemctl daemon-reload
#重启docker
sudo systemctl restart docker
```



国内第三方镜像源几乎失效，可自行配置代理官方镜像地址

一些解决方法：

[cmliu/CF-Workers-docker.io: 这个项目是一个基于 Cloudflare Workers 的 Docker 镜像代理工具。它能够中转对 Docker 官方镜像仓库的请求，解决一些访问限制和加速访问的问题。 (github.com)](https://github.com/cmliu/CF-Workers-docker.io)

[24年6月国内Docker镜像源失效解决办法--小白也可以自给自足（镜像仓库搭建）含可用Docker镜像源 - 掘金 (juejin.cn)](https://juejin.cn/post/7385374199914938406)

