---
title: 使用 Visual Studio 管理逻辑应用 - Azure 逻辑应用 | Microsoft Docs
description: 使用 Visual Studio Cloud Explorer 管理逻辑应用和其他 Azure 资产
author: ecfan
manager: jeconnoc
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: ''
ms.service: logic-apps
ms.workload: logic-apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: mvc
ms.date: 03/15/2018
ms.author: estfan; LADocs
ms.openlocfilehash: b4d7f557923a67ae0c9fc513cd2b4fe7555241be
ms.sourcegitcommit: 6f6d073930203ec977f5c283358a19a2f39872af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35301110"
---
# <a name="manage-logic-apps-with-visual-studio"></a>使用 Visual Studio 管理逻辑应用

尽管可以在 <a href="https://portal.azure.com" target="_blank">Azure 门户</a>中创建、编辑、管理和部署逻辑应用，但在需要将逻辑应用添加到源代码管理、发布不同的版本，以及为不同的部署环境创建 [Azure 资源管理器](../azure-resource-manager/resource-group-overview.md)模板时，也可以使用 Visual Studio。 使用 Visual Studio Cloud Explorer 可以查找和管理逻辑应用以及其他 Azure 资源。 例如，可以打开、下载、编辑、运行、禁用和启用已在 Azure 门户中部署的逻辑应用，以及查看其运行历史记录。 如果你还不太熟悉如何在 Visual Studio 中处理 Azure 逻辑应用，请参阅[如何使用 Visual Studio 创建逻辑应用](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md)。

> [!IMPORTANT]
> 从 Visual Studio 部署或发布逻辑应用会覆盖该应用在 Azure 门户中的版本。 因此，若要在 Azure 门户进行更改并保存这些更改，请务必通过 Azure 门户[在 Visual Studio 中刷新逻辑应用](#refresh)，然后，便可以通过 Visual Studio 部署或发布该应用。

<a name="requirements"></a>

## <a name="prerequisites"></a>先决条件

* 如果没有 Azure 订阅，请<a href="https://azure.microsoft.com/free/" target="_blank">注册一个免费 Azure 帐户</a>。

* 下载并安装以下工具（如果没有）： 

  * <a href="https://www.visualstudio.com/downloads" target="_blank">Visual Studio 2017 或 Visual Studio 2015 - Community Edition 或更高版本</a>。 
  本快速入门使用免费的 Visual Studio Community 2017。

  * <a href="https://azure.microsoft.com/downloads/" target="_blank">Azure SDK（2.9.1 或更高版本）</a>和 <a href="https://github.com/Azure/azure-powershell#installation" target="_blank">Azure PowerShell</a>

  * <a href="https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551" target="_blank">适用于 Visual Studio 2017 的 Azure 逻辑应用工具</a>或 <a href="https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio" target="_blank">Visual Studio 2015 版</a> 
  
    可以直接从 Visual Studio Marketplace 下载并安装 Azure 逻辑应用工具，或了解<a href="https://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions" target="_blank">如何从 Visual Studio 内部安装此扩展</a>。 
    完成安装后，请务必重启 Visual Studio。

* 使用嵌入式逻辑应用设计器时访问 Web

  设计器需要通过 Internet 连接在 Azure 中创建资源，以及从逻辑应用中的连接器读取属性和数据。 
  例如，如果使用 Dynamics CRM Online 连接器，则设计器在 CRM 实例中检查可用的默认属性和自定义属性。

<a name="find-logic-apps-vs"></a>

## <a name="find-your-logic-apps"></a>查找逻辑应用

在 Visual Studio 中，可以使用 Cloud Explorer 来查找与 Azure 订阅关联的，以及在 Azure 门户中部署的所有逻辑应用。

1. 打开 Visual Studio。 在“视图”菜单中选择“Cloud Explorer”。

2. 在 Cloud Explorer 中选择“帐户管理”。 选择与逻辑应用关联的 Azure 订阅，然后选择“应用”。 例如：

   ![选择“帐户管理”](./media/manage-logic-apps-with-visual-studio/account-management-select-Azure-subscription.png)

2. 根据搜索依据是“资源组”还是“资源类型”执行以下步骤：

   * **资源组**：Cloud Explorer 会在你的 Azure 订阅下显示与该订阅关联的所有资源组。 
   展开包含你的逻辑应用的资源组，然后选择该逻辑应用。

   * **资源类型**：在 Azure 订阅下展开“逻辑应用”。 在 Cloud Explorer 显示与订阅关联的所有已部署逻辑应用后，请选择自己的逻辑应用。

<a name="open-designer"></a>

## <a name="open-in-visual-studio"></a>在 Visual Studio 中打开

在 Visual Studio 中，可以打开以前直接通过 Azure 门户或者使用 Visual Studio 作为 Azure 资源管理器项目创建和部署的逻辑应用。

1. 打开 Cloud Explorer 并找到自己的逻辑应用。 

2. 在逻辑应用的快捷菜单中，选择“使用逻辑应用编辑器打开”。

   此示例按资源类型演示逻辑应用，因此，你的逻辑应用会显示在“逻辑应用”部分下。

  ![从 Azure 门户打开部署的逻辑应用](./media/manage-logic-apps-with-visual-studio/open-logic-app-in-editor.png)

   逻辑应用在逻辑应用设计器中打开后，可以在设计器的底部选择“代码视图”，以便查看逻辑应用的基础定义结构。 
   若要为逻辑应用创建部署模板，请了解如何为该逻辑应用[下载 Azure 资源管理器模板](#download-logic-app)。 详细了解[资源管理器模板](../azure-resource-manager/resource-group-overview.md#template-deployment)。

<a name="download-logic-app"></a>

## <a name="download-from-azure"></a>从 Azure 下载

可以从 <a href="https://portal.azure.com" target="_blank">Azure 门户</a>下载逻辑应用，并将其保存为 [Azure 资源管理器](../azure-resource-manager/resource-group-overview.md)模板。 然后，可以在本地使用 Visual Studio 编辑模板，并根据不同的部署环境自定义逻辑应用。 下载逻辑应用会在[资源管理器模板](../azure-resource-manager/resource-group-overview.md#template-deployment)中将这些逻辑应用的定义（也使用 JavaScript 对象表示法 (JSON)）*参数化*。

1. 在 Visual Studio 中打开 Cloud Explorer，然后找到并选择要从 Azure 下载的逻辑应用。

2. 在该应用的快捷菜单中，选择“使用逻辑应用编辑器打开”。

   逻辑应用设计器随即打开并显示该逻辑应用。 
   若要查看逻辑应用的基础定义和结构，请在设计器的底部选择“代码视图”。 

3. 在设计器工具栏上选择“下载”。

   ![选择“下载”](./media/manage-logic-apps-with-visual-studio/download-logic-app.png)

4. 当系统提示输入位置时，请浏览到该位置，并在资源管理器模板中以 JSON (.json) 文件格式保存逻辑应用的定义。 

逻辑应用定义显示在资源管理器模板中的 `resources` 子节内。 现在，可以使用 Visual Studio 来编辑逻辑应用定义和资源管理器模板。 还可以将模板作为 Azure 资源管理器项目添加到 Visual Studio 解决方案中。 了解 [Visual Studio 中逻辑应用的资源管理器项目](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md)。 

<a name="refresh"></a>

## <a name="refresh-from-azure"></a>从 Azure 刷新

如果在 Azure 门户中编辑了逻辑应用并想要保存这些更改，请务必在 Visual Studio 中使用这些更改刷新该应用的版本。 

* 在 Visual Studio 中的逻辑应用设计器工具栏上，选择“刷新”。

  -或-

* 在 Visual Studio Cloud Explorer 中打开逻辑应用的快捷菜单，选择“刷新”。 

![使用更新内容刷新逻辑应用](./media/manage-logic-apps-with-visual-studio/refresh-logic-app.png)

## <a name="publish-logic-app-updates"></a>发布逻辑应用更新

准备好将逻辑应用更新从 Visual Studio 部署到 Azure 时，请在逻辑应用设计器工具栏上选择“发布”。

![发布更新的逻辑应用](./media/manage-logic-apps-with-visual-studio/publish-logic-app.png)

## <a name="manually-run-your-logic-app"></a>手动运行逻辑应用

可以通过 Visual Studio 手动触发 Azure 中部署的逻辑应用。 在逻辑应用设计器工具栏上，选择“运行触发器”。

![手动运行逻辑应用](./media/manage-logic-apps-with-visual-studio/manually-run-logic-app.png)

## <a name="review-run-history"></a>查看运行历史记录

若要检查逻辑应用运行的状态和诊断问题，可以在 Visual Studio 中查看这些运行的详细信息，例如输入和输出。

1. 在 Cloud Explorer 中打开逻辑应用的快捷菜单，选择“打开运行历史记录”。

   ![打开运行历史记录](./media/manage-logic-apps-with-visual-studio/view-run-history.png)

2. 若要查看特定运行的详细信息，请双击该运行。 例如：

   ![详细运行历史记录](./media/manage-logic-apps-with-visual-studio/view-run-history-details.png)
  
   > [!TIP]
   > 若要按属性将表排序，请选择该属性的列标题。 

3. 展开要查看其输入和输出的步骤。 例如：

   ![查看每个步骤的输入和输出](./media/manage-logic-apps-with-visual-studio/run-inputs-outputs.png)

## <a name="disable-or-enable-logic-app"></a>禁用或启用逻辑应用

如果不删除逻辑应用，可以在下一次满足触发条件时，阻止触发器激发。 禁用逻辑应用可以防止逻辑应用引擎创建和运行以后的逻辑应用工作流实例。
在 Cloud Explorer 中打开逻辑应用的快捷菜单，选择“禁用”。

![禁用逻辑应用](./media/manage-logic-apps-with-visual-studio/disable-logic-app.png)

准备好让逻辑应用恢复操作时，可以重新激活逻辑应用。 在 Cloud Explorer 中打开逻辑应用的快捷菜单，选择“启用”。

![启用逻辑应用](./media/manage-logic-apps-with-visual-studio/enable-logic-app.png)

## <a name="delete-your-logic-app"></a>删除逻辑应用

若要从 Azure 门户删除逻辑应用，请在 Cloud Explorer 中打开逻辑应用的快捷菜单，并选择“删除”。

![删除逻辑应用](./media/manage-logic-apps-with-visual-studio/delete-logic-app.png)

## <a name="next-steps"></a>后续步骤

本文已介绍如何使用 Visual Studio 管理部署的逻辑应用。 接下来，请了解如何自定义部署的逻辑应用定义：

> [!div class="nextstepaction"]
> [以 JSON 编写逻辑应用定义](../logic-apps/logic-apps-author-definitions.md)
