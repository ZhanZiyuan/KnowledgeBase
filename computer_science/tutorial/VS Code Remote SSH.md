# Visual Studio Code使用SSH远程连接服务器

> First created by *Ziyuan Zhan* on September 29th, 2022. Last updated on November 1st, 2023.

## 本地SSH设置

1. 首先在VS Code中下载 Remote - SSH 和 Remote - SSH: Editing Configuration Files 两个插件。
2. 修改VS Code的SSH配置文件。下面是例子：

    ```yaml
    Host group_name
      HostName your_IP
      User your_user_name 
      Port port_number(e.g., 22) 
      ServerAliveInterval 40
    ```

现在完成了本地VS Code的SSH设置，接下来需要为服务器安装VS Code Server。

## 在服务器上安装VS Code Server——在Wget中使用http代理

1. 使用vi编辑Wget设置。在终端中输入：

    ```bash
    vi ~/.wgetrc 
    ```

2. 在个人目录下的`.wgetrc`文件中写入以下内容：

    ```bash
    https_proxy = http://group:group_account@proxy_IP
    http_proxy = http://group:group_account@proxy_IP
    ftp_proxy = http://group:group_account@proxy_IP

    use_proxy = on
    ```

对于vi操作的说明：
> 来自[html中文网](https://www.html.cn/script/42723.html)

|      操作       |                      输入内容                       |
| :-------------: | :-------------------------------------------------: |
|      删除       |                       输入dd                        |
|      换行       |            先按esc，再输入i，再按下enter            |
|   保存并退出    |      先按esc，再输入:，再输入wq，最后按下enter      |
| vi的3种工作模式 | [C语言中文网](http://c.biancheng.net/view/519.html) |
| vi的保存和退出  |  [php中文网](https://www.php.cn/linux-434450.html)  |

然后在VS Code中输入用户密码，连接服务器。等待下载VS Code Server，安装后即可在VS Code中使用SSH远程开发。

## [适用于 Windows 的 OpenSSH 入门](https://learn.microsoft.com/zh-cn/windows-server/administration/openssh/openssh_install_firstuse?tabs=gui)

如果配置的是默认端口（22），在Windows Terminal中输入（请替换`username`和`hostIP`）：

```bash
# `-o`：指定SSH客户端的配置选项。
# `ServerAliveInterval=60`：设置心跳间隔的时间为60秒，以保持连接的活跃状态。
ssh -o ServerAliveInterval=60 username@hostIP
```

即可使用Windows自带的OpenSSH远程访问服务器。

## Windows Terminal SSH 保持长时间连接  

> 来自[CSDN](https://blog.csdn.net/humanbeng/article/details/120062468)

我的JSON配置示例：  

```json
            {
                "backgroundImage": "D:\\xxxxxx\\xxxxxx\\xxxxxx\\xxxxxx\\Gradient Outline.jpg",
                "backgroundImageOpacity": 0.5,
                "commandline": "ssh -o ServerAliveInterval=60 username@hostIP",
                "guid": "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}",
                "hidden": false,
                "icon": "D:\\xxxxxx\\xxxxxx\\xxxxxx\\xxxxxx\\centos_logo_96px.png",
                "name": "group_name",
                "opacity": 50,
                "useAcrylic": true
            },
```

## 离线安装Visual Studio Code Server及插件

> 参考 [winscp如何查看隐藏文件](https://blog.csdn.net/weixin_41990913/article/details/105520245)，
  [vscode更新后连接不上服务器](https://codeantenna.com/a/CsNWf3aDEY)，
  ["command '_workbench.downloadResource' failed" when connecting to a remote host via ssh #4743](https://github.com/microsoft/vscode-remote-release/issues/4743)，
  [VS Code Server的离线安装过程](https://zhuanlan.zhihu.com/p/294933020)

~~注意：请谨慎更新Visual Studio Code，
因为更新本地端的Visual Studio Code之后，
将会自动同步更新服务器端的Visual Studio Code Server，两者的版本号必须相同。
但是Visual Studio Code Server的更新往往会因为网络或者代理问题出现错误。~~
（此问题已在版本`1.80.0`之后解决：
Visual Studio Code将会先更新本地程序，
再通过SSH上传Visual Studio Code Server的更新到服务器端。）

1. 查看Visual Studio Code的版本号和Commit ID。

    在PowerShell或者Command Prompt中输入以下命令：

    ```bash
    code -v
    ```

    即可查看本地Visual Studio Code的版本号和Commit ID。
    或者在Visual Studio Code的 帮助 - 关于 中也可以查看版本号和Commit ID。

2. The direct download link of Visual Studio Code Server (sample)

    ```bash
    https://vscode.cdn.azure.cn/stable/2d23c42a936db1c7b3b06f918cde29561cc47cd6/vscode-server-linux-x64.tar.gz

    https://update.code.visualstudio.com/commit:${commit_id}/server-linux-x64/stable（注意把:${commit_id}替换成对应的Commit ID）
    ```

3. （不推荐）Visual Studio Code Server也可以通过Wget获取。

    > 参考 [The Visual Studio Code Server](https://code.visualstudio.com/blogs/2022/07/07/vscode-server)
    和 [Cannot download VS Code Remote Development via SSH when proxy is needed #78](https://github.com/microsoft/vscode-remote-release/issues/78)

    ```bash
    wget -O- https://aka.ms/install-vscode-server/setup.sh | sh
    ```

4. 运行下面两行命令，建立空的`$HOME/.vscode-server/bin`文件夹。

    ```bash
    mkdir -p ~/.vscode-server/bin
    rm ~/.vscode-server/bin/* -rf   # 把$HOME/.vscode-server/bin下的内容删干净，防止出错
    ```

5. 然后将`vscode-server-linux-x64.tar.gz`上传在服务器上的`$HOME/.vscode-server/bin`文件夹中，解压。

    ```bash
    cd ~/.vscode-server/bin
    tar -zxf vscode-server-linux-x64.tar.gz
    mv vscode-server-linux-x64 ${commit_id} # 注意把:${commit_id}替换成对应的Commit ID
    ```

6. 如果要将新的服务器上的VS Code Server上安装插件包，
   最快的办法就是直接将已安装完插件的服务器上的`$HOME/.vscode-server/extensions`目录打包，
   解压到新服务器上对应位置。
   插件包一般没有版本要求，因此VS Code Server版本不同也能正常使用。

## SSH免密登录

> 参考 [OpenSSH for Windows 中基于密钥的身份验证](https://learn.microsoft.com/zh-cn/windows-server/administration/openssh/openssh_keymanagement)，
  [Windows Terminal：SSH连接远程服务器](https://zhuanlan.zhihu.com/p/445909756)，
  [VS Code配置SSH免密远程登录](https://www.cnblogs.com/safe-rabbit/p/16254860.html)，
  和 [三步完成VS Code配置SSH免密登录远程开发](https://juejin.cn/post/7023042621295558692)
