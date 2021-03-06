---
title: 教程：Azure Active Directory 与 NetSuite 集成 | Microsoft Docs
description: 了解如何在 Azure Active Directory 和 Netsuite 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2018
ms.author: jeedes
ms.openlocfilehash: 55ee7f6b496def5669160f5cfafed7bc6d7eab11
ms.sourcegitcommit: 16ddc345abd6e10a7a3714f12780958f60d339b6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36219364"
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a>教程：Azure Active Directory 与 NetSuite 集成

本教程介绍如何将 Netsuite 与 Azure Active Directory (Azure AD) 集成。

将 Netsuite 与 Azure AD 集成提供以下优势：

- 可在 Azure AD 中控制谁有权访问 Netsuite
- 可让用户使用其 Azure AD 帐户自动登录到 Netsuite（单一登录）
- 可以在一个中心位置（即 Azure 门户）管理帐户

如果要了解有关 SaaS 应用与 Azure AD 集成的更多详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](../manage-apps/what-is-single-sign-on.md)。

## <a name="prerequisites"></a>先决条件

若要配置 Azure AD 与 Netsuite 的集成，需要以下项：

- Azure AD 订阅
- 已启用 Netsuite 单一登录的订阅

> [!NOTE]
> 为了测试本教程中的步骤，我们不建议使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可以在[此处](https://azure.microsoft.com/pricing/free-trial/)获取一个月的试用版。

## <a name="scenario-description"></a>方案描述
在本教程中，将在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 Netsuite
2. 配置和测试 Azure AD 单一登录

## <a name="adding-netsuite-from-the-gallery"></a>从库中添加 Netsuite
要配置 Netsuite 与 Azure AD 的集成，需要从库中将 Netsuite 添加到托管 SaaS 应用列表。

若要从库中添加 Netsuite，请执行以下步骤：

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。 

    ![Active Directory][1]

2. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![应用程序][2]
    
3. 单击对话框顶部的“新建应用程序”按钮。

    ![应用程序][3]

4. 在“搜索”框中键入“Netsuite”。

    ![创建 Azure AD 测试用户](./media/netsuite-tutorial/tutorial_netsuite_search.png)

5. 在结果面板中，选择“Netsuite”，并单击“添加”按钮添加该应用程序。

    ![创建 Azure AD 测试用户](./media/netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录
本部分介绍基于一个名为“Britta Simon”的测试用户使用 Netsuite 配置和测试 Azure AD 单一登录。

为使单一登录能正常工作，Azure AD 需要知道 Netsuite 中与 Azure AD 用户对应的用户。 换句话说，需要建立 Azure AD 用户与 Netsuite 中相关用户之间的链接关系。

可通过将 Azure AD 中“用户名”的值指定为 Netsuite 中“用户名”的值来建立此链接关系。

若要配置和测试 Netsuite 的 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configuring-azure-ad-single-sign-on)** - 让用户使用此功能。
2. **[创建 Azure AD 测试用户](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
3. [创建 Netsuite 测试用户](#creating-a-netsuite-test-user) - 在 Netsuite 中创建 Britta Simon 的对应用户，并将其链接到用户的 Azure AD 身份。
4. **[分配 Azure AD 测试用户](#assigning-the-azure-ad-test-user)** - 让 Britta Simon 使用 Azure AD 单一登录。
5. **[测试单一登录](#testing-single-sign-on)** - 验证配置是否正常工作。

### <a name="configuring-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

本部分介绍如何在 Azure 门户中启用 Azure AD 单一登录并在 Netsuite 应用程序中配置单一登录。

若要配置 Netsuite 的 Azure AD 单一登录，请执行以下步骤：

1. 在 Azure 门户中，在“Netsuite”应用程序集成页上，单击“单一登录”。

    ![配置单一登录][4]

2. 在“单一登录”对话框中，选择“基于 SAML 的单一登录”作为“模式”以启用单一登录。
 
    ![配置单一登录](./media/netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. 在“Netsuite 域和 URL”部分，执行以下步骤：

    ![配置单一登录](./media/netsuite-tutorial/tutorial_netsuite_url.png)

    在“回复 URL”文本框中，使用以下模式键入 URL：`https://<tenant-name>.netsuite.com/saml2/acs`、`https://<tenant-name>.na1.netsuite.com/saml2/acs`、`https://<tenant-name>.na2.netsuite.com/saml2/acs`、`https://<tenant-name>.sandbox.netsuite.com/saml2/acs`、`https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs`、`https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`

    > [!NOTE] 
    > 这些不是实际值。 使用实际回复 URL 更新这些值。 若要获取这些值，请与 [Netsuite 支持团队](http://www.netsuite.com/portal/services/support.shtml)联系。
 
4. 在“SAML 签名证书”部分中，单击“元数据 XML”，并在计算机上保存 XML 文件。

    ![配置单一登录](./media/netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. 单击“保存”按钮。

    ![配置单一登录](./media/netsuite-tutorial/tutorial_general_400.png)

6. 在“Netsuite 配置”部分，单击“配置 Netsuite”，打开“配置登录”窗口。 从“快速参考”部分中复制“SAML 单一登录服务 URL”

    ![配置单一登录](./media/netsuite-tutorial/tutorial_netsuite_configure.png) 

7. 在浏览器中打开新选项卡，并以管理员的身分登录 Netsuite 公司站点。

8. 在页面顶部的工具栏上，单击“设置”，并单击“设置管理员”。

    ![配置单一登录](./media/netsuite-tutorial/ns-setup.png)

9. 从“设置任务”列表中，选择“集成”。

    ![配置单一登录](./media/netsuite-tutorial/ns-integration.png)

10. 在“管理身份验证”部分中，单击“SAML 单一登录”。

    ![配置单一登录](./media/netsuite-tutorial/ns-saml.png)

11. 在“SAML 设置”页上执行以下步骤：
   
    a. 从“配置登录”的“快速参考”部分复制“SAML 单一登录服务 URL”值，并将其粘贴到 Netsuite 中的“标识提供者登录页”字段。

    ![配置单一登录](./media/netsuite-tutorial/ns-saml-setup.png)
  
    b. 在 NetSuite 中，选择“主要身份验证方法”。

    c. 对于标有“SAMLV2 标识提供者元数据”的字段，请选择“上载 IDP 元数据文件”。 然后单击“浏览”，上传从 Azure 门户下载的元数据文件。

    ![配置单一登录](./media/netsuite-tutorial/ns-sso-setup.png)

    d. 单击“提交”。

12. 在 Azure AD 中，单击“查看和编辑所有其他用户属性”复选框，并添加属性。

    ![配置单一登录](./media/netsuite-tutorial/ns-attributes.png)

13. 在“属性名称”字段中，键入 `account`。 在“属性值”字段中，键入 NetSuite 帐户 ID。 此值是常量，会随帐户而改变。 下面提供了有关如何找出帐户 ID 的说明：

      ![配置单一登录](./media/netsuite-tutorial/ns-add-attribute.png)

    a. 在 Netsuite 的顶部导航菜单中单击“设置”。

    b. 单击左侧导航菜单中的“设置任务”部分，选择“集成”部分，并单击“Web 服务首选项”。

    c. 复制 NetSuite 帐户 ID 并将它粘贴到 Azure AD 中的“属性值”字段。

    ![配置单一登录](./media/netsuite-tutorial/ns-account-id.png)

14. 在用户能够单一登录到 NetSuite 之前，必须先在 NetSuite 中为他们分配适当的权限。 请按以下说明来分配这些权限。

    a. 在顶部导航菜单中单击“设置”，并单击“设置管理员”。
      
      ![配置单一登录](./media/netsuite-tutorial/ns-setup.png)

    b. 在左侧导航菜单中，选择“用户/角色”，并单击“管理角色”。
      
      ![配置单一登录](./media/netsuite-tutorial/ns-manage-roles.png)

    c. 单击“新建角色”。

    d. 键入新角色的“名称”。
      
      ![配置单一登录](./media/netsuite-tutorial/ns-new-role.png)

    e. 单击“ **保存**”。

    f. 在顶部菜单中，单击“权限”。 然后单击“设置”。
      
       ![配置单一登录](./media/netsuite-tutorial/ns-sso.png)

    g. 选择“设置 SAML 单一登录”，并单击“添加”。

    h. 单击“ **保存**”。

    i. 在顶部导航菜单中单击“设置”，并单击“设置管理员”。
      
       ![配置单一登录](./media/netsuite-tutorial/ns-setup.png)

    j. 在左侧导航菜单中，选择“用户/角色”，并单击“管理用户”。
      
       ![配置单一登录](./media/netsuite-tutorial/ns-manage-users.png)

    k. 选择一个测试用户。 然后单击“编辑”。
      
       ![配置单一登录](./media/netsuite-tutorial/ns-edit-user.png)

    l. 在“角色”对话框中，选择创建的角色，并单击“添加”。
      
       ![配置单一登录](./media/netsuite-tutorial/ns-add-role.png)

    m. 单击“ **保存**”。
    
### <a name="creating-an-azure-ad-test-user"></a>创建 Azure AD 测试用户
本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

![创建 Azure AD 用户][100]

**若要在 Azure AD 中创建测试用户，请执行以下步骤：**

1. 在 **Azure 门户**的左侧导航窗格中，单击“Azure Active Directory”图标。

    ![创建 Azure AD 测试用户](./media/netsuite-tutorial/create_aaduser_01.png) 

2.  若要显示用户列表，请转到“用户和组”，单击“所有用户”。
    
    ![创建 Azure AD 测试用户](./media/netsuite-tutorial/create_aaduser_02.png) 

3. 在对话框顶部，单击“添加”以打开“用户”对话框。
 
    ![创建 Azure AD 测试用户](./media/netsuite-tutorial/create_aaduser_03.png) 

4. 在“用户”对话框页上，执行以下步骤：
 
    ![创建 Azure AD 测试用户](./media/netsuite-tutorial/create_aaduser_04.png) 

    a. 在“名称”文本框中，键入 **BrittaSimon**。

    b. 在“用户名”文本框中，键入 BrittaSimon 的“电子邮件地址”。

    c. 选择“显示密码”并记下“密码”的值。

    d. 单击“创建”。 

### <a name="creating-a-netsuite-test-user"></a>创建 Netsuite 测试用户

本部分将在 Netsuite 中创建一个名为 Britta Simon 的用户。 Netsuite 支持默认启用的实时预配。
此部分不存在任何操作项。 尝试访问 Netsuite 时，如果 Netsuite 中没有用户，系统会创建一个新用户。


### <a name="assigning-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，通过授予 Britta Simon 访问 Netsuite 的权限，允许其使用 Azure 单一登录。

![分配用户][200] 

若要将 Britta Simon 分配到 Netsuite，请执行以下步骤：

1. 在 Azure 门户中打开应用程序视图，导航到目录视图，接着转到“企业应用程序”，并单击“所有应用程序”。

    ![分配用户][201] 

2. 在应用程序列表中，选择“Netsuite”。

    ![配置单一登录](./media/netsuite-tutorial/tutorial_netsuite_app.png) 

3. 在左侧菜单中，单击“用户和组”。

    ![分配用户][202] 

4. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![分配用户][203]

5. 在“用户和组”对话框的“用户”列表中，选择“Britta Simon”。

6. 在“用户和组”对话框中单击“选择”按钮。

7. 在“添加分配”对话框中单击“分配”按钮。
    
### <a name="testing-single-sign-on"></a>测试单一登录

在本部分中，使用访问面板测试 Azure AD 单一登录配置。

若要测试单一登录设置，请打开“访问面板”（网址为 [https://myapps.microsoft.com](https://myapps.microsoft.com/)），登录测试帐户，并单击“Netsuite”。

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](tutorial-list.md)
* [什么是使用 Azure Active Directory 的应用程序访问和单一登录？](../manage-apps/what-is-single-sign-on.md)
* [配置用户预配](netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/netsuite-tutorial/tutorial_general_01.png
[2]: ./media/netsuite-tutorial/tutorial_general_02.png
[3]: ./media/netsuite-tutorial/tutorial_general_03.png
[4]: ./media/netsuite-tutorial/tutorial_general_04.png

[100]: ./media/netsuite-tutorial/tutorial_general_100.png

[200]: ./media/netsuite-tutorial/tutorial_general_200.png
[201]: ./media/netsuite-tutorial/tutorial_general_201.png
[202]: ./media/netsuite-tutorial/tutorial_general_202.png
[203]: ./media/netsuite-tutorial/tutorial_general_203.png

