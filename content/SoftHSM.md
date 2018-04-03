# 第四章：SoftHSM第二版简单介绍

## 第一节：概览

OpenDNSSEC是一个基于策略的区域签名者，可以自动跟踪DNSSEC密钥和区域签名。 该项目的目标是使DNSSEC易于部署。 该项目是开放源代码，旨在推动域名系统安全扩展（DNSSEC）的采用，以进一步增强互联网安全。

OpenDNSSEC通过PKCS＃11接口处理和存储其加密密钥。 该接口指定如何与加密设备（如HSM：（硬件安全模块）和智能卡）进行通信。 除其他外，这些设备的目的是在不向外界透露私钥资料的情况下生成加密密钥和签名信息。 与普通计算机中的普通进程相比，它们经常被设计为在这些特定任务上表现良好。

使用PKCS＃11接口的潜在问题是，它可能会限制OpenDNSSEC的广泛使用，因为潜在用户可能不愿意投资于新的硬件设备。 为了解决这个问题，OpenDNSSEC提供了一个带有PKCS＃11接口的通用加密设备SoftHSM的软件实现。 SoftHSM旨在满足OpenDNSSEC的要求，但由于PKCS＃11接口，它还可以与其他加密产品一起使用。

一旦安装和配置，OpenDNSSEC将自动执行关键管理和区域签名活动。OpenDNSSEC接收未签名的区域，为DNSSEC添加签名和其他记录，并将区域传递给该区域的权威名称服务器。它根据密钥和签名策略（KASP）执行此操作，该策略描述了组织如何配置DNSSEC。

图片2： 
    ![图片2](https://github.com/guoshijiang/Hyperledger_fabric_v1.0/blob/master/img/2.png "图片2")

## 第二节：依赖

SoftHSM取决于加密库Botan或OpenSSL。 最低要求版本：

* Botan 1.10.0
* OpenSSL 1.0.0

如果您使用的是Botan，请确保它支持GNU MP（--with-gnump）。这将改善执行公钥操作时的性能。

GNU Autotools也是构建软件所必需的。

有一个迁移工具可将令牌数据库从SoftHSMv1转换为新的令牌类型。 如果建立了这个工具，那么SQLite3是必需的（> = 3.4.2）。

## 第三节：安装

### 1.配置

配置安装/编译脚本：

    sh ./autogen.sh
    ./configure

选项：

    --disable-non-paged-memory
          Disable non-paged memory for secure storage
          (default enabled)
    --disable-ecc		Disable support for ECC (default enabled)
    --disable-eddsa		Disable support for EDDSA (default enabled)
    --disable-gost		Disable support for GOST (default enabled)
    --disable-visibility	Disable hidden visibilty link mode [enabled]
    --with-crypto-backend	Select crypto backend (openssl|botan)
    --with-openssl=PATH	Specify prefix of path of OpenSSL
    --with-botan=PATH	Specify prefix of path of Botan
    --with-migrate		Build the migration tool. Used when migrating
          a SoftHSM v1 token database. Requires SQLite3
    --with-objectstore-backend-db
          Build with database object store (SQLite3)
    --with-sqlite3=PATH	Specify prefix of path of SQLite3
    --disable-p11-kit	Disable p11-kit integration (default enabled)
    --with-p11-kit=PATH	Specify install path of the p11-kit module, will
          override path given by pkg-config

更多选项

  ./configure --help


### 2.编译

使用以下命令编译源代码：

    make

### 3.安装库

使用以下命令安装库：

    sudo make install

### 4.配置

配置文件的默认位置是/etc/softhsm2.conf。 这个位置可以通过设置环境变量来改变。

    export SOFTHSM2_CONF=/home/user/config.file

关于配置的详细信息可以在“man softhsm2.conf”中找到。

创建您在配置文件中定义的令牌目录：

    mkdir <token_dir>

### 5.初始化令牌

使用softhsm2-util或PKCS＃11接口。 SO PIN可以例如 用于重新初始化令牌，并将用户PIN发给应用程序，以便它可以与令牌交互。

      softhsm2-util --init-token --slot 0 --label "My token 1"

输入SO PIN和用户PIN。 一旦令牌被初始化，更多的插槽将自动添加一个新的未初始化的令牌。
    
已初始化的令牌将被重新分配给另一个插槽（基于令牌序列号）。 建议通过在槽列表/令牌信息中搜索令牌标签或序列号来查找并与令牌交互。

## 第四节：备份

所有的令牌及其对象都存储在softhsm2.conf给出的位置。 因此备份可以作为常规文件副本来完成。

## 第五节：日志信息

日志信息发送到系统日志或Windows事件日志，日志级别在配置文件中设置。 每个日志事件都附带有源文件名和行号。

## 第六节：从仓库构建

如果代码是直接从代码库下载的，则必须先准备配置脚本，然后再继续使用真实的README。

* 您需要安装automake，autoconf，libtool等。
* 运行命令'sh autogen.sh'
* 继续阅读本自述文件。










