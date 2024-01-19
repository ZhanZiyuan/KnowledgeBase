# [PowerShell][]常用命令

> First created by *Ziyuan Zhan* on September 16th, 2023. Last updated on September 18th, 2023.
>> 基于Windows PowerShell 5.1和PowerShell 7

1. 查看PowerShell版本
    > 来自 [查看PowerShell版本](https://blog.csdn.net/H_O_W_E/article/details/122853549)

    ```powershell
    $PSVersionTable
    ```

2. 运行以下命令以安装 NuGet 提供程序
    > 来自 [更新用于 Windows PowerShell 5.1 的 PowerShellGet](https://learn.microsoft.com/zh-cn/powershell/gallery/powershellget/update-powershell-51?view=powershellget-2.x)

    ```powershell
    Install-PackageProvider -Name NuGet -Force
    ```

3. 以下命令尝试在没有 NuGet 提供程序的情况下安装更新的 PowerShellGet 模块
    > 来自 [更新用于 Windows PowerShell 5.1 的 PowerShellGet](https://learn.microsoft.com/zh-cn/powershell/gallery/powershellget/update-powershell-51?view=powershellget-2.x)

    ```powershell
    Install-Module PowerShellGet -AllowClobber -Force
    ```

4. 将 PowerShell 库注册为受信任的存储库
    > 来自 [更新用于 Windows PowerShell 5.1 的 PowerShellGet](https://learn.microsoft.com/zh-cn/powershell/gallery/powershellget/update-powershell-51?view=powershellget-2.x)

    ```powershell
    Set-PSRepository -Name PSGallery -InstallationPolicy Trusted
    ```

5. 显示目录树
    > 来自 [tree](https://learn.microsoft.com/zh-cn/windows-server/administration/windows-commands/tree)

    ```powershell
    tree \
    ```

6. 使用Winget查看所有可升级的包

    ```powershell
    winget upgrade
    ```

7. 在PowerShell模拟Bash中的`top`命令
    > 来自 [Linux "Top" command for Windows Powershell?](https://superuser.com/questions/176624/linux-top-command-for-windows-powershell)

    ```powershell
    While(1) {ps | sort -des cpu | select -f 15 | ft -a; sleep 1; cls}
    ```

8. 在PowerShell模拟Bash中的`screenfetch`命令
    > 来自 [windows-screenfetch 1.0.2](https://www.powershellgallery.com/packages/windows-screenfetch/1.0.2)

    ```powershell
    # 安装Windows ScreenFetch
    Install-Module -Name windows-screenfetch
    ```

9. 导入模块`PoshColor`

    ```powershell
    Import-Module PoshColor
    ```

10. 查看模块`PoshColor`的所有主题

    ```powershell
    Get-PoshColorThemes
    ```

11. 查看模块`oh-my-posh`的所有主题
    > 来自 [Themes](https://ohmyposh.dev/docs/themes)

    ```powershell
    Get-PoshThemes
    ```

12. 使用Python模块`glances`

    ```powershell
    glances
    ```

13. 通过`Get-Process`获取指定`ProcessName`的所有进程，并使用`Stop-Process`结束它们

    ```powershell
    Get-Process -Name "WeChat" | Stop-Process -Force
    ```

[PowerShell]:
https://learn.microsoft.com/zh-cn/powershell/scripting/install/installing-powershell-on-windows?view=powershell-7.3
