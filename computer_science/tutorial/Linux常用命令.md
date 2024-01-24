# Linux常用命令

> First created by *Ziyuan Zhan* on October 4th, 2022. Last updated on September 16th, 2023.
>> 基于Linux发行版CentOS

1. 查看所有任务队列
    >来自 [Slurm作业管理系统](https://www.bkunyun.com/helpce/docs/2032/about/)

    ```bash
    squeue
    ```

2. 查看指定用户的任务队列

    ```bash
    squeue -u zhanziyuan
    ```

3. 查看所有任务详细信息

    ```bash
    scontrol show jobs
    ```

4. 查看指定任务ID的任务

    ```bash
    scontrol show job jobID
    ```

5. 取消指定任务ID的任务

    ```bash
    scancel jobID
    ```

6. LAMMPS任务提交

    ```bash
    qlammps -n 4 -q node2 test.in
    ```

7. Gaussian任务提交

    ```bash
    qg16 -n 4 -q node9 BTA_1a2_30.gjf
    ```

8. 查看当前所在目录

    ```bash
    pwd
    ```

9. 查看所有节点占用情况

    ```bash
    pestat
    ```

10. 查看所有任务排队和运行情况

    ```bash
    qstat
    ```

11. 将当前目录下所有文件移动到上级目录  
    >来自 [CSDN](https://blog.csdn.net/BADAO_LIUMANG_QIZHI/article/details/98022010)

    ```bash
    mv * ../
    ```

12. 移动文件夹及文件夹下所有文件  
    >来自 [博客园](https://www.cnblogs.com/lansetiankongblog/p/7851489.html)

    将`/usr/lib/`下所有的东西移到`/zone/`中

    ```bash
    mv /usr/lib/* /zone
    ```

    将`lib`下以`.txt`结尾的所有文件移到`/zone`中。其他类型，以此类推。

    ```bash
    mv /usr/lib/*.txt /zone
    ```

13. Linux下解压文件和压缩文件
    >来自 [CSDN](https://blog.csdn.net/laobai1015/article/details/89405905)，
    [码农教程](http://www.manongjc.com/article/42355.html)，
    [Linux tar命令参数详细说明](https://blog.csdn.net/u013053075/article/details/103117341)
    和 [Linux unzip命令：解压zip文件](http://c.biancheng.net/view/782.html)

    将文件`test_archive_01.tar.gz`解压到目录`blue_archive`

    ```bash
    tar -xzvf test_archive_01.tar.gz -C blue_archive
    ```

    命令的解释：
    - `-x`：从存档中提取文件。
    - `-z`：使用gzip算法解压缩。
    - `-v`：表示详细模式，显示提取的文件列表。
    - `-f`：指定存档的文件名或者目录名。
    - `-J`：使用xz算法解压缩。

    将文件`test_archive_02.tar.xz`解压到目录`blue_archive`

    ```bash
    # -z：默认使用gzip算法解压缩
    tar -xvf test_archive_02.tar.xz -C blue_archive

    # -J：使用xz算法解压缩
    tar -xJvf test_archive_02.tar.xz -C blue_archive
    ```

    将文件`test_archive_03.zip`解压到目录`blue_archive`

    ```bash
    unzip test_archive_03.zip -d blue_archive
    ```

    将目录`blue_archive`压缩为文件`red_archive.tar.gz`

    ```bash
    tar -czvf red_archive.tar.gz blue_archive
    ```

    命令的解释：
    - `-c`：创建新的存档文件。
    - `-z`：使用gzip算法压缩。
    - `-v`：表示详细模式，显示压缩的文件列表。
    - `-f`：指定存档的文件名或者目录名。

    将目录`blue_archive`压缩为文件`orange_archive.tar.xz`

    ```bash
    tar -cJvf orange_archive.tar.xz blue_archive
    ```

    命令的解释：
    - `-c`：创建新的存档文件。
    - `-J`：使用xz算法压缩。
    - `-v`：表示详细模式，显示压缩的文件列表。
    - `-f`：指定存档的文件名或者目录名。

    将目录`blue_archive`压缩为文件`green_archive.zip`

    ```bash
    zip -r green_archive.zip blue_archive
    ```

    命令的解释：
    - `-r`：递归地压缩该目录及其下的所有文件。

14. 使用vi编辑`.bashrc`

    ```bash
    vi ~/.bashrc
    ```

15. 运行Moltemplate

    ```bash
    moltemplate.sh system.lt
    ```

16. 运行Moltemplate，指定参数

    ```bash
    moltemplate.sh -atomstyle "full" system.lt
    # 指定atom style为"full"，运行Moltemplate生成体系
    ```

17. 运行Moltemplate时调用外部文件（支持`.PDB`、`.XYZ`等格式的文件）

    ```bash
    moltemplate.sh -pdb coords.pdb -atomstyle "full" system.lt
    # 调用外部文件（“coords.pdb”）来提供原子坐标和周期性边界条件；使用原子style为full（默认为“full”）
    # 注意：PDB文件中的原子顺序必须与原子在LT文件中出现的顺序一致
    ```

18. 复制文件
    >来自 [C语言中文网](http://c.biancheng.net/view/746.html)

    ```bash
    # cp [选项] 源文件 目标文件
    ```

    ```bash
    # (1) 不改名复制

    cp cangls /tmp/
    # 把源文件不改名复制到 /tmp/ 目录下

    # (2) 改名复制

    cp cangls /tmp/bols
    # 把源文件复制到 /tmp/ 目录下，并且改名为bols

    # (3) 使用“cp -i”，如果复制的目标位置已经存在同名的文件，则会提示是否覆盖

    cp -i /home/user/test/system.lt /home/user/modelling
    cp: overwrite ‘/home/user/modelling/system.lt’? y
    # 目标位置有同名文件，所以会提示是否覆盖。确认覆盖输入“y”，取消覆盖输入“n”。
    ```

19. 复制目录
    >来自 [C语言中文网](http://c.biancheng.net/view/746.html)

    ```bash
    mkdir test
    # 创建测试目录

    cp -r /home/user/test/ /tmp/
    # 目录原名复制
    ```

20. 复制指定目录下所有文件
    >来自 [CSDN](https://blog.csdn.net/anle01532/article/details/101989951)

    ```bash
    # 指定目录下的隐藏文件不会被复制，子目录下的隐藏文件会被复制
    cp -r /home/user/test/ben_alk/* /home/user/modelling

    # 指定目录下和子目录下的隐藏文件都会被复制
    cp -r /home/user/test/ben_alk/. /home/user/modelling
    ```

21. 重命名文件/目录
    >来自 [在 Linux 中重命名文件](https://cloud.tencent.com/developer/article/1876435)，
    [linux 之重命名文件和文件夹](https://zhuanlan.zhihu.com/p/353664138)
    和 [Linux下批量修改文件名](https://www.jianshu.com/p/bdd27936416e)

    ```bash
    # 重命名文件
    mv example01.txt example02.txt

    # 重命名目录
    mv notebook notebooks
    ```

22. 查找文件
    >来自 [Linux which命令](https://www.runoob.com/linux/linux-comm-which.html)

    ```bash
    which bash
    ```

23. Linux命令自动补全
    >来自 [Linux命令自动补全工具，自动补全git、Docker、k8s等命令](https://cloud.tencent.com/developer/news/598652)

24. `chmod`（change mode）命令
    >来自 [linux终端文件名颜色问题（文件夹具有可执行文件颜色之类的问题）](https://blog.csdn.net/qq_29343201/article/details/51880760)，
    [Linux系统文件名字体不同的颜色都代表什么](https://blog.csdn.net/jaray/article/details/103467268)，
    [linux下chmod +x的意思？为什么要进行chmod +x](https://blog.csdn.net/u012106306/article/details/80436911)，
    [在linux终端(terminal)中执行python文件](https://blog.csdn.net/qq_28267025/article/details/60337293)
    和 [Linux chmod命令](https://m.runoob.com/linux/linux-comm-chmod.html)

    ```bash
    # +x：设置为可执行权限
    chmod +x helloworld.py
    ```

    ```bash
    # 777：设置文件的权限为读取、写入和执行，无论文件原本有什么权限
    chmod 777 helloworld.py
    ```

25. bash-completion - `exec` 命令
    >来自 [Linux 系统中的 Bash 自动补全功能简介](https://kubernetes.io/zh-cn/docs/tasks/tools/included/optional-kubectl-configs-bash-linux/)，
    [What does an "exec" command do?](https://askubuntu.com/questions/525767/what-does-an-exec-command-do)
    和 [exec Man Page - Linux - SS64.com](https://ss64.com/bash/exec.html)

    ```bash
    exec bash
    ```

26. Linux清屏命令
    >来自 [关于在linux下清屏的几种技巧](https://www.cnblogs.com/5201351/p/4208277.html)

    ```bash
    clear
    # 这个命令将会刷新屏幕，本质上只是让终端显示页向后翻了一页，如果向上滚动屏幕还可以看到之前的操作信息。
    ctrl + l（小写的L）
    # 这是一个清屏的快捷键，这个是笔者在工作中用得最多的一种清屏方式，清屏效果同clear命令一样。
    reset
    # 这个命令将完全刷新终端屏幕，之前的终端输入操作信息将都会被清空，这样虽然比较清爽，但整个命令过程速度有点慢，使用较少。
    printf "\033c"
    # 这个命令它才是真正的清空了终端屏幕，它的功能跟DOS里CMD.EXE提供的CLS效果很相似。
    ```

27. Linux终端中文本的颜色
    >来自 [linux终端文件名颜色问题（文件夹具有可执行文件颜色之类的问题）](https://blog.csdn.net/qq_29343201/article/details/51880760)
    和 [Linux系统文件名字体不同的颜色都代表什么](https://blog.csdn.net/jaray/article/details/103467268)

    Linux中文件名颜色不同，代表文件类型不一样。  
    - 浅蓝色：表示软链接；
    - 灰色：表示其他文件；
    - 绿色：表示可执行文件；
    - 红色：表示压缩文件；
    - 蓝色：表示目录；
    - 红色闪烁：表示链接的文件有问题了；
    - 黄色：表示设备文件，包括block，char，fifo，管道文件。
    - 粉色：网络文件；  
    用 `dircolors -p` 命令可以看到缺省的颜色设置，
    包括各种颜色和粗体、下划线、闪烁等。

28. Linux终端中Ctrl + C和Ctrl + Z的区别
    >来自 [Linux中Ctrl+C,Ctrl+Z,Ctrl+D说明](https://developer.aliyun.com/article/632369)

    Ctrl+C：送SIGINT信号，默认进程会结束，但是进程自己可以重定义收到这个信号的行为。  
    Ctrl+Z：送SIGSTOP信号，进程只是被停止，再送SIGCONT信号，进程继续运行。  
    Ctrl+D：不是发送信号，而是表示一个特殊的二进制值，表示 EOF。  

    Ctrl+C和Ctrl+Z都是中断命令，但是它们的作用却不一样。  
    Ctrl+C是强制中断程序的执行；  
    Ctrl+Z的作用是将任务中断，但是此任务并没有结束，
    它仍然以进程形式存在于系统中，它只是维持挂起的状态。  

29. ls命令
    >来自 [Linux ls命令](https://deepinout.com/linux-cmd/linux-folder-file-cmd/linux-cmd-ls.html)，
    [linux查看文件大小的各种操作命令](https://www.baiyangz1.com/194.html)，
    和 [Linux查看文件大小5个常用命令](https://www.cnblogs.com/gucb/p/11280443.html)

    ```bash
    # 以长格式来显示文件的详细信息
    ls -l
    # 在大部分的Linux系统中，都已经设置了ls -l的别名为ll
    ls -ll
    # 文件或目录大小大于1024字节时，以KB、MB或GB来表示文件大小和目录大小
    ls -lh
    ```

30. 删除Bash命令的历史记录
    >来自 [清除Bash命令的历史记录· Linux Command](https://ficapy1.gitbooks.io/linux-command/content/ru-he-qing-chu-bash-ming-ling-de-li-shi-ji-lu.html)，
    [linux删除历史操作命令](https://www.cnblogs.com/yunwangjun-python-520/p/10812392.html)，
    和 [Linux history命令](https://www.coonote.com/linux/linux-cmd-history.html)

    ```bash
    << BLOCK
        删除单行历史记录
        比如删除66行
    BLOCK
    history -d 66

    # 清除所有历史记录
    history -c
    # 将历史命令文件中的命令读入当前历史命令缓冲区
    history -r
    ```

31. Bash单行和多行注释
    >来自 [shell 多行注释详解](https://blog.csdn.net/qianggezhishen/article/details/51981804)
    和 [Bash注释](https://www.yiibai.com/bash/bash-comments.html)

    ```bash
    # 多行注释-方法一

    #!/bin/bash
    <<BLOCK 
        This is the first comment  
        This is the second comment  
        This is the third comment  
    BLOCK

    echo "Hello World"

    # 多行注释-方法二

    #!/bin/bash  
    : '  
    This is the first comment  
    This is the second comment  
    This is the third comment  
    '  

    echo "Hello World"
    ```

32. 将Linux终端输出保存到文件中
    >来自 [如何将 Linux 终端中命令的输出保存到文件中](https://linux.cn/article-12920-1.html)

    ```bash
    # ">" 会将命令输出重定向到文件，它会替换文件中的所有内容。
    # 使用标准输出重定向运算符 > 将输出重定向到文件：
    command > file.txt
    # ">>" 会将命令输出添加到文件现有内容的末尾。
    # 如果你不想在保存脚本或命令的输出时丢失现有文件的内容，可以使用 ">>" ：
    command >> file.txt
    ```

33. 创建目录
    >来自 [Linux mkdir 命令创建目录](https://www.myfreax.com/how-to-create-directories-in-linux-with-the-mkdir-command/)
    和 [Linux mkdir命令：创建目录（文件夹）](http://c.biancheng.net/view/723.html)

    ```bash
    # 仅提供目录名称而没有完整路径时，mkdir命令将会在当前工作目录创建目录。
    # 要在其他文件夹创建目录，需要提供绝对路径或相对路径。
    mkdir demo
    ```

34. 创建文件
    >来自 [如何在Linux中创建文件？多个文件创建操作命令。](https://cloud.tencent.com/developer/article/1858594)
    和 [Linux 创建文件](https://www.myfreax.com/create-a-file-in-linux/)

    ```bash
    # 此处只展示了一种较为简单的方式。
    # 如果touch命令参数指定的文件不存在，touch命令将会创建文件；
    # 否则，它将修改已存在的文件的时间戳。
    touch file1.txt
    # 使用touch命令创建多个文件
    touch file1.txt file2.txt file3.txt
    ```

35. 查找文件和目录
    >来自 [Linux find 命令](https://www.runoob.com/linux/linux-comm-find.html)

    ```bash
    # 在当前目录下查找名为file.txt的文件
    find . -name file.txt
    # 列出在当前目录及其子目录下所有扩展名为.c的文件
    find . -name "*.c"
    # 在/home目录下查找大于1MB的文件
    find /home -size +1M
    ```

36. 结束进程
    >来自 [Linux kill命令](https://www.runoob.com/linux/linux-comm-kill.html)

    ```bash
    # kill -9代表的信号是SIGKILL，表示进程被终止，需要立即退出，
    # 强制杀死该进程，这个信号不能被捕获也不能被忽略。
    kill -9 14231
    ```

37. 查找文件里符合条件的字符串或正则表达式
    >来自 [使用VSCode 时间线/本地文件历史功能防止误删文件](https://tutorials.tinkink.net/zh-hans/vscode/timeline-local-history-usage.html)

    ```bash
    # Linux / Mac
    grep -r set_initial_guess "/home/zhanziyuan/python_assignments/"
    ```

    ```cmd
    :: Windows
    findstr /s /i set_initial_guess "C:\Users\user\Downloads"
    ```

38. 一个简短的Bash shell教程
    >来自 [Shell编程基础](https://fanling521.github.io/mybolg/?file=03-Linux%E7%B3%BB%E7%BB%9F/02-Shell%E7%BC%96%E7%A8%8B/001-Shell%E7%BC%96%E7%A8%8B%E5%9F%BA%E7%A1%80)
    和 [一篇教会你写90%的shell脚本](https://zhuanlan.zhihu.com/p/264346586)

39. SSH免密登录
    >来自 [Windows Terminal：SSH连接远程服务器](https://zhuanlan.zhihu.com/p/445909756)，
    [VS Code配置SSH免密远程登录](https://www.cnblogs.com/safe-rabbit/p/16254860.html)，
    和 [三步完成VS Code配置SSH免密登录远程开发](https://juejin.cn/post/7023042621295558692)

40. top命令
    >来自 [Linux top 命令](https://www.runoob.com/linux/linux-comm-top.html)

    ```bash
    # 查看指定用户的所有进程
    top -u username
    ```

41. 输出重定向与命令后台运行
    >来自 [Linux命令-nohup和&--不占用终端运行和后台运行方式](https://blog.csdn.net/tomy2426214836/article/details/106159532/)
    和 [Linux ：输入/输出重定向 >, 1>, 2>, &>, >> , <<](https://gwaslab.org/2021/11/28/linux-redirection/)

    ```bash
    # `nohup`：忽略 SIGHUP 信号，使得命令在终端关闭后继续运行。
    # `>`：将命令的标准输出重定向到指定的文件中。
    # `2>&1`：将标准错误输出（文件描述符为2）重定向到标准输出（文件描述符为1）。
    # `&`：将命令放到后台运行。这样，终端将会立即返回，而不会等待命令执行完成。
    nohup python run_sample.py > redirected_output.log 2>&1 &
    ```

42. 登录到从节点

    ```bash
    # 登录到node 8；可能需要额外权限和身份认证
    ssh node8
    ```

43. 使用`find`命令显示大于指定文件大小的所有文件

    ```bash
    find . -type f -size +100M -exec ls -lh {} \;
    ```

    命令的解释：

    - `find .`: 在当前目录及其子目录中查找文件。
    - `-type f`: 限制查找结果为文件而不是目录。
    - `-size +100M`: 指定查找大于100MB的文件。
    - `-exec ls -lh {} \;`: 对于每个符合条件的文件，
    执行`ls -lh`命令以显示文件的详细信息，包括文件大小。

    这个命令将在终端中列出所有符合条件的文件。
    如果需要将结果保存到文件中，可以使用重定向操作符`>`，例如：

    ```bash
    find . -type f -size +100M -exec ls -lh {} \; > large_files.txt
    ```

    以上命令将会把结果保存到名为`large_files.txt`的文件中。

44. 将`find . -name "*.ipynb"`的结果按照文件大小降序排列

    ```bash
    find . -name "*.ipynb" -exec du -h {} + | sort -rh
    ```

    命令的解释：

    - `find . -name "*.ipynb"`: 查找当前目录及其子目录中所有扩展名为`.ipynb`的文件。
    - `-exec du -h {} +`: 对找到的文件执行`du -h`命令，以人类可读的格式显示文件大小。
    - `|`: 将`du`的输出通过管道传递给下一个命令。
    - `sort -rh`: 对`du`的输出进行反向（从大到小）排序，`-h`表示按人类可读格式排序。

45. 将`find . -name "*.ipynb"`的结果按照文件的时间戳从晚到早排列

    ```bash
    find . -name "*.ipynb" -exec ls -lt --time=atime {} +
    ```

    命令的解释：

    - `find . -name "*.ipynb"`:
    查找当前目录及其子目录中所有扩展名为`.ipynb`的文件。
    - `-exec ls -lt --time=atime {} +`:
    对找到的文件执行`ls -lt --time=atime`命令，按访问时间从晚到早排序。

    这将列出`.ipynb`文件并按文件访问时间从晚到早排序。
    如果想按照修改时间排序，可以使用`--time=mtime`。

46. 使用`grep`命令和`find`命令来搜索包含字符串`"con"`的以`.txt`为扩展名的文件

    ```bash
    find . -type f -name "*.txt" -exec grep -l "con" {} +
    ```

    命令的解释：

    - `find . -type f -name "*.txt"`:
    查找当前目录及其子目录中所有扩展名为`.txt`的文件。
    - `-exec grep -l "con" {} +`:
    对找到的文件执行`grep -l "con"`命令，以列出包含字符串`"con"`的文件的文件名。

47. 终止指定用户的所有进程

    使用`pkill`命令：

    ```bash
    pkill -u yellowdog
    ```

    使用`killall`命令：

    ```bash
    killall -u yellowdog
    ```

    这两个命令都会向属于用户“yellowdog”的所有进程发送终止信号。
    请注意，强行终止进程可能会导致数据丢失或其他不良影响，因此请谨慎操作。

48. 计算指定目录下所有文件的总大小

    ```bash
    du -sh /path/to/your/directory
    ```

    命令的解释：

    - `du`: Disk Usage的缩写，用于显示文件和目录磁盘使用情况统计。
    - `-s`: 仅显示总计大小。
    - `-h`: 以人类可读的格式显示大小（例如，KB、MB、GB）。

49. 查找包含指定内容的指定扩展名的文件

    缩略形式：

    ```bash
    grep -r "Hello Mike" *.log
    ```

    命令的解释：

    - `grep`: 用于在文件中搜索指定模式。
    - `-r`: 递归地在子目录中搜索。
    - `"Hello Mike"`: 待搜索的字符串。
    - `*.log`: 指定搜索的文件类型为以“.log”为扩展名的文件。

    完整形式：

    ```bash
    grep --recursive "Hello Mike" --include=*.log
    ```

    使用`find`和`grep`命令查找包含字符串`"blue_dog"`的扩展名为`".py"`的所有文件：

    ```bash
    find /path/to/search -type f -name "*.py" -exec grep -l "blue_dog" {} +
    ```

    命令的解释：

    - `find /path/to/search`: 在指定路径下执行查找操作。
    - `-type f`: 仅查找文件而非目录。
    - `-name "*.py"`: 指定查找文件的扩展名为".py"。
    - `-exec grep -l "blue_dog" {} +`: 对找到的文件执行`grep`命令，查找包含字符串`"blue_dog"`的文件，并输出文件名。
    `{}`是一个占位符，表示`find`命令找到的每个文件名。`{}`将会被替换为实际的文件名。
    `+`表示将找到的多个文件名一次性传递给`grep`命令，而不是每个文件单独执行一次`grep`。

50. 统计代码行数
    >来自 [推荐一波代码量、行数、提交量、作者等全维度统计神器](https://zhuanlan.zhihu.com/p/259663572)

    ```bash
    find . -name "*.java" -or -name "*.xml" -print | xargs wc -l
    ```

    命令的解释：
    - `find`: 用于在文件系统中搜索文件和目录的命令。
    - `.`: 从当前目录开始搜索。
    - `-name "*.java" -or -name "*.xml"`: 指定了两个条件，分别是查找扩展名为`".java"`和`".xml"`的文件。
    - `-print`: 在找到匹配的文件时，将文件名输出到标准输出。
    - `|`: 管道符，将前一个命令的输出传递给后一个命令。
    - `xargs`: 从标准输入中获取参数，并将其传递给其他命令作为参数。
    - `wc -l`: 统计文件的行数。

    因此，整个命令的作用是找到当前目录及其子目录中所有以`".java"`或`".xml"`为扩展名的文件，
    然后使用`xargs`将它们传递给`wc -l`命令，最终输出这些文件的总行数。
