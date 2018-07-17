# What's new in v1.2

快速了解Hyperledger Fabric v1.2版本中的新功能和文档：

## New major features

* **[Private Data Collections](https://hyperledger-fabric-document-zh.readthedocs.io/en/release-1.2/private-data/private-data.html)**:
  一种在某些channel成员中保持某些数据/交易私有化的方法。我们还有一个关于这个主题的架构文档，可以在 [这里](https://hyperledger-fabric-document-zh.readthedocs.io/en/latest/private-data-arch.html)找到.

* **[Service Discovery](https://hyperledger-fabric-document-zh.readthedocs.io/en/release-1.2/discovery-overview.html)**:
  动态发现网络服务，包括orders，peers，chaincode和背书策略，以简化客户端应用程序。

* **[Access control](https://hyperledger-fabric-document-zh.readthedocs.io/en/release-1.2/access_control.html)**:
  如何配置哪些客户端标识可以在每个channel基础上与peer进行功能交互

* **[Pluggable endorsement and validation](https://hyperledger-fabric-document-zh.readthedocs.io/en/release-1.2/pluggable_endorsement_and_validation.html)**:
  每个chaincode使用可插拔的背书和校验策略。

### New tutorials

* **[Upgrade to version v1.2](https://hyperledger-fabric-document-zh.readthedocs.io/en/release-1.2/upgrade_to_newest_version.html)**:
  利用BYFN网络显示升级流程应如何工作。包括脚本（可用作升级模板）以及各个命令。

* **[CouchDB](https://hyperledger-fabric-document-zh.readthedocs.io/en/release-1.2/couchdb_tutorial.html)**:
  如何设置CouchDB（允许丰富的查询）进行数据存储

* **[Private data](https://hyperledger-fabric-document-zh.readthedocs.io/en/release-1.2/private_data_tutorial.html)**:
  显示如何使用 BYFN 设置collection

* **[Query certificates based on various filter criteria (Fabric CA)](https://hyperledger-fabric-ca.readthedocs.io/en/latest/users-guide.html#manage-certificates)**:
  Describes how to use `fabric-ca-client` to manage certificates.

### New conceptual documentation

* **[Fabric network as a concept](https://hyperledger-fabric-document-zh.readthedocs.io/en/release-1.2/network/network.html)**:
  了解Fabric网络的各个部分的结构以及它们如何交互

* **Private data**: See above.

### Other new documentation

* **[Service Discovery CLI](https://hyperledger-fabric-document-zh.readthedocs.io/en/release-1.2/discovery-cli.html)**:
  使用CLI配置发现服务

## Release notes

For more information, including `FAB` numbers for the issues and code reviews
that made up these changes (in addition to other hygiene/performance/bug fixes
we did not explicitly document), check out the:

* [Fabric release notes](https://github.com/hyperledger/fabric/releases/tag/v1.2.0).
* [Fabric CA release notes](https://github.com/hyperledger/fabric-ca/releases/tag/v1.2.0).

<!--- Licensed under Creative Commons Attribution 4.0 International License
https://creativecommons.org/licenses/by/4.0/ -->
