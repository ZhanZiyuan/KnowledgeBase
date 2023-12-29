# [Windows Subsystem for Linux](https://learn.microsoft.com/zh-cn/windows/wsl/install)

> First created by *Ziyuan Zhan* on May 15th, 2023. Last updated on September 16th, 2023.
>> 基于Linux发行版Ubuntu

1. 先更新软件列表源地址，再更新软件
    > 来自 [sudo apt-get update 和 sudo apt-get upgrade 命令的区别](https://blog.csdn.net/u011318077/article/details/105161296)

    ```bash
    sudo apt update && sudo apt upgrade
    ```

2. 添加`wget`和`ca-certificates`
    > 来自 [WSL tips](https://code.visualstudio.com/docs/remote/troubleshooting#_wsl-tips)

    ```bash
    sudo apt-get update && sudo apt-get install wget ca-certificates
    ```
