# pip 使用国内镜像源

默认情况下 pip 使用的是国外的镜像，在下载的时候速度非常慢，本文我们介绍使用国内清华大学的源，地址为：

```bash
https://pypi.tuna.tsinghua.edu.cn/simple
```

我们可以直接在 pip 命令中使用 -i 参数来指定镜像地址，例如：

```bash
pip3 install numpy -i https://pypi.tuna.tsinghua.edu.cn/simple
```

以上命令使用清华镜像源安装 numpy 包。  
这种只对当前安装命令有用，如果需要全局修改，则需要修改配置文件。  

## Linux/Mac os 配置方法

Linux/Mac os 环境中，配置文件位置在 ~/.pip/pip.conf（如果不存在创建该目录和文件）：

```bash
mkdir ~/.pip
```

打开配置文件 ~/.pip/pip.conf，修改如下：

```bash
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host = https://pypi.tuna.tsinghua.edu.cn
```

查看镜像地址：

```bash
$ pip3 config list   
global.index-url='https://pypi.tuna.tsinghua.edu.cn/simple'
install.trusted-host='https://pypi.tuna.tsinghua.edu.cn'
```

可以看到已经成功修改了镜像。

## Windows 配置方法

Windows下，你需要在当前对用户目录下（C:\Users\xx\pip，xx 表示当前使用对用户，比如张三）创建一个 pip.ini 在 pip.ini 文件中输入以下内容：

```bash
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host = pypi.tuna.tsinghua.edu.cn
```

## 其他国内镜像源

中国科学技术大学：<https://pypi.mirrors.ustc.edu.cn/simple>  
豆瓣：<http://pypi.douban.com/simple/>  
阿里云：<http://mirrors.aliyun.com/pypi/simple/>  
