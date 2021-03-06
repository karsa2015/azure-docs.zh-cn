---
title: Azure Monitor 中的指标概述
description: 了解如何在 Azure 中自定义监视图表。
author: rboucher
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 06/06/2017
ms.author: robb
ms.component: metrics
ms.openlocfilehash: 878ba004e7572ad78f574c15fd76c8868b281117
ms.sourcegitcommit: 1b8665f1fff36a13af0cbc4c399c16f62e9884f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35262250"
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Microsoft Azure 中的度量值概述
所有 Azure 服务都会跟踪使你可以监视你服务的运行状况、性能、可用性和使用情况的关键指标。 可以在 Azure 门户中查看这些度量值，也可以使用 [REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx) 或 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) 以编程方式访问完整的度量值集。

对于某些服务，可能需要打开诊断以便查看任何指标。 对于其他服务（如虚拟机），会获得基本指标集，但需要启用完整高频率指标集。 有关详细信息，请参阅[启用监视和诊断](insights-how-to-use-diagnostics.md)。

## <a name="using-monitoring-charts"></a>使用监视图表
可以在所选的任何时间段内绘制任何指标的图表。

1. 在 [Azure 门户](https://portal.azure.com/)中，单击“浏览”，并单击要监视的资源。
2. “监视”部分包含每个 Azure 资源的最重要度量值。 例如，Web 应用具有“请求和错误”，而虚拟机具有“CPU 百分比”和“磁盘读写”：![监视可重用功能区](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)
3. 单击任何图表都会显示“度量值”边栏选项卡。 在该边栏选项卡中，除了该图之外还有一个表，其中显示指标（例如在所选时间范围内的平均值、最小值和最大值）的聚合。 下面是资源的警报规则。
    ![度量值边栏选项卡](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)
4. 若要自定义显示的折线图，请单击图表上的“编辑”按钮，或单机度量值边栏选项卡上的“编辑图表”命令。
5. 在“编辑查询”边栏选项卡上，可以执行三个操作：
   
   * 更改时间范围
   * 在条形图与折线图之间切换外观
   * 选择不同的度量值![编辑查询](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)
6. 更改时间范围十分轻松，只需选择不同的范围（例如“前一个小时”），并单击边栏选项卡底部的“保存”即可。 还可选择“自定义”，由此选择过去两周内的任何时间段。 例如，可以查看整个两周，或仅仅是昨天的 1 小时。 在文本框中键入一个不同的小时即可。
    ![自定义时间范围](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)
7. 在时间范围的下面，可以选择要在图表上显示的任意数目的度量值。
8. 单击“保存”时，会针对该特定资源保存更改。 例如，如果有两个虚拟机，并且对其中一个更改了图表，则不会影响另一个。

## <a name="creating-side-by-side-charts"></a>创建并排图表
借助门户中功能强大的自定义，可以添加所需任何数量的图表。

1. 在边栏选项卡顶部的“...”菜单中，单击“添加磁贴”：  
    ![添加菜单](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)
2. 然后可从屏幕右侧的“库”中选择图表：![库](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)
3. 如果看不到所需度量值，则始终可以添加一个预设度量值，并“编辑”图表以显示所需度量值。

## <a name="monitoring-usage-quotas"></a>监视使用配额
大多数指标都会显示随时间推移的趋势，但某些数据（如使用配额）是具有阈值的时间点信息。

还可以在具有配额的资源的边栏选项卡上查看使用配额：

![使用情况](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

与度量值一样，可使用 [REST API](https://msdn.microsoft.com/library/azure/dn931963.aspx) 或 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) 按编程方式访问完整使用配额集。

## <a name="next-steps"></a>后续步骤
* 每当度量值超过阈值时[接收警报通知](insights-receive-alert-notifications.md)。
* [启用监视和诊断](insights-how-to-use-diagnostics.md)以收集有关服务的详细高频率指标。
* [自动缩放实例计数](insights-how-to-scale.md)确保服务可用且响应迅速。
* 要确切了解代码在云中的执行情况时[监视应用程序性能](../application-insights/app-insights-azure-web-apps.md)。
* 若要获取有关访问网页的浏览器的客户端分析，请使用[适用于 JavaScript 应用和网页的 Application Insights](../application-insights/app-insights-web-track-usage.md)。
* 使用 Application Insights [监视任何网页的可用性和响应能力](../application-insights/app-insights-monitor-web-app-availability.md)，以便可以在页面出现故障时及时发现。

