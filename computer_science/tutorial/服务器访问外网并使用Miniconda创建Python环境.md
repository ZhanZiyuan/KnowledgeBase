# 服务器访问外网并使用Miniconda创建Python环境

> First created by *Ziyuan Zhan* on October 4th, 2022. Last updated on September 18th, 2023.

## 路由器代理

1. 首先，确认路由器中 VPN-V2ray 服务器-启用√  

    代理地址：<http://group:group_account@proxy_IP>

## 安装[Miniconda](https://docs.conda.io/en/latest/miniconda.html)

1. 有两种方式：

    1.1. 在[Miniconda](https://docs.conda.io/en/latest/miniconda.html)官网下载sh脚本
    >来自 [简书](https://www.jianshu.com/p/47ed480daccc)

    1.2. 使用Wget下载
    >来自 [简书](https://www.jianshu.com/p/4d4c786ed454)

    ```bash
    wget -c https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
    ```

2. 授予权限并安装

    ```bash
    chmod 777 Miniconda2-latest-Linux-x86_64.sh
    sh Miniconda2-latest-Linux-x86_64.sh
    ```

## 在conda中使用http代理

1. 使用vi编辑`.condarc`

    ```bash
    vi ~/.condarc
    ```

2. 在个人目录下的`.condarc`文件中添加以下内容：

    ```text
    proxy_servers:
     http: http://group:group_account@proxy_IP
     https: http://group:group_account@proxy_IP
    ```

这样就可以使用conda install从外网中获得各种库并安装了。

## conda channel换源

>来自 [简书](https://www.jianshu.com/p/eba58694537b)
和 [GitBook](https://ocxs.gitbooks.io/python/content/manage/170516_conda_channels.html)

例如清华大学镜像：
>来自 [简书](https://www.jianshu.com/p/e39cb192bde0)

```bash
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
```

## 使用Miniconda创建虚拟Python环境

>来自 [博客园](https://www.cnblogs.com/xiaojianliu/p/13466666.html)

1. 创建虚拟Python环境，在终端中输入：
   >来自 [CSDN](https://blog.csdn.net/weixin_46307478/article/details/119946049)

    ```bash
    conda create -n py310 python=3.10
    ```

2. 删除虚拟Python环境：

    ```bash
    conda remove -n your_env_name --all
    conda remove --name your_env_name --all
    ```

3. 激活虚拟Python环境：

    ```bash
    conda activate env_name
    ```

4. 退出虚拟Python环境：

    ```bash
    conda deactivate
    ```

5. 查看所有的虚拟Python环境：

    ```bash
    conda env list
    # 或者使用：
    conda info -e
    ```

6. 去除终端命令行前出现的`base`
    >来自 [终端命令行前出现(base)怎么办？](https://blog.csdn.net/qq_41523462/article/details/117857194)
    和 [安装conda后取消命令行前出现的base，取消每次启动自动激活conda的基础环境](https://blog.csdn.net/u014734886/article/details/90718719)

    在终端中使用以下命令进行检查：

    ```bash
    conda config --show | grep auto_activate_base
    ```

    若为True，可以通过以下命令将其设置为False：

    ```bash
    conda config --set auto_activate_base False
    ```

7. 激活公用的Anaconda3环境
    >参考 [Anaconda利用方法](http://www.hpc.cmc.osaka-u.ac.jp/system/manual/squid-use/anaconda/) 和 [conda activate 和 source activate 的区别](https://stackoverflow.com/questions/49600611/python-anaconda-should-i-use-conda-activate-or-source-activate-in-linux)

    ```bash
    source conda_env
    conda activate base
    ```

8. 升级Anaconda版本/升级Anaconda中的Python版本
    >参考 [anaconda 升级 python](https://www.jianshu.com/p/092c3585e6a8)
    和 [不重装anaconda升级base中的Python版本](https://www.cnblogs.com/ruhai/p/12684838.html)

    ```bash
    # 先更新conda
    conda upgrade conda
    # 如果上一步更新失败，执行这个命令即可
    conda update --force conda
    # 第二步更新anaconda
    conda update anaconda
    # 第三步，安装python，这个命令默认升级到最新版本
    conda install python
    # 如需指定版本，使用：
    conda install python=3.11
    ```

9. 一个简短的Anaconda教程
    >参考 [Anaconda-用conda创建python虚拟环境](https://zhuanlan.zhihu.com/p/94744929)
    和 [Miniconda 安装及使用](https://juejin.cn/post/7078965942968909854)

## 设置环境变量使用代理

1. 直接在终端输入：

    ```bash
    export ALL_PROXY=http://group:group_account@proxy_IP
    ```

## [A Faster Solver for Conda: Libmamba](https://www.anaconda.com/blog/a-faster-conda-for-a-growing-community)

1. To use the new solver, update conda in your base environment:

    ```bash
    conda update -n base conda
    ```

2. To install and set the new solver, run the following commands:

    ```bash
    conda install -n base conda-libmamba-solver
    conda config --set solver libmamba
    ```
