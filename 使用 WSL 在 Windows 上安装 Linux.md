# 使用 WSL 在 Windows 上安装 Linux

## 先决条件

- 必须运行 Windows 10 版本 2004 及更高版本（内部版本 19041 及更高版本）或 Windows 11
  - 检查 Windows 版本及内部版本号，选择 Windows 徽标键 + R，然后键入“winver”，选择“确定”
- 需要在BIOS中开启虚拟化技术
  - 检查是否启用虚拟化，同时按住 CTRL、Shift 和 ESC 键打开任务管理器，选择“性能”>“CPU”
- 启用 Windows 子系统
  - “控制面板”>“程序和功能”>“启用或关闭 Windows 功能”>勾选“适用于 Linux 的 Windows 子系统”

## WSL 的基本命令

```PowerShell
# 安装 WSL 命令
wsl --install

# 更新 WSL
wsl --update

# 检查正在运行的 WSL 版本
wsl -l -v

# 检查 WSL 状态
wsl --status

# 关闭
wsl --shutdown
```

## 设置WSL的默认版本

```PowerShell
wsl --set-default-version <Version>
# 若要将默认版本设置为 WSL 1 或 WSL 2，将 <Version> 替换为 1 或 2。
# 例如 wsl --set-default-version 2
```

## 设置默认 Linux 发行版

```PowerShell
wsl --set-default <DistributionName>
# 将 <DistributionName> 替换为要使用的 Linux 发行版的名称。
# 例如 wsl --set-default CentOS8
```

## 要设置与 wsl 命令一起使用的默认 Linux 发行版

```PowerShell
wsl --setdefault <DistributionName>
# 将 <DistributionName> 替换为要使用的 Linux 发行版的名称。
```

## 将 WSL 版本设置为 1 或 2

```PowerShell
wsl --set-version <DistributionName> <Version>
# 若要指定运行 Linux 发行版的 WSL 版本
# 将 <DistributionName> 替换为 Linux 发行版的名称，并将 <Version> 替换为 1 或 2。
# 例如 wsl --set-version CentOS8 2 会将 CentOS8 发行版设置为使用 WSL 2
```

## 更改发行版的默认用户

```PowerShell
<DistributionName> config --default-user <Username>
# 更改用于发行版登录的默认用户。 用户必须已经存在于发行版中才能成为默认用户。
# 例如 CentOS8 config --default-user root 会将 CentOS8 发行版的默认用户更改为“root”用户。
```

## 其他命令

```PowerShell
# 关闭子系统
net stop LxssManager

# 终止子系统
wsl --terminate <DistributionName>

# 注销或卸载子系统
wsl --unregister <DistributionName>

# 导出系统镜像
wsl --export <DistributionName> <镜像存放路径>

# 将 <DistributionName> 替换为要使用的 Linux 发行版的名称。
```
