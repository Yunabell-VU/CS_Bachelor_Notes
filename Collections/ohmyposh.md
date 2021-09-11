# Windows VSCode 终端美化方案



本篇为**WINDOWS**系统下，对 **VS Code** 终端使用`oh-my-posh`进行UI美化的指南。

Mac用户可参考，部分有区别。



## 配色

**此步骤是初级美化方案**， 目的在于调整终端文字的配色。

此文字配色修改和后续的`oh-my-posh`风格修改不冲突，如果不想更改默认配色，可以不看这一步。



打开 VSCode 中的设置 = > 在搜索栏里搜索 `json` => 在搜索结果中 打开 “**在settings.json中编辑**”。

![image-20210911205039145](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20210911205039145.png)

在 **settings.json**文件中，找到 

```json
"workbench.colorTheme": <你的主题>,
```

在这条后面属性后面输入：

```json
"workbench.colorCustomizations": {
    
}
```

比如，你的主题是 `Visual Studio Dark`, 现在你的**setting.json**文件应该是下面这样:

```json
"workbench.colorTheme": "Visual Studio Dark",
"workbench.colorCustomizations": {
}
```



打开以下链接：

https://glitchbone.github.io/vscode-base16-term/#/3024

挑选喜欢的配色方案，点击 "**Copy to clipboard**"

![image-20210911210003602](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20210911210003602.png)



将复制的内容，填入刚才打开的**settings.json** `"workbench.colorCustomizations"`属性中。

比如：

```json
"workbench.colorCustomizations": {
        "terminal.background": "#282936",
        "terminal.foreground": "#f6f6f8",
        "terminalCursor.background": "#E9E9F4",
        "terminalCursor.foreground": "#E9E9F4",
        "terminal.ansiBlack": "#282936",
        "terminal.ansiBlue": "#62D6E8",
        "terminal.ansiBrightBlack": "#626483",
        "terminal.ansiBrightBlue": "#62D6E8",
        "terminal.ansiBrightCyan": "#A1EFE4",
        "terminal.ansiBrightGreen": "#EBFF87",
        "terminal.ansiBrightMagenta": "#B45BCF",
        "terminal.ansiBrightRed": "#EA51B2",
        "terminal.ansiBrightWhite": "#F7F7FB",
        "terminal.ansiBrightYellow": "#00F769",
        "terminal.ansiCyan": "#A1EFE4",
        "terminal.ansiGreen": "#EBFF87",
        "terminal.ansiMagenta": "#B45BCF",
        "terminal.ansiRed": "#EA51B2",
        "terminal.ansiWhite": "#E9E9F4",
        "terminal.ansiYellow": "#00F769"
    }
```



## 字体

`oh-my-posh`的风格效果需要NERD字体支持，因此我们先在这一步提前准备好需要的字体。



打开下面链接：

https://www.nerdfonts.com/font-downloads

选择自己喜欢的字体，然后Download下载。

下载之后解压获得字体，压缩包中所有的文件都选上后右键点击安装：

![image-20210911211153896](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20210911211153896.png)



在VSCode的设置中，搜索 `terminal font`,  并填入你安装好的字体的名称

![image-20210911213017435](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20210911213017435.png)





## oh-my-posh

到这一步开始正式安装 `oh-my-posh`

在VSCode中打开**终端**，shell选择**powershell**

![image-20210911211618250](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20210911211618250.png)



在指令行中输入以下指令安装`oh-my-posh`：

```powershell
Install-Module oh-my-posh -Scope CurrentUser
```



**如果提示权限不足**，请用管理员模式打开Powershell进行安装：

<img src="http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20210911212103580.png" alt="image-20210911212103580" style="zoom: 50%;" />



安装成功后，在VSCode的终端输入以下指令，可看到各种风格方案的预览

```powershell
Get-PoshThemes
```

![image-20210911213253913](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20210911213253913.png)



更改主题方案，只需要以下指令：

```powershell
Set-PoshPrompt -Theme <主题名称>
```

比如，你想要的 `agnoster`风格：

```powershell
Set-PoshPrompt -Theme agnoster
```



这时终端的主题应该成功改变。



但需要注意的是，这个改动是一次性，为了每次打开终端都能自动获得该风格，我们需要修改PROFILE文件。

在**VSCode的终端中**，输入以下指令：

```powershell
if (!(Test-Path -Path $PROFILE )) {New-Item -Type File -Path $PROFILE -Force }
```

接着输入：

```powershell
code $PROFILE
```

此时，应该打开了一个配置文件（可能是个空文件），将以下内容复制其中：

```powershell
Import-Module posh-git
Import-Module oh-my-posh
Set-PoshPrompt -Theme agnoster
```

注意，这里的主题名称可以根据你的需要修改。

`ctrl+S` 保存文档后，在终端输入：

```powershell
echo $profile
```

退出PROFILE文件。



到这一步，整个美化应该已经完成，重启一下VSCode，观察是否美化成功。


## 参考

1. Oh-My-Posh 官网 https://ohmyposh.dev/docs/pwsh
2. Base16 Terminal Colors https://glitchbone.github.io/vscode-base16-term/#/dracula
3. 打造 Windows 优雅终端（Windows Termial+Oh-My-Posh）https://zhuanlan.zhihu.com/p/144611023
4. Nerd Fonts https://www.nerdfonts.com/font-downloads
5. oh-my-posh3及oh-my-zsh提示prompt出现乱码的原因及使用Nerd字体的解决方法 https://blog.csdn.net/yihuajack/article/details/111405007
6. 美化PowerShell（含WindowsTerminal和VSCode终端）https://blog.csdn.net/jeremyjone/article/details/106236656

