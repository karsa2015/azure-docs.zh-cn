---
title: Azure 自动化中的子 Runbook
description: 介绍从 Azure 自动化中的一个 Runbook 启动另一个 Runbook 并在它们之间共享信息的不同方法。
services: automation
ms.service: automation
ms.component: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 05/04/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 0511c2bf7eed15f997f8444c945afb18179bbc63
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2018
ms.locfileid: "34193996"
---
# <a name="child-runbooks-in-azure-automation"></a>Azure 自动化中的子 Runbook

在 Azure 自动化中，最佳实践之一是编写可重用、模块化且提供可由其他 Runbook 使用的离散功能的 Runbook。 父 Runbook 通常会调用一个或多个子 Runbook 来执行所需的功能。 可通过两种方法调用子 Runbook，每种方法都有明显不同的差异，应该了解这些差异，以确定哪种方法最适合方案。

## <a name="invoking-a-child-runbook-using-inline-execution"></a>使用内联执行调用子 Runbook 

若要从另一个 Runbook 调用某个内嵌 Runbook，请使用被调用 Runbook 的名称并提供其参数值，就像使用活动或 cmdlet 时一样。  同一自动化帐户中的所有 Runbook 可按此方式相互使用。 父 Runbook 将等待子 Runbook 完成，然后转移到下一行，并直接向父级返回任何输出。

在调用某个内联 Runbook 时，它会在与父 Runbook 所在的同一个作业中运行。 父 Runbook 运行的子 Runbook 的作业历史记录中不会提供相应的指示。 子 Runbook 发生的任何异常和任何流输出将与父级关联。 这减少了作业数，简化了作业的跟踪，并便于排查自从子 Runbook 引发任何异常以及将其流输出与父作业关联以来发生的问题。

发布某个 Runbook 时，必须事先发布它所调用的任何子 Runbook。 这是因为，在编译 Runbook 时，Azure 自动化会生成与任何子 Runbook 的关联。 如果未进行这种关联，父 Runbook 看似发布正常，但在启动时会生成异常。 如果发生这种情况，可以重新发布父 Runbook，以正确引用子 Runbook。 如果由于已创建关联而更改了任何子 Runbook，则不需重新发布父 Runbook。

内联调用的子 Runbook 的参数可以是任意数据类型（包括复杂对象），并且不会进行 [JSON 序列化](automation-starting-a-runbook.md#runbook-parameters)，因为使用 Azure 门户或 Start-AzureRmAutomationRunbook cmdlet 启动 Runbook 时会进行这种序列化。

### <a name="runbook-types"></a>Runbook 类型

哪些类型可以互相调用：

* [PowerShell Runbook](automation-runbook-types.md#powershell-runbooks) 和[图形 Runbook](automation-runbook-types.md#graphical-runbooks) 可以互相内联调用（两者都基于 PowerShell）。
* [PowerShell 工作流 Runbook](automation-runbook-types.md#powershell-workflow-runbooks) 和图形 PowerShell 工作流 Runbook 可以互相内联调用（两者都基于 PowerShell 工作流）
* PowerShell 类型和 PowerShell 工作流类型不能互相内联调用，并且必须使用 Start-AzureRmAutomationRunbook。

发布顺序何时重要：

* Runbook 的发布顺序仅对于 PowerShell 工作流和图形 PowerShell 工作流 Runbook 重要。

在通过内联执行调用图形或 PowerShell 工作流子 Runbook 时，只需使用 Runbook 的名称。  调用 PowerShell 子 runbook 时，必须在其名称前面添加 *.\\*，以指定脚本位于本地目录中。 

### <a name="example"></a>示例

下面的示例将调用一个测试子 Runbook，该 Runbook 接受三个参数：一个复杂对象、一个整数和一个布尔值。 该子 Runbook 的输出将分配到某个变量。  在本示例中，子 Runbook 属于 PowerShell 工作流 Runbook

```azurepowershell-interactive
$vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
$output = PSWF-ChildRunbook –VM $vm –RepeatCount 2 –Restart $true
```

下面是使用 PowerShell Runbook 作为子项的同一示例。

```azurepowershell-interactive
$vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
$output = .\PS-ChildRunbook.ps1 –VM $vm –RepeatCount 2 –Restart $true
```

## <a name="starting-a-child-runbook-using-cmdlet"></a>使用 cmdlet 启动子 Runbook

可以根据[使用 Windows PowerShell 启动 Runbook](automation-starting-a-runbook.md#starting-a-runbook-with-windows-powershell) 中所述，使用 [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) cmdlet 来启动 Runbook。 使用此 cmdlet 的模式有两种。  在第一个模式中，cmdlet 会在子 Runbook 的子作业创建时立即返回作业 ID。  在第二个模式（通过指定 **-wait** 参数启用）中，cmdlet 会等待子作业完成，并且会返回子 Runbook 的输出。

使用 cmdlet 启动的子 Runbook 的作业会在父 Runbook 的某个独立作业中运行。 这会导致比调用内联 Runbook 更多的作业，并使这些作业更难以跟踪。不过，父级可以异步启动多个子 Runbook，而无需等待每个子 Runbook 完成。 对于调用内嵌子 Runbook 的同一种并行执行，父 Runbook 需要使用[并行关键字](automation-powershell-workflow.md#parallel-processing)。

由于时间原因，子 Runbook 的输出不会可靠地返回到父 Runbook。 另外，某些变量（如 $VerbosePreference、$WarningPreference 等）可能不会传播到子 Runbook。 为避免这些问题，可以使用带 `-Wait` 开关的 `Start-AzureRmAutomationRunbook` cmdlet 将子 Runbook 作为单独的自动化作业调用。 这会阻止父 Runbook，直到子 Runbook 完成。

如果不希望父 Runbook 在等待时被阻止，则可以使用不带 `-Wait` 开关的 `Start-AzureRmAutomationRunbook` cmdlet 调用子 Runbook。 然后，需要使用 `Get-AzureRmAutomationJob` 等待作业完成，然后使用 `Get-AzureRmAutomationJobOutput` 和 `Get-AzureRmAutomationJobOutputRecord` 来检索结果。

使用 cmdlet 启动的子 Runbook 的参数以哈希表形式提供，如 [Runbook 参数](automation-starting-a-runbook.md#runbook-parameters)中所述。 只能使用简单数据类型。 如果 Runbook 的参数使用复杂数据类型，则必须内联调用该 Runbook。

### <a name="example"></a>示例

以下示例将启动一个包含参数的子 Runbook，然后使用 Start-AzureRmAutomationRunbook -wait 参数等待其完成。 完成后，将从子 Runbook 收集其输出。

```azurepowershell-interactive
$params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true}
$joboutput = Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-ChildRunbook" -ResourceGroupName "LabRG" –Parameters $params –wait
```

## <a name="comparison-of-methods-for-calling-a-child-runbook"></a>子 Runbook 调用方法的比较
下表汇总了从一个 Runbook 调用另一个 Runbook 的两种方法的差异。

|  | 内联 | Cmdlet |
|:--- |:--- |:--- |
| 作业 |子 Runbook 在父级所在的同一个作业中运行。 |为子 Runbook 创建单独的作业。 |
| 执行 |父 Runbook 等待子 Runbook 完成，然后再继续。 |父 Runbook 会在子 Runbook 启动后立刻继续运行，或父 Runbook 会等待子作业完成。 |
| 输出 |父 Runbook 可以直接从子 Runbook 获取输出。 |父 Runbook 必须检索子 Runbook 作业的输出，或父 Runbook 可以直接从子 Runbook 获取输出。 |
| parameters |子 Runbook 参数的值需单独指定，并且可以使用任意数据类型。 |子 Runbook 参数值必须组合成单个哈希表，并且只能包含简单数据类型、数组和利用 JSON 序列化的对象数据类型。 |
| 自动化帐户 |父 Runbook 只能使用同一自动化帐户中的子 Runbook。 |父 Runbook 可以使用同一 Azure 订阅甚至（已连接的）不同订阅中的任何自动化帐户内的子 Runbook。 |
| 发布 |在发布父 Runbook 之前必须先发布子 Runbook。 |必须在启动父 Runbook 前的任意时间发布子 Runbook。 |

## <a name="next-steps"></a>后续步骤

* [在 Azure 自动化中启动 Runbook](automation-starting-a-runbook.md)
* [Azure 自动化中的 Runbook 输出和消息](automation-runbook-output-and-messages.md)
