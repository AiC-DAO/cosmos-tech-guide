# Cosmos生态技术栈入门指南

## 引言

[AiC DAO](https://twitter.com/AiC_DAO)在入门学习Cosmos生态技术之初，深感学习资料之匮乏，特别是中文技术资料。

为了方便后来的技术人员能一览Cosmos技术，做到快速入门，快速学习，快速上手开发，特制作维护本文档。

本文档对Cosmos技术栈涉及到的各个方面做简要介绍，并给出相关学习链接，大家自取。

## 核心技术

### Tendermint Core

Tendermint Core是Cosmos应用链的共识引擎，主要负责底层的区块验证打包和P2P网络通信等，它需要确保相同的交易以相同的顺序记录在每台机器上，但它不负责具体的应用逻辑处理。Tendermint Core通过ABCI(Application BlockChain Interface)接口与具体的应用程序进行交互，由于该接口将共识引擎和应用逻辑隔离开，因此，开发者可以在应用层使用任何流行的开发语言开发应用。在Cosmos生态最流行的应用开发语言为Go和Rust，对于Go语言，提供了开箱即用的Cosmos SDK。

Github：[Tendermint Core ](https://github.com/tendermint/tendermint)

技术规范：[tendermint/spec](https://github.com/tendermint/tendermint/tree/main/spec)

开发文档：[Quick Start | Tendermint Core](https://docs.tendermint.com/v0.34/introduction/quick-start.html)

### Cosmos SDK

正如上文所述，Cosmos SDK给Go开发者提供了一个开箱即用的区块链应用开发框架，SDK提供了一些常用的/公用的区块链功能，将其打包为模块，开发者只需使用这些现有模块和自定义的模块(每条链按自己的应用需求而定)，即可快速开发部署一条区块链，一般使用Cosmos SDK开发的区块链称为应用链( application-specific blockchains)。

Github：[cosmos/cosmos-sdk](https://github.com/cosmos/cosmos-sdk)

开发文档：[Cosmos SDK Documentation | Cosmos SDK](https://docs.cosmos.network/main)

### IBC Protocol

IBC协议(Inter-Blockchain Communication Protocol)，正如TCP/IP之与PC机，IBC是一种通用的互操作性协议，允许两个不同的区块链相互通信。IBC 保证可靠、有序和经过身份验证的通信。世界因互联的丰富多彩，IBC是Cosmos的精髓灵魂所在，也是其成功的最重要基石。IBC协议的Go实现版本也是SDK的一个重要模块。

正如HTTP、HTTPS、FTP等建立在TCP/IP协议之上的应用层协议一样，IBC同样有自己的应用层协议，且在迅速丰富，蓬勃发展，如用于代币传输的ICS20协议，用户区块链间互操作的ICA(链间账户)/ICQ(链间查询)等等。

Github(Go实现)：[cosmos/ibc-go](https://github.com/cosmos/ibc-go)

协议概览：[什么是 IBC？](https://medium.com/the-interchain-foundation/eli5-what-is-ibc-def44d7b5b4c)

技术规范：[cosmos/ibc: Interchain Standards (ICS) ](https://github.com/cosmos/ibc)

开发文档：[IBC Go Documentation](https://ibc.cosmos.network/)

在IBC协议里，区块链不直接通过网络相互传递消息，而是使用中继器。中继器进程监视启用 IBC 的链之间的开放路径上的更新。 中继器以特定消息类型的形式将这些更新提交给交易对手链，然后使用客户端来跟踪和验证共识状态。

Github(Go中继器实现)：[cosmos/relayer](https://github.com/cosmos/relayer)

Github(Rust中继器实现)：[informalsystems/hermes](https://github.com/informalsystems/hermes)

Github(TS中继器实现)：[confio/ts-relayer](https://github.com/confio/ts-relayer)

### CosmWasm

CosmWasm是Cosmos应用链启用智能合约能力的标准平台，同样其作为SDK的一个标准模块提供给开发者。这意味着目前使用SDK构建区块链的任何人都可以快速轻松地将CosmWasm智能合约支持添加到他们的链中，而无需调整现有逻辑。Rust是目前CosmWasm使用最多的编程语言，未来可能会有不同的编程语言支持。

Github：[CosmWasm/cosmwasm](https://github.com/CosmWasm/cosmwasm)

开发文档：[CosmWasm Documentation](https://docs.cosmwasm.com/docs/1.0/)



## 客户端

为了与运行的Cosmos应用链交互(如查询/转账等)，需要客户端工具完成这些动作，本节介绍Cosmos常用的客户端工具。

### CosmJS

JS/TS客户端CosmJS，探索Cosmos应用链的瑞士军刀，被广泛应用在dApp，浏览器，钱包，爬虫，自动化bot等各个领域。

Github：[CosmJS](https://github.com/cosmos/cosmjs)

API文档：https://cosmos.github.io/cosmjs/

中文区大佬写的一些用例：[ericet/cosmos-learn ](https://github.com/ericet/cosmos-learn)

### lens

Go客户端lens，lens由Cosmos生态的核心开发小组strangelove开发维护，该工具旨在提供一个命令行工具与所有支持Cosmos SDK**核心模块**的应用链交互。该开发小组也是IBC协议Go中继器(主流使用版本)的核心贡献。

Github：[lens](https://github.com/strangelove-ventures/lens)

暂无开发文档。

除了作为命令行工具与应用链交互，你也可以将lens作为你自己Go工程的一个package来使用，下面是官方提供一些使用场景：

Github：[lens-examples ](https://github.com/strangelove-ventures/lens-examples)

### CosmPy

Python客户端CosmPy，CosmPy由Fetch.ai团队开发维护，同样该客户端提供了命令行工具与Cosmos应用链交互，且提供了接口部署交互智能合约(lens不具备该能力)。

Github：[CosmPy](https://github.com/fetchai/cosmpy)

开发文档：[Getting started - Developer Documentation (fetch.ai)](https://docs.fetch.ai/CosmPy/)

## CosmWasm合约开发

CosmWasm在Cosmos应用链中日益扮演着重要角色，因此对于开发者来说，特别是2C项目方的开发者，CosmWasm合约(后文简称CW合约)开发能力也成了一项必备技能。本小节将总结目前常用的一些CW合约开发的学习资料。（假设你已经具备一些Rust开发经验）

建议在开始之前观看下[Delphi Digital]([Delphi Digital (@Delphi_Digital) / Twitter](https://twitter.com/delphi_digital))的工程师[larry]([larry.cosmos (@larry0x) / Twitter](https://twitter.com/larry0x))做的这个访谈节目👇，该节目虽然讲的是他发起的新项目CW-SDK，但也很好的介绍了本文章的所有内容，以及每一个技术所处的位置，综合性较强。

[ Understanding CosmWasm SDK with Larry Engineer - YouTube](https://www.youtube.com/watch?v=LQoBF5xr00c)

CW-SDK：用CW合约的形式实现Cosmos SDK，Github：[steak-enjoyers/cw-sdk](https://github.com/steak-enjoyers/cw-sdk)

### [AREA-52](https://area-52.io/)





