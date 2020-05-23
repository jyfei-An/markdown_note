# PowerShell 

## -NoLogo

​    启动时隐藏版权标志

## -Version

启动指定版本的 Windows PowerShell，使用参数输入版本号，如 "-version 2.0"。

## -PSConsoleFile

​    加载指定的 Windows PowerShell 控制台文件。若要创建控制台
​    文件，请在 Windows PowerShell 中使用 Export-Console。

## -Mta

​    使用多线程单元启动 shell。

## -NoProfile

​    不加载 Windows PowerShell 配置文件。

## -NonInteractive

​    不向用户显示交互式提示。

## -InputFormat

​    描述发送到 Windows PowerShell 的数据的格式。有效值为
​    "Text" (文本字符串)或 "XML" (序列化的 CLIXML 格式)。

## -OutputFormat

​    确定如何设置 Windows PowerShell 输出内容的格式。有效值
​    为 "Text" (文本字符串)或 "XML" (序列化的 CLIXML 格式)。

## -WindowStyle

​    将窗口样式设置为 Normal、Minimized、Maximized 或 Hidden。

## -EncodedCommand

​    接受 base-64 编码字符串版本的命令。使用此参数
​    向 Windows PowerShell 提交需要复杂引号
​    或大括号的命令。

## -ConfigurationName

​    指定运行 Windows PowerShell 的配置终结点。
​    该终结点可以是在本地计算机上注册的任何终结点，包括
​    默认的 Windows PowerShell 远程处理终结点或具有特定用户角色功能
​    的自定义终结点。

## -File

​    在本地作用域("dot-sourced")中运行指定的脚本，以便
​    脚本创建的函数和变量可以在当前
​    会话中使用。输入脚本文件路径和任何参数。
​    File 必须是命令中的最后一个参数，因为在 File 参数
​    名称后面键入的所有字符都将解释
​    为后跟脚本参数的脚本文件路径。

## -ExecutionPolicy

​    设置当前会话的默认执行策略，并将其保存
​    在 $env:PSExecutionPolicyPreference 环境变量中。
​    该参数不会更改在注册表中
​    设置的 Windows PowerShell 执行策略。

## -Command

​    执行指定的命令(和任何参数)，就好像它们是
​    在 Windows PowerShell 命令提示符下键入的一样，然后退出，除非
​    指定了 NoExit。Command 的值可以为 "-"、字符串或
​    脚本块。



## ExecutionPolicy Bypass

绕过当前执行策略，无障碍运行脚本



# 查找文件

```
//查找C盘根目录(包括递归子目录)下的所有test.png文件
dir /S test.png
```



# 切换盘目录

```
 c:/
```



# 切换目录

```
cd path
```



# 注释

```
REM 语句
```





# 创建文件夹

```
mkdir 文件夹名
```





# 删除文件夹

```
rmdir /s/q 文件夹名
```





# 查看当前目录文件

```
dir
```





