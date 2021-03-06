---
title: 在 Azure AD 中创建用户的组 |Microsoft Docs
description: 如何在 Azure Active Directory 中创建组并向该组添加成员
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: fundamentals
ms.topic: quickstart
ms.date: 08/04/2017
ms.author: lizross
ms.reviewer: krbain
ms.custom: it-pro
ms.openlocfilehash: 3c71c9c49413045e3a730c10e90ea3c12648b4cb
ms.sourcegitcommit: 0b4da003fc0063c6232f795d6b67fa8101695b61
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37857715"
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a>在 Azure Active Directory 中创建组并添加成员
> [!div class="op_single_selector"]
> * [Azure 门户](active-directory-groups-create-azure-portal.md)
> * [PowerShell](../users-groups-roles/groups-settings-v2-cmdlets.md)

本文介绍如何在 Azure Active Directory 中创建和填充新组。 使用组来执行管理任务，例如一次向多个用户或设备分配许可证或权限。

## <a name="how-do-i-create-a-group"></a>如何创建组？
1. 使用目录全局管理员的帐户登录到 [Azure 门户](https://portal.azure.com)。
2. 选择“所有服务”，在文本框中输入“用户和组”，并选择 **Enter**。

   ![打开“用户管理”](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. 在“用户和组”边栏选项卡中，选择“所有组”。

   ![打开“组”边栏选项卡](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. 在“用户和组 - 所有组”边栏选项卡中，选择“添加”命令。

   ![选择“添加”命令](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. 在“组”边栏选项卡中，为组添加名称和描述。
6. 要选择要添加到组的成员，请在“成员身份类型”框中选择“已分配”，并选择“成员”。 有关如何动态管理组的成员身份的详细信息，请参阅[使用属性创建组成员身份的高级规则](../users-groups-roles/groups-dynamic-membership.md)。

   ![选择要添加的成员](./media/active-directory-groups-create-azure-portal/select-members.png)
7. 在“成员”边栏选项卡中，选择一个或多个要添加到组的用户或设备，然后选择边栏选项卡底部的“选择”按钮以将它们添加到组。 “用户”框会通过将输入内容与用户或设备名称的任何部分进行匹配来筛选显示内容。 该框中不允许使用任何通配符。
8. 完成向组添加成员后，请在“组”边栏选项卡中选择“创建”。    

   ![创建组确认](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a>后续步骤
这些文章提供了有关 Azure Active Directory 的更多信息。

* [查看现有组](active-directory-groups-view-azure-portal.md)
* [管理组的设置](active-directory-groups-settings-azure-portal.md)
* [管理组的成员](active-directory-groups-members-azure-portal.md)
* [管理组的成员身份](active-directory-groups-membership-azure-portal.md)
* [管理组中用户的动态规则](../users-groups-roles/groups-dynamic-membership.md)
