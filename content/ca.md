# 第三章：HyperLedger证书认证服务

本章的内容的构建来自“主”分支

Hyperledger fabric CA是Hyperledger fabric的认证中心（CA）。

它提供了以下功能：

* 注册身份，或者连接到LDAP作为用户注册表
* 发放登记证书（ECerts）
* 证书更新和撤销

Hyperledger fabric CA由服务器和客户端组件组成。

如果您兴趣参与Hyperledger Fabric CA的开发人员，请参阅Fabric CA存储库以获取更多信息。

## 第一节.概述

下图说明了Hyperledger Fabric CA服务器如何适用于整体Hyperledger Fabric架构。

图片1： 
    ![图片1](https://github.com/guoshijiang/Hyperledger_fabric_v1.0/blob/master/img/1.png "图片1")

有两种与Hyperledger Fabric CA服务器进行交互的方式：通过Hyperledger Fabric CA客户端或通过某个Fabric SDK进行交互。 与Hyperledger Fabric CA服务器的所有通信均通过REST API提供。 有关这些REST API的swagger文档，请参阅fabric-ca/swagger/swagger-fabric-ca.json。

Hyperledger Fabric CA客户端或SDK可能连接到Hyperledger Fabric CA服务器群集中的服务器。 这在图的右上部分中说明。 客户端路由到HA代理端点，该端点将流量负载平衡到fabric-ca-server集群成员之一。

群集中的所有Hyperledger Fabric CA服务器都共享相同的数据库以跟踪身份和证书。 如果配置了LDAP，则身份信息将保存在LDAP中而不是数据库中。

一台服务器可能包含多个CA。 每个CA都是根CA或中间CA. 每个中间CA都有一个父CA，它是根CA或另一个中间CA.






