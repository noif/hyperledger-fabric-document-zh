# Introduction

一般而言，区块链是由一系列 _对等节点_ 维护的不可篡改的transaction账本。每一个对等节点都可以持有
完整的账本，每个block中的所有交易都是经过验证的而且通过后一个block包含前一个block的hash方式来关联。

区块链第一个而且也是最广为人知的应用是[比特币](https://en.wikipedia.org/wiki/Bitcoin)，
引领了很多类似的应用。以太坊，另一个可供选择的加密货币应用，采取了不同的方式来实现，它集成了很多与比特币
相同的特性但是创造性的添加了 _智能合约_ 来构建分布式应用（Dapp）。比特币和以太坊属于一类区块链，我们将
其归类为 _公有链_ 技术，它们是公开网络，对任何人开放的同时参与者之间又是匿名互动。

随着比特币，以太坊和其他一些衍生技术的普及，对于将区块链、分布式账本和分布式应用平台的基础技术
应用于更具创新性的 _企业_ 案例中的需求也随之增长。但是，许多企业用例需要无权区块链技术无法（目前）交付的性能特征。
此外，在许多使用案例中，参与者的身份是一项硬性要求，例如在必须遵循“了解客户”（KYC）和反洗钱（AML）法规的金融交易中。

为了满足企业应用标准，我们需要考虑以下需求：

- 成员之间是确认的或者是可辨别的
- 网络必须是需要 _经过授权_
- 支持高并发特性
- 低交易延迟
- 交易涉及商业机密的保护策略与隐私性

虽然许多早期的区块链平台目前正在兼容企业使用，但Hyperledger Fabric从一开始就被设计用于企业用途。 
以下部分描述了Hyperledger Fabric（Fabric）如何将自己与其他区块链平台区分开来，并描述了其架构决策的一些动机。

## Hyperledger Fabric

Hyperledger Fabric是一种开源的企业级许可分布式分类帐技术（DLT）平台，专为在企业环境中使用而设计，
与其他流行的分布式分类帐或区块链平台相比，它提供了一些关键的差异化功能。

差异化的一个关键点是Hyperledger是在Linux基金会下建立的，该基金会基于 **开放式治理** 模式下在培育开源项目的方面
拥有很长并且很成功的历史，这些开源项目都具有强大社区支持和完善生态系统。Hyperledger由多元化技术指导委员会和
Hyperledger Fabric项目管理，该项目由来自多个组织的各种维护人员组成。它拥有一个开发社区，自最早提交以来已经发展到
超过35个组织和近200个开发人员。

Fabric具有高度模块化和可配置的架构，可为各种行业用例包括但不限于银行，金融，保险，医疗保健，
人力资源，供应链甚至数字音乐交付提供创新化，多功能化和更优化的设计。

Fabric是第一个支持使用通用编程语言（如Java，Go和Node.js）而不是受限制的特定于域的语言（DSL）来创建智能合约的
分布式账本平台。这意味着大多数企业已经拥有开发智能合约所需的技能，并且不需要额外的培训来学习新的语言或DSL。

Fabric平台也是 **许可式** 网络，这意味着，与公共无权网络不同，参与者之间彼此了解，而不是因为匿名所以相互
之间不受信任。这意味着, 虽然参与者可能不完全信任对方 (例如, 他们可能是同一行业中的竞争对手), 但网络可以根据
参与者之间存在的信任建立治理模型来进行管理, 例如创建法律处理纠纷的协议或框架。

该平台最重要的与众不同之处在于它支持可插拔的共识协议，使平台能够更有效地进行定制以适应特定的用例和信任模型。
例如，当部署在单个企业内或由可信任的权威机构运营时，完全拜占庭容错的共识可能被认为是不必要的，并且对性能和吞吐量会
造成过度拖累。 在这种情况下，[crash fault-tolerant](https://en.wikipedia.org/wiki/Fault_tolerance) （CFT）共识协议
可能绰绰有余，而在多方分散用例中，可能需要更传统的[byzantine fault tolerant](https://en.wikipedia.org/wiki/Byzantine_fault_tolerance)（BFT）共识协议。

Fabric可以利用不需要内置 **加密货币** 来激活昂贵的挖矿行为或智能合约的执行 的共识协议。 移除加密货币会减少一些重要的风险/攻击向量，
并且去掉加密挖矿操作意味着可以使用与任何其他分布式系统大致相同的运营成本来部署平台。

这些差异化设计特性的结合使Fabric成为了当今在业务处理和事务确认延迟方面性能 **更好的平台** 之一，因为它靠隐私和隐秘的transaction和智能合同 (什么结构调用 "chaincode") 来实现

让我们更详细地探索这些差异化的功能。

## Modularity

Hyperledger Fabric经过专门设计，具有模块化架构。无论是可插拔的共识，可插拔的身份管理协议（如LDAP或OpenID Connect），密钥管理协议还是加密库，该平台的核心都经过精心设计，以满足企业用例需求的多样性。

在高层次上，Fabric由以下模块化组件组成：

- 可插拔 _order服务_ 就交易顺序建立共识，然后向peers广播blocks

- 可插拔的 _MSP_ 负责将网络中的实体与加密身份相关联

- 可选的 _p2p gossip 服务_ 使peers之间可以同步由order产生的blocks

- 智能合约("chaincode")在一个隔离的容器环境中（如Docker）运行。它们由标准语言写成但是却不能够与账本状态
进行直接交互

- 账本存储可以通过配置来支持多种种DBMS

- 可插拔的背书和验证策略可以灵活地被每个应用独立配置

业界已经对“没有一个区块链可以统治所有”达成了共识。Hyperledger Fabric可以通过多种方式进行配置，
以满足多个行业用例的各种解决方案要求。

## Permissioned vs Permissionless Blockchains

在一个无权限的区块链中，几乎任何人都可以参与，每个参与者都是匿名的。在这种情况下，
除了在某个深度之前区块链的状态是不可变的之外，彼此之间不存在任何信任。为了减轻这种信任的缺失，
无权限的区块链通常采用“挖矿”的形式或者收取交易费用来提供经济激励，以抵消参与基于“工作证明”（PoW）的拜占庭容错共识所需的成本。

相对来说，许可的区块链是在一组已知的，已识别的且经常经过审查的参与者中操作区块链，这些参与者在一种
产生一定程度信任的治理模型下运作。许可的区块链提供了一种方法来保护具有共同目标但可能彼此不完全信任的
一组实体之间的交互。通过依赖参与者的身份，许可的区块链可以使用更传统的崩溃容错（CFT）或拜占庭容错（BFT）共识协议，
而不需要昂贵的挖矿。

另外，在这种许可的背景下，参与者通过智能合约故意引入恶意代码的风险降低。首先，参与者彼此了解并且所有动作，
无论是提交应用程序事务，修改网络配置还是部署智能合约，都会在为网络和相关交易类型建立的背书策略下执行并记录
在区块链上。而正是不完全匿名，所以可以很容易地识别有罪方，并根据治理模式的条款处理事件。

## Smart Contracts

智能合约（或者Fabric称之为”chaincode“）作为受信任的分布式应用程序，区块链通过peer之间的共识
使得其更加安全/可行。它所实现的是商业业务逻辑。

有三个关键点适用于智能合约，尤其是应用于平台时：

- 同一个网络中运行着很多智能合约
- 它们有可能被动态部署（很多情况下被任何人）
- 因此应用程序代码应视为不受信任，甚至可能是恶意的

大多数现有的具有智能合约能力的区块链平台遵循 **order-execute** 架构，其中共识协议：

- 验证并排序transactions然后将它们传播到所有peer节点
- 每个peer顺序执行transactions

几乎所有现有的区块链系统都可以找到order-execute架构，范围从公共无权限平台，如 [Ethereum](https://ethereum.org/) 
（基于PoW的共识）到许可式平台，如[Tendermint](http://tendermint.com/)， [Chain](http://chain.com/)和[Quorum](http://www.jpmorgan.com/global/Quorum)。

在order-execute架构区块链中执行的智能合约必须是确定性的; 否则，可能永远不会达成共识。
为了解决非确定性问题，许多平台要求智能合约以非标准或特定于的语言（例如[Solidity](https://solidity.readthedocs.io/en/v0.4.23/))）来编写，以便可以消除非确定性操作。
这阻碍了广泛采用，因为它要求开发人员编写智能合同以学习新语言并可能导致编程错误。

此外，由于所有节点都顺序执行所有transactions，因此性能和规模有限。正是由于智能合约代码在系统中的每个节点上需要执行的情况所以必须
采取复杂措施来保护整个系统免受潜在恶意合同的影响，以确保整个系统的弹性。

## A New Approach

Fabric引入了一种新的被称为 **execute-order-validate** 体系架构来操作transactions。
它通过将transaction流分为三个步骤来解决order-execute模型面临的弹性，灵活性，可伸缩性，性能和机密性挑战：

- _execute_ 执行一个transaction并检查其正确性，从而背书认可它
- _order_ transactions 通过可插拔的共识协议进行共识
- _validate_ transactions 在将提交到分类帐之前，根据特定于应用程序的背书策略验证transactions

这种设计与order-execute形式完全不同，因为Fabric在达成transactions的最终共识之前执行交易

在Fabric中，特定于应用程序的背书策略指定哪些peer节点或多少peer节点需要保证正确执行给定的智能合约。
因此，每个transaction只需要由满足事务的背书策略所必需的peer节点的子集来执行（认可）。
这样就会允许并行执行，从而提高系统的整体性能和规模。因为在排序之前可以滤除不一致的结果，第一阶段也 **消除了任何非确定性** 。

因为我们已经消除了非确定性，所以Fabric是第一个 **能够使用标准编程语言** 的区块链技术。
在1.1.0版本中，智能合约可以用Go或Node.js编写，而有计划在后续版本中支持其他流行语言，包括Java。

## Privacy and Confidentiality

正如我们所讨论的，在一个公共的，无权限的区块链网络中，利用PoW作为其共识模型，transactions在每个节点上执行。
这意味着合约本身和他们处理的交易数据都不存在机密性。每个transaction以及实现它的代码对于网络中的每个节点都是可见的。
在这种情况下，我们交换了由PoW提供的拜占庭容错共识的合同和数据的机密性。

对于许多商业/企业用例而言，这种机密性的缺乏可能会有问题。例如，在供应链合作伙伴网络中，某些消费者可能会获得优惠利率
作为巩固关系或促进额外销售的手段。如果每个参与者都可以看到每个合同和交易，那么就无法在完全透明的网络中维持这种业务关系 - 
每个人都希望获得优惠费率！

再举个例子，考虑证券业，其中一名商人建立一个位置（或其中的处置）后不希望她的竞争对手知道这一点，否则他们将寻求获得在游戏中
削弱了交易商的开局。

为了解决隐私和机密性在企业用例要求中的缺乏，区块链平台采用了多种方法。当然每个人都有自己的权衡。

数据加密是提供机密性的一种方法; 然而，在利用PoW达成共识的无权网络中，加密数据位于每个节点上。如果有足够的时间和计算资源，
加密可能会被打破。对于许多企业用例来说，其信息可能受到损害的风险是不可接受的。

零知识证明（ZKP）是正在探索解决该问题的另一个研究领域，这里需要考虑的是计算ZKP需要相当多的时间和计算资源。
因此, 这种情况下的权衡是对保密性的表现。

在可以利用其他形式来共识的无许可背景下, 人们可能会探讨限制将机密信息仅分配给授权节点的方法。

Hyperledger Fabric是一个经过许可的平台，通过其channel架构实现机密性。 基本上，Fabric网络上的参与者可以在
参与者子集之间建立“channel”，该channel被授予对特定transactions集的可见性。类似于网络覆盖。 因此，只有加入该channel的节点
才能访问智能合约（链代码）和进行数据交易，从而保护两者的隐私和机密性。

为了进一步提高其隐私和机密性，Fabric增加了对[private data](./private-data/private-data.html) 的支持，
并且正在开发未来可用的零知识证明（ZKP）。更详细内容敬请期待。

## Pluggable Consensus

transactions的排序被委派给一个模块化共识组件, 这样就使其与执行transactions和维护账本的peer逻辑上分离。
特别的是，排序服务由于共识是模块化的，因此可以根据特定部署或解决方案的信任假设来定制其实现。这种模块化架构允许平台
依赖完善的工具包进行CFT（崩溃容错）或BFT（拜占庭容错）排序。

在现有的releases版本中，Fabric提供了基于CFT（[Kafka](https://kafka.apache.org/) and
[Zookeeper](https://zookeeper.apache.org/)）的排序服务。在随后的版本中，Fabric将提供使用etcd / Raft（（[Raft consensus ordering service](https://raft.github.io/)））共识排序服务以及完全分分布式的BFT排序服务。

另请注意，这些并不相互排斥。Fabric网络可以具有多种排序服务，支持不同的应用或应用要求。

## Performance and Scalability

区块链平台的性能可能会受到许多变量的影响，例如transaction大小，块大小，带宽以及硬件限制等.
Hyperledger社区目前正在编写性能和规模工作组中的一组 [度量标准](https://docs.google.com/document/d/1DQ6PqoeIH0pCNJSEYiw7JVbExDvWh_ZRVhWkuioG4k0/edit#heading=h.t3gztry2ja8i) ，并相应地开发了一个名为 [Hyperledger Caliper](https://wiki.hyperledger.org/projects/caliper)的基准框架。

虽然这项工作仍在继续开发并且应该被视为区块链平台性能和规模特征的明确衡量标准，但IBM Research的一个团队还是先行发表了一份 [peer reviewed paper](https://arxiv.org/abs/1801.10228v1)，评估了Hyperledger Fabric的架构和性能。该文提供了对Fabric架构的深入讨论，然后使用报告对Hyperledger Fabric v1.1平台的初步版本的进行了性能评估。

研究团队所做的基准测试工作为Fabric v1.1.0版本带来了大量的性能改进，从v1.0.0版本级别将平台的整体性能提高了一倍以上。

## Conclusion

鉴于要使用对区块链平台的任何认真评估都应该在其候选名单中包含Hyperledger Fabric。

结合Fabric的差异化功能使其成为一个高度可扩展的系统，用于支持灵活的信任假设的许可区块链，使该平台能够
支持从政府，金融，供应链物流到医疗保健等各种行业用例。

更重要的是，Hyperledger Fabric是（目前）十个Hyperledger项目中最活跃的。围绕平台的社区建设正在稳步增长，每个连续版本提供的
创新远远超过任何其他企业区块链平台。

## Acknowledgement

The preceding is derived from the peer reviewed
["Hyperledger Fabric: A Distributed Operating System for Permissioned Blockchains"](https://arxiv.org/abs/1801.10228v1) - Elli Androulaki, Artem
Barger, Vita Bortnikov, Christian Cachin, Konstantinos Christidis, Angelo De
Caro, David Enyeart, Christopher Ferris, Gennady Laventman, Yacov Manevich,
Srinivasan Muralidharan, Chet Murthy, Binh Nguyen, Manish Sethi, Gari Singh,
Keith Smith, Alessandro Sorniotti, Chrysoula Stathakopoulou, Marko Vukolic,
Sharon Weed Cocco, Jason Yellick
