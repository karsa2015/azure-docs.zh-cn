---
title: "排查 Linux VM 分配失败 | Microsoft Docs"
description: "排查在 Azure 中创建、重新启动 Linux VM 或调整其大小时发生的分配失败"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resourece-manager,azure-service-management
ms.assetid: 1ef41144-6dd6-4a56-b180-9d8b3d05eae7
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cjiang
translationtype: Human Translation
ms.sourcegitcommit: 5919c477502767a32c535ace4ae4e9dffae4f44b
ms.openlocfilehash: d4520768a13de519fcc3f8778d2b87caa667b654


---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a>排查在 Azure 中创建、重新启动 Linux VM 或调整其大小时发生的分配失败
创建 VM、重新启动已停止（解除分配）的 VM 和重设 VM 大小时，Microsoft Azure 会为你的订阅分配计算资源。 执行这些操作时，即使尚未达到 Azure 订阅限制，也可能偶尔发生错误。 本文说明一些常见分配故障的原因，并建议可能的补救方法。 规划服务的部署时，本信息可能也有用。 还可以[排查在 Azure 中创建、重新启动 Windows VM 或调整其大小时发生的分配失败](virtual-machines-windows-allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

[!INCLUDE [virtual-machines-common-allocation-failure](../../includes/virtual-machines-common-allocation-failure.md)]




<!--HONumber=Nov16_HO3-->

