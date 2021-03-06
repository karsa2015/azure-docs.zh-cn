---
title: 可用于 Azure 机器学习数据准备的目标/输出示例 | Microsoft Docs
description: 本文档提供了一组可用于 Azure 机器学习数据准备的自定义数据目标/输出的示例
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: desktop-workbench
ms.workload: data-services
ms.custom: ''
ms.devlang: ''
ms.topic: article
ms.date: 02/01/2018
ms.openlocfilehash: 93da07006280b38c9e6539773e6ac22e50e48b57
ms.sourcegitcommit: 944d16bc74de29fb2643b0576a20cbd7e437cef2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2018
ms.locfileid: "34831806"
---
# <a name="sample-of-destination-connections-python"></a>目标连接示例 (Python) 
阅读本附录前，请先阅读 [Python 扩展性概述](data-prep-python-extensibility-overview.md)。


## <a name="write-to-excel"></a>写入到 Excel 


写入到 Excel 需要其他库。 在扩展性概述中介绍了如何添加新库。 `openpyxl` 是需要添加的库。

写入到 Excel 之前，可能需要进行其他一些更改。 某些目标格式不支持在数据准备中使用的某些数据类型。 例如，如果存在“错误”对象，它们将不会正确序列化到 Excel。 因此，在尝试写入 Excel 之前，需要执行从任何列中删除错误的“替换错误值”转换。

如果上述所有工作都已完成，以下行会将数据表写入 Excel 文档中的单个工作表。 添加“转换数据流(脚本)”转换。 然后在表达式部分中输入以下代码。


### <a name="on-windows"></a>在 Windows 上 
```python
df.to_excel('c:\dev\data\Output\Customer.xlsx', sheet_name='Sheet1')
```

### <a name="on-macosos-x"></a>在 macOS/OS X 上 ###
```python
df.to_excel('c:/dev/data/Output/Customer.xlsx', sheet_name='Sheet1')
```
