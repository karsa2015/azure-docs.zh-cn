---
title: 连接到 FTP 服务器 - Azure 逻辑应用 | Microsoft Docs
description: 使用 Azure 逻辑应用创建、监视和管理 FTP 服务器上的文件
author: ecfan
manager: jeconnoc
ms.author: estfan
ms.date: 07/22/2016
ms.topic: article
ms.service: logic-apps
services: logic-apps
ms.reviewer: klam, LADocs
ms.suite: integration
tags: connectors
ms.openlocfilehash: 983e8f84e6e44bc9e5de5f4e7fff361b92b316c9
ms.sourcegitcommit: 6f6d073930203ec977f5c283358a19a2f39872af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35295687"
---
# <a name="get-started-with-the-ftp-connector"></a>FTP 连接器入门
使用 FTP 连接器在 FTP 服务器上监视、管理和创建文件。 

若要使用[“任何连接器”](apis-list.md)，首先需要创建逻辑应用。 可通过[“立即创建逻辑应用”](../logic-apps/quickstart-create-first-logic-app-workflow.md)开始操作。

## <a name="connect-to-ftp"></a>连接到 FTP
与服务创建*连接*后，逻辑应用才能访问服务。 [连接](connectors-overview.md)提供逻辑应用和其他服务之间的连接性。  

### <a name="create-a-connection-to-ftp"></a>创建到 FTP 的连接
> [!INCLUDE [Steps to create a connection to FTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a>使用 FTP 触发器
触发器是用于启动在逻辑应用中定义的工作流的事件。 [了解有关触发器的详细信息](../logic-apps/logic-apps-overview.md#logic-app-concepts)。  

> [!IMPORTANT]
> FTP 连接器需要可从 Internet 访问并配置为在 PASSIVE 模式下运行的 FTP 服务器。 此外，FTP 连接器**与隐式 FTPS (FTP over SSL) 不兼容**。 FTP 连接器仅支持显式 FTPS (FTP over SSL)。  
> 
> 

在此示例中，我将演示如何使用“FTP - 添加或修改文件时”触发器，在 FTP 服务器上添加或修改文件时启动逻辑应用工作流。 在企业示例中，可以使用此触发器监视 TFP 文件夹中表示客户订单的新文件。  然后可以使用 FTP 连接器操作（如**获取文件内容**）来获取订单内容，以便进行进一步处理并将其存储到订单数据库中。

1. 在逻辑应用设计器上的搜索框中输入 *ftp*，并选择“FTP - 添加或修改文件时”触发器。   
   ![FTP 触发器图 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)  
   “添加或修改文件时”控件打开  
   ![FTP 触发器图 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)  
2. 选择位于控件右侧的“...”。 这会打开文件夹选取器控件  
   ![FTP 触发器图 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)  
3. 选择“>”（向右箭头），并通过浏览查找要监视新文件或已修改文件的文件夹。 选择该文件夹，注意文件夹现在显示在“文件夹”控件中。  
   ![FTP 触发器图 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)   

现在，逻辑应用中已经配置了一个触发器，当在特定 FTP 文件夹中修改或创建文件时，该触发器就会开始运行工作流中的其他触发器和操作。 

> [!NOTE]
> 若要使逻辑应用正常工作，必须包含至少一个触发器和一个操作。 按照下一部分中的步骤添加操作。  
> 
> 

## <a name="use-a-ftp-action"></a>使用 FTP 操作
操作是指在逻辑应用中定义的由工作流执行的操作。 [了解有关操作的详细信息](../logic-apps/logic-apps-overview.md#logic-app-concepts)。  

现已添加触发器，按照以下步骤添加将获取由该触发器找到的新文件或已修改文件内容的操作。    

1. 选择“+ 新步骤”添加在 FTP 服务器上获取文件内容的操作。  
2. 选择**添加操作**链接。  
   ![FTP 操作图 1](./media/connectors-create-api-ftp/ftp-action-1.png)  
3. 输入 *FTP* 搜索与 FTP 相关的所有操作。
4. 选择“FTP - 获取文件内容”作为要在 FTP 文件夹中找到新文件或已修改文件时采取的操作。      
   ![FTP 操作图 2](./media/connectors-create-api-ftp/ftp-action-2.png)  
   “获取文件内容”控件打开。 **注意：** 系统会提示授权逻辑应用访问 FTP 服务器帐户（如果之前尚未这样做）。  
   ![FTP 操作图 3](./media/connectors-create-api-ftp/ftp-action-3.png)   
5. 选择“文件”控件（**文件** * 下方的空白处）。 此处可以使用在 FTP 服务器上找到的新文件或已修改文件的任何属性。  
6. 选择“文件内容”选项。  
   ![FTP 操作图 4](./media/connectors-create-api-ftp/ftp-action-4.png)   
7. 控件更新，指示“FTP - 获取文件内容”操作将获取 FTP 服务器上新文件或已修改文件的“文件内容”。      
   ![FTP 操作图 5](./media/connectors-create-api-ftp/ftp-action-5.png)     
8. 保存所做工作，然后将文件添加到 FTP 文件夹以测试工作流。    

在这种情况下，使用在 FTP 服务器上发现新文件或已修改文件时，监视 FTP 服务器上的文件夹并启动工作流的触发器配置了逻辑应用。 

逻辑应用中也已经配置了一个操作，可获取新文件或已修改文件的内容。

现在可以添加另一个操作（[如“SQL Server - 插入行”](connectors-create-api-sqlazure.md)操作），将新文件或已修改文件的内容插入到 SQL 数据库表中。  

## <a name="connector-specific-details"></a>特定于连接器的详细信息

在[连接器详细信息](/connectors/ftpconnector/)中查看在 Swagger 中定义的触发器和操作，并查看限制。 

## <a name="next-steps"></a>后续步骤
[创建逻辑应用](../logic-apps/quickstart-create-first-logic-app-workflow.md)

