---
title: 了解 Azure Service Fabric 术语 | Microsoft Docs
description: Service Fabric 的术语概述。 讨论本文档其余部分所用的重要术语概念和术语。
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: chackdan;subramar
ms.assetid: 3a970679-e19e-43b3-9be8-71773f307c57
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/26/2018
ms.author: ryanwi
ms.openlocfilehash: e3da081f9b327031d6d1e0afd2f2fb52383bf933
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2018
ms.locfileid: "34212062"
---
# <a name="service-fabric-terminology-overview"></a>Service Fabric 术语概述
Azure Service Fabric 是一种分布式系统平台，适用于打包、部署和管理可缩放的可靠微服务。 本文详细介绍 Service Fabric 所使用的术语，帮助了解文档中使用的术语。

以下 Microsoft Virtual Academy 视频中还讨论了本部分列出的概念：<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">核心概念</a>、<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965">设计时概念</a>和<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">运行时概念</a>。

## <a name="infrastructure-concepts"></a>基础结构概念
**群集**：一组通过网络连接在一起的虚拟机或物理计算机，微服务会在其中部署和管理。  群集可以扩展到成千上万台计算机。

节点：属于群集一部分的计算机或 VM 称为节点。 需为每个节点分配节点名称（字符串）。 节点具有各种特征，如放置属性。 每个计算机或 VM 都有一个自动启动 Windows 服务 `FabricHost.exe`，此服务在引导时开始运行，并启动两个可执行文件：`Fabric.exe` 和 `FabricGateway.exe`。 这两个可执行文件构成了节点。 在测试方案中，可以通过运行 `Fabric.exe` 和 `FabricGateway.exe` 的多个实例，在单台计算机或 VM 上托管多个节点。

## <a name="application-concepts"></a>应用程序概念
应用程序类型：分配给服务类型集合的名称/版本。 在 `ApplicationManifest.xml` 文件中定义并嵌入到应用程序包目录。 然后将目录复制到 Service Fabric 群集的映像存储。 然后，可以基于此应用程序类型，在群集内创建命名的应用程序。

有关详细信息，请阅读[应用程序模型](service-fabric-application-model.md)一文。

应用程序包：一个磁盘目录，其中包含应用程序类型的 `ApplicationManifest.xml` 文件。 引用构成应用程序类型的每个服务类型的服务包。 应用程序包目录中的文件将复制到 Service Fabric 群集的映像存储。 例如，电子邮件应用程序类型的应用程序包可能包含对队列服务包、前端服务包和数据库服务包的引用。

命名应用程序：将应用程序包复制到映像存储后，在群集中创建应用程序实例。 当你指定应用程序包的应用程序类型时，通过使用其名称或版本来创建一个实例。 将为每个应用程序类型实例分配一个类似如下的统一资源标识符 (URI) 名称：`"fabric:/MyNamedApp"`。 在群集中，可以从单个应用程序类型创建多个命名应用程序。 还可以从不同的应用程序类型创建命名应用程序。 可单独管理每个命名应用程序并设置其版本。      

服务类型：分配给服务的代码包、数据包、配置包的名称/版本。 服务类型在 `ServiceManifest.xml` 文件中定义，并嵌入到服务包目录中。 然后，服务包目录由应用程序包的 `ApplicationManifest.xml` 文件引用。 在群集中创建命名应用程序后，可以从应用程序类型的服务类型之一创建命名服务。 服务类型的 `ServiceManifest.xml` 文件描述该服务。

有关详细信息，请阅读[应用程序模型](service-fabric-application-model.md)一文。

有两种类型的服务：

* 无状态：服务的持久状态存储在 Azure 存储、Azure SQL 数据库、Azure Cosmos DB 等外部存储服务中时，请使用无状态服务。 当服务没有永久性存储时，请使用无状态服务。 以计算器服务为例，首先要将值传递给该服务，然后服务使用这些值执行计算并返回结果。
* 有状态：如果要让 Service Fabric 通过其 Reliable Collections 或 Reliable Actors 编程模型管理服务状态，请使用有状态服务。 创建命名服务时，请指定要将状态分布于其中的分区数量，以实现伸缩性。 此外，指定跨节点复制状态的次数，以实现可靠性。 每个命名服务都有一个主副本和多个辅助副本。 在写入主要副本时修改命名服务的状态。 然后，Service Fabric 会将此状态复制到所有次要副本以使状态保持同步。当主要副本失败时，Service Fabric 会自动检测到此状态，并将现有的次要副本升级为主要副本。 然后，Service Fabric 会创建新的次要副本。  

副本或实例是指已部署或运行中的服务的代码（和有状态服务的状态）。 请参阅[副本和实例](service-fabric-concepts-replica-lifecycle.md)。

重新配置是指服务副本集中任何更改的过程。 请参阅[重新配置](service-fabric-concepts-reconfiguration.md)。

服务包：一个磁盘目录，其中包含服务类型的 `ServiceManifest.xml` 文件。 此文件引用服务类型的代码、静态数据和配置包。 应用程序类型的 `ApplicationManifest.xml` 文件引用服务包目录中的文件。 例如，服务包可能引用构成数据库服务的代码、静态数据和配置包。

命名服务：创建命名应用程序后，可以在群集中创建它的其中一个服务类型的实例。 通过使用其名称/版本指定服务类型。 需为每个服务类型实例分配一个 URI 名称，该名称归并到实例的命名应用程序的 URI 之下。 例如，如果在命名应用程序“MyNamedApp”中创建命名服务“MyDatabase”，则 URI 将类似于：`"fabric:/MyNamedApp/MyDatabase"`。 在一个命名应用程序中可以创建多个命名服务。 每个命名服务可以有自身的分区方案和实例或副本计数。

代码包：一个磁盘目录，其中包含服务类型的可执行文件，通常是 EXE/DLL 文件。 服务类型的 `ServiceManifest.xml` 文件引用代码包目录中的文件。 创建命名服务后，会将代码包复制到选定来运行命名服务的一个或多个节点。 然后代码将开始运行。 有两种类型的代码包可执行文件：

* **来宾可执行文件**：在主机操作系统（Windows 或 Linux）上按原样运行的可执行文件。 这些可执行文件不会链接到或引用任何 Service Fabric 运行时文件，因此不会使用任何 Service Fabric 编程模型。 这些可执行文件不能使用某些 Service Fabric 功能，例如终结点发现的命名服务。 来宾可执行文件无法报告特定于每个服务实例的负载指标。
* 服务主机可执行文件：通过链接到 Service Fabric 运行时文件、启用 Service Fabric 功能来使用 Service Fabric 编程模型的可执行文件。 例如，命名服务实例可在 Service Fabric 命名服务中注册终结点，还可以报告负载指标。      

数据包：一个磁盘目录，其中包含服务类型的静态只读数据文件，通常是照片、音频和视频文件。 服务类型的 `ServiceManifest.xml` 文件引用数据包目录中的文件。 创建命名服务后，会将数据包复制到选定来运行命名服务的一个或多个节点。 代码开始运行，现在即可访问数据文件。

配置包：一个磁盘目录，其中包含服务类型的静态只读配置文件，通常是文本文件。 服务类型的 `ServiceManifest.xml` 文件引用配置包目录中的文件。 创建命名服务后，会将配置包中的文件复制到选定运行命名服务的一个或多个节点。 然后，代码开始运行，现在即可访问配置文件。

**容器**：默认情况下，Service Fabric 以进程形式部署和激活这些服务。 Service Fabric 还可以部署容器映像中的服务。 容器是在应用程序中将基础操作系统虚拟化的一种虚拟化技术。 应用程序及其运行时、依赖项和系统库在一个容器内运行。 容器对自己的操作系统构造隔离视图具有全部专有访问权限。 Service Fabric 支持 Linux 上的 Docker 容器和 Windows Server 容器。 有关详细信息，请参阅 [Service Fabric 和容器](service-fabric-containers-overview.md)。

分区方案：创建命名服务时，需要指定一个分区方案。 包含大量状态的服务跨分区拆分数据，将状态分散在群集的节点上。 通过在分区之间拆分数据，可以扩展命名服务的状态。 在分区中，无状态命名服务具有实例，而有状态命名服务具有副本。 通常，无状态命名服务只有一个分区，因为它们没有内部状态。 分区实例提供可用性。 如果一个实例失败，其他实例可继续正常运行，然后 Service Fabric 将创建新的实例。 有状态命名服务在副本中保持其状态，每个分区都有自身的副本集，以便状态保持同步。如果某个副本失败，Service Fabric 将从现有副本创建新副本。

有关详细信息，请阅读 [Service Fabric Reliable Services 分区](service-fabric-concepts-partitioning.md)一文。

## <a name="system-services"></a>系统服务
系统在每个群集中创建了一些系统服务，用于提供 Service Fabric 的平台功能。

命名服务：每个 Service Fabric 群集均有一个命名服务，该服务将服务名称解析到群集中的某个位置。 使用类似于管理群集的 Internet 域名系统 (DNS) 的方式管理服务名称和属性。 客户端可以使用命名服务安全地与群集中的任何节点进行通信，以解析服务名称及其位置。 应用程序在群集内移动。 例如，原因可以是故障、资源平衡或重设群集大小。 可开发解析当前网络位置的服务和客户端。 客户端会获得实际计算机 IP 地址及其当前运行位置所在的端口。

有关使用搭配命名服务运行的客户端与服务通信 API 的详细信息，请阅读[与服务通信](service-fabric-connect-and-communicate-with-services.md)。

映像存储服务：每个 Service Fabric 群集都有一个映像存储服务，其中保存已部署且版本化的应用程序包。 将应用程序包复制到映像存储，并注册该应用程序包内包含的应用程序类型。 预配应用程序类型后，根据它创建命名应用程序。 在删除某个应用程序类型的所有命名应用程序之后，可以从映像存储服务中注销该应用程序类型。

有关映像存储服务的详细信息，请参阅[了解 ImageStoreConnectionString 设置](service-fabric-image-store-connection-string.md)。

有关将应用程序部署到映像存储服务的详细信息，请阅读[部署应用程序](service-fabric-deploy-remove-applications.md)一文。

**故障转移管理器服务**：每个 Service Fabric 群集都具有一个故障转移管理器服务，负责执行以下操作：
   - 执行与服务的高可用性和一致性相关的功能。
   - 协调应用程序和群集升级。
   - 与其他系统组件交互。

**修复管理器服务**：这是一项可选的系统服务，可在集群上实现自动、透明、安全的修复操作。 修复管理器可用于：
   - 在[白银和黄金持久性](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) Azure Service Fabric 集群上执行 Azure 维护修复。
   - 实施面向[修补业务流程应用](service-fabric-patch-orchestration-application.md)的修复操作

## <a name="built-in-programming-models"></a>内置编程模型
有一些 .NET Framework 和 Java 编程模型可用于生成 Service Fabric 服务：

**Reliable Services**：用于构建无状态和有状态服务的 API。 有状态服务将其状态存储在 Reliable Collections（例如字典或队列）中。 也可插入各种通信堆栈，如 Web API 和 Windows Communication Foundation (WCF)。

**Reliable Actors**：用于通过虚拟执行组件编程模型构建无状态和有状态对象的 API。 如果有大量的独立计算或状态单位，此模型可能十分有用。 此模型使用基于轮次的线程模型，因此最好避免使用向外调用其他执行组件或服务的代码，原因是只有在单个执行组件的所有出站请求都已完成后，该执行组件才能处理其他传入请求。

还可以在 Service Fabric 上运行现有应用程序：

**容器**：Service Fabric 支持在 Linux 上部署 Docker 容器，在 Windows Server 2016 上部署 Windows Server 容器，同时支持 Hyper-V 隔离模式。 在 Service Fabric [应用程序模型](service-fabric-application-model.md)中，容器表示放置多个服务副本的应用程序主机。 Service Fabric 可运行任何容器，该方案类似于来宾可执行的方案，可在容器内打包现有应用程序。 此外，也可[在容器内运行 Service Fabric 服务](service-fabric-services-inside-containers.md)。

**来宾可执行文件**：可在 Azure Service Fabric 中运行任何类型的代码（如 Node.js、Java 或 C++）作为服务。 Service Fabric 将这些类型的服务称为来宾可执行文件，视其为无状态服务。 在 Service Fabric 群集中运行来宾可执行文件的优点包括高可用性、运行状况监视、应用程序生命周期管理、高密度和可发现性。

有关详细信息，请阅读[为服务选择编程模型](service-fabric-choose-framework.md)一文。

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>后续步骤
了解有关 Service Fabric 的详细信息：

* [Service Fabric 概述](service-fabric-overview.md)
* [为什么通过微服务的方法构建应用程序？](service-fabric-overview-microservices.md)
* [应用程序方案](service-fabric-application-scenarios.md)


