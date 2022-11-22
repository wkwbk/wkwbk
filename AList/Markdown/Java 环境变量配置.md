# Java 环境变量配置

下载安装包，安装JDK到本地电脑中。

我的电脑->右键->属性->左侧菜单->高级系统设置->环境变量

系统变量->新建

```bash
变量名：JAVA_HOM
变量值：C:\Programs\Java\jdk1.8.0_341 #变量值为 JDK 安装路径
```

系统变量->打开 Path 变量->新建

```bash
#添加以下两个变量值
%JAVA_HOME%\bin
%JAVA_HOME%\jre\bin
```

系统变量->新建

```bash
变量名：CLASSPATH
变量值：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar; #不要漏了开头那一点
```
