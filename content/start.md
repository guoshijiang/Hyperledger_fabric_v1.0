
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

## 第二节：安装二进制文件和Docker镜像

在我们致力于开发Hyperledger Fabric二进制文件的真正安装程序时，我们提供了一个脚本，可以将特定于平台的二进制文件下载到您的系统。 该脚本还会将Docker镜像下载到您的本地注册表中。

## 第三节：Hyperledger Fabric样例

在教程开始之前，我们提供了一组示例应用程序，您可能希望安装这些Hyperledger结构示例，因为教程利用示例代码。

注意：如果您在Windows上运行，您将需要使用Docker Quickstart终端来获取即将发布的终端命令。 如果您以前没有安装它，请访问必备条件部分。如果您在Windows7或macOS上使用Docker Toolbox，则在安装和运行示例时，您需要使用C:\Users（Windows 7）或/Users（macOS）下的位置。如果你是在Mac上使用Docker，则需要使用/Users，/Volumes，/private或/tmp下的位置。 要使用不同的位置，请参阅Docker文档以进行文件共享。如果你是在windows平台上使用的是Docker，请参阅Docker文档中的共享驱动器，并使用其中一个共享驱动器下的位置。

确定在计算机上的特定位置放置Hyperledger Fabric示例应用程序存储库，并在终端窗口中打开该位置。 然后，执行以下命令：

        git clone -b master https://github.com/hyperledger/fabric-samples.git
        cd fabric-samples
        git checkout {TAG}
       
为了确保样本与您在下面下载的Fabric二进制文件版本兼容，请检查与您的Fabric版本相匹配的样本{TAG}，例如v1.1.0。 要查看所有面料样本标签的列表，请使用命令“git tag”。

### 一.下载特定于平台的二进制文件

接下来，我们将安装Hyperledger Fabric平台特定的二进制文件。 此过程旨在补充上面的Hyperledger Fabric样例，但可以单独使用。 如果您没有安装上述示例，那么只需创建并输入一个目录，在该目录中提取特定于平台的二进制文件的内容。

请从您将解压缩特定于平台的二进制文件的目录中执行以下命令：

    curl -sSL https://goo.gl/6wtTN5 | bash -s 1.1.0

注意：如果运行上述curl命令时出现错误，则可能会有太旧的卷曲版本，无法处理重定向或不支持的环境。请查看必备条件部分，了解有关在哪里可以找到最新版本的curl并获得正确环境的其他信息。 或者，您可以替换未缩短的网址：https：//github.com/hyperledger/fabric/blob/master/scripts/bootstrap.sh

注意：您可以使用上述命令来发布任何已发布的Hyperledger Fabric版本。 只需将“1.1.0”替换为您希望安装的版本的版本标识符即可。

上面的命令下载并执行bash脚本，该脚本将下载并提取所有需要设置网络并将它们放入上面创建的克隆仓库的平台指定定二进制文件。 它检索四个特定于平台的二进制文件：
* cryptogen,
* configtxgen,
* configtxlator,
* peer
* orderer和fabric-ca-client

并将它们放在当前工作目录的bin子目录中。

您可能希望将其添加到PATH环境变量中，以便可以在不完全限定每个二进制文件的路径的情况下提取它们。 例如：

        export PATH=<path to download location>/bin:$PATH

最后，脚本会将来自Docker Hub的Hyperledger Fabric docker镜像下载到您的本地Docker注册表中，并将它们标记为“最新”。

该脚本列出了在结束时安装的Docker镜像。

查看每个镜像的名称; 这些组件将最终构成我们的Hyperledger Fabric网络。 您还会注意到，您有两个相同镜像ID的实例 - 一个标记为“x86_64-1.x.x”，一个标记为“最新”。

注意：在不同的体系结构中，x86_64将被替换为标识您的体系结构的字符串。

## 第四节：Hyperledger Fabric API文档

Hyperledger Fabric的Golang API的API文档可以在Fabric的Godoc站点上找到。 如果您打算使用这些API进行任何开发，你可以点击下面的链接进去看。
    
https://godoc.org/github.com/hyperledger/fabric

## 第五节：Hyperledger Fabric SDK

Hyperledger Fabric旨在为各种编程语言提供许多SDK。前两个交付的SDK是Node.js和Java SDK。 在后续版本中将会提供Python，REST和Go SDK。

* Node.js的SDK英语文档： https://fabric-sdk-node.github.io/
* Java的SDK英语文档：https://github.com/hyperledger/fabric-sdk-java

关于上面这两个文档的内容我们将会在后面的章节中介绍

## 第六节:Hyperledger Fabric证书认证服务

Hyperledger Fabric提供可选的证书颁发机构服务，您可以选择使用该服务来生成证书和密钥材料，以配置和管理区块链网络中的身份。 但是，可以使用任何可以生成ECDSA证书的CA.关于证书的详细内容将会在后面章节中介绍











