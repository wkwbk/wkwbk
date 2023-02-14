# Debian 修改国内镜像源

## 先备份一下原始的源

```bash
mv /etc/apt/sources.list /etc/apt/sources.list.bak
```

## 更新为国内的源

一般情况下，将 /etc/apt/sources.list 文件中 Debian 默认的源地址 http://deb.debian.org/ 替换为 http://mirrors.ustc.edu.cn 即可

可以使用如下命令：

```bash
sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
```

当然也可以直接编辑 /etc/apt/sources.list 文件

```bash
vi /etc/apt/sources.list
```

把下面的源地址复制进去 sources.list 文件

```text
deb http://mirrors.ustc.edu.cn/debian/ buster main
deb-src http://mirrors.ustc.edu.cn/debian/ buster main

deb http://security.debian.org/debian-security buster/updates main
deb-src http://security.debian.org/debian-security buster/updates main

# buster-updates, previously known as 'volatile'
deb http://mirrors.ustc.edu.cn/debian/ buster-updates main
deb-src http://mirrors.ustc.edu.cn/debian/ buster-updates main

deb http://mirrors.ustc.edu.cn/debian/ buster-backports main non-free contrib
deb-src http://mirrors.ustc.edu.cn/debian/ buster-backports main non-free contrib
```

更改完 sources.list 文件后运行下面命令更新索引以生效

```bash
apt update
```
