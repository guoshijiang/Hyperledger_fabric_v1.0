
# 第二章：Hyperledger fabric入门

## 第一节：安装fabric运行的必要条件

在开始之前，如果您尚未这样做，则可能希望检查是否已在要开发区块链应用程序和/或操作Hyperledger Fabric的平台上安装了所有必备条件。

### 一.安装cURL

如果尚未安装cURL工具或从文档运行curl命令时遇到错误，请下载最新版本的cURL工具。下载地址如下：

https://curl.haxx.se/download.html

如果您使用的是Windows，请参阅下面关于Windows其他版本的具体说明。

### 二.docker和docker compose

您需要在将要运行的平台上安装以下产品，或者在（或为）Hyperledger Fabric上进行开发：

需要MacOSX，*nix或Windows 10：Docker Docker 17.06.2-ce或更高版本。
较旧版本的Windows：Docker Toolbox - 同样需要Docker版本Docker 17.06.2-ce或更高版本。

您可以从终端提示符处使用以下命令检查您已安装的Docker版本：

    docker --version

您可以从终端提示符处使用以下命令检查您安装的Docker Compose的版本：

    docker-compose --version

### 三.go语言

Hyperledger Fabric在其许多组件中使用Go编程语言1.9.x。

鉴于我们正在编写一个`Go`链代码程序，我们需要确保源代码位于`$GOPATH`树中的某处。 首先，你需要检查你是否设置了`$GOPATH`环境变量。

    echo $GOPATH
    /Users/xxx/go
    
如果在回显`$GOPATH`时没有显示任何内容，则需要对其进行设置。 通常情况下，如果您的开发工作空间中有一个目录树子目录，或者您的`$HOME`目录的子目录为该目录树子目录的值，那么该值就是该子目录树的子目录。 由于我们将在Go中执行一系列编码，因此可能需要将以下内容添加到`〜/.bashrc`中：

    export GOPATH=$HOME/go
    export PATH=$PATH:$GOPATH/bin

### 四.Node.js和NPM

如果您将开发利用Hyperledger Fabric的Node.js的SDK开发Hyperledger Fabric应用程序，则需要安装版本8.9.x的Node.js。

注意：Node.js版本9.x目前不受支持。--Node.js-版本8.9.x或更高
注意：安装Node.js也将安装NPM，但建议您确认安装的NPM的版本。 您可以使用以下命令升级npm工具：

    npm install npm@5.6.0 -g

### 五.Python

注意：以下内容仅适用于Ubuntu 16.04用户。

默认情况下，Ubuntu 16.04随Python 3.5.1一起安装为python3二进制文件。 为了使npm安装操作成功完成，Fabric Node.js SDK需要迭代Python 2.7。 使用以下命令检索2.7版本：

    sudo apt-get install python

检查Python版本

  python --version

### Windows的其他说明

如果您正在Windows 7上开发，您将需要在`Docker Quickstart`终端中使用`Git Bash`工作，并为内置`Windows shell`提供更好的替代方案。

然而，经验表明这是一个功能有限的糟糕的开发环境。 适用于运行基于Docker的场景，比如入门，但是在涉及make和docker命令的操作中可能会遇到困难。

在Windows10上，您应该使用本机Docker分配，并且您可以使用`Windows PowerShell`。 但是，要使“特定于下载平台的二进制文件”命令成功，您仍然需要使用uname命令。 你可以把它作为Git的一部分，但要注意只支持64位版本。

在运行任何git克隆命令之前，运行以下命令：

    git config --global core.autocrlf false
    git config --global core.longpaths true
    
您可以使用以下命令检查这些参数的设置：

    git config --get core.autocrlf
    git config --get core.longpaths

这些需要分别是false和true的。

Git和Docker Toolbox附带的·`curl`命令是旧的，无法正确处理入门中使用的重定向。 确保从cURL下载页面安装并使用更新的版本

对于Node.js，您还需要必要的Visual Studio C++构建工具，这些工具可以免费使用，并且可以使用以下命令进行安装：

    npm install --global windows-build-tools

有关更多详细信息，请参见NPM windows-build-tools页面。下面是链接

https://www.npmjs.com/package/windows-build-tools

一旦完成，您还应该使用以下命令安装NPM GRPC模块：
  
    npm install --global grpc


