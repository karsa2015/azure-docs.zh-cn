---
title: Azure 文件常见问题解答 (FAQ) | Microsoft Docs
description: 查看有关 Azure 文件的常见问题解答。
services: storage
documentationcenter: ''
author: RenaShahMSFT
manager: aungoo
editor: tamram
ms.assetid: ''
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 05/31/2018
ms.author: renash
ms.openlocfilehash: d11ddb0bc15798187ccea22fe1a80a9c86162dcd
ms.sourcegitcommit: ab3b2482704758ed13cccafcf24345e833ceaff3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2018
ms.locfileid: "37866464"
---
# <a name="frequently-asked-questions-faq-about-azure-files"></a>有关 Azure 文件的常见问题解答 (FAQ)
[Azure 文件](storage-files-introduction.md)在云端提供完全托管的文件共享，这些共享项可通过行业标准的[服务器消息块 (SMB) 协议](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx)进行访问。 你可以在云或 Windows、Linux 和 macOS 的本地部署同时装载 Azure 文件共享。 另外，你也可以使用 Azure 文件同步（预览版）在 Windows Server 计算机上缓存 Azure 文件共享，以在靠近使用数据的位置实现快速访问。

本文回答了关于 Azure 文件特性和功能（包括 Azure 文件同步与 Azure 文件的使用）的常见问题。 如果本文未能涵盖你的问题，欢迎通过以下渠道联系我们（以升序排列）：

1. 本文评论部分。
2. [Azure 存储论坛](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)。
3. [Azure 文件 UserVoice](https://feedback.azure.com/forums/217298-storage/category/180670-files)。 
4. Microsoft 支持部门。 若要创建新的支持请求，请在 Azure 门户中的“帮助”选项卡上，选择“帮助和支持”按钮，然后选择“新建支持请求”。

## <a name="general"></a>常规
* <a id="why-files-useful"></a>
**Azure 文件如何发挥作用？**  
   你可以使用 Azure 文件在云中创建文件共享，而无需应对物理服务器、设备或装置的开销。 诸如应用操作系统更新和更换损坏的磁盘等琐碎枯燥的工作，我们可为你逐一代劳。 若要详细了解 Azure 文件适用的应用场景，请参阅[为何 Azure 文件很有用](storage-files-introduction.md#why-azure-files-is-useful)。

* <a id="file-access-options"></a>
**访问 Azure 文件中的文件有哪些不同方式？**  
    可以使用 SMB 3.0 协议将文件共享装载到本地计算机上，也可以使用[存储资源管理器](http://storageexplorer.com/)等工具访问文件共享中的文件。 在应用程序中，可以使用存储客户端库、REST API、PowerShell 或 Azure CLI 来访问 Azure 文件共享中的文件。

* <a id="what-is-afs"></a>
**什么是 Azure 文件同步？**  
    你可以使用 Azure 文件同步，即可将组织的文件共享集中在 Azure 文件中，又不失本地文件服务器的灵活性、性能和兼容性。 Azure 文件同步可以将 Windows Server 计算机转换为 Azure 文件共享的快速缓存。 你可以使用 Windows Server 上的任何可用的协议本地访问你的数据，包括 SMB、网络文件系统 (NFS) 和文件传输协议服务 (FTPS)， 并且可以根据需要在世界各地具有多个缓存。

* <a id="files-versus-blobs"></a>
**相对于 Azure Blob 存储，我为什么要对数据使用 Azure 文件共享？**  
    Azure 文件和 Azure Blob 存储均提供在云中存储大量数据的方法，但是用途略有不同。 
    
    Azure Blob 存储适用于需要存储非结构化数据且具有大规模缩放性的云本机应用程序。 为了更大程度地提升性能和可缩放性，相对于真实的文件系统而言，Azure Blob 存储是更简单的存储抽象。 此外，只可通过基于 REST 的客户端库访问 Azure Blob 存储（或直接通过基于 REST 的协议访问）。

    Azure 文件是一个专门的文件系统， 具有你在使用本地操作系统多年来所熟知和喜爱的所有文件抽象。 例如 Azure Blob 存储，Azure 文件提供了一个 REST 接口和基于 REST 的客户端库。 与 Azure Blob 存储不同的是，Azure 文件提供了对 Azure 文件共享的 SMB 访问权限。 通过使用 SMB，无需对文件系统写入任何代码或附加任何特殊驱动程序，即可在 Windows、Linux 或 macOS 上及本地或云 VM 中直接装载 Azure 文件共享。 此外，你也可以使用 Azure 文件同步在本地文件服务器上缓存 Azure 文件共享，以在靠近使用数据的位置实现快速访问。 
   
    有关 Azure 文件和 Azure Blob 存储之间差异的深入描述，请参阅[确定何时使用 Azure Blob 存储、Azure 文件或 Azure 磁盘](../common/storage-decide-blobs-files-disks.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)。 若要了解有关 Azure Blob 存储的详细信息，请参阅 [Blob 存储简介](../blobs/storage-blobs-introduction.md)。

* <a id="files-versus-disks"></a>**相对于 Azure 磁盘，我为什么要使用 Azure 文件共享？**  
    Azure 磁盘中的磁盘只是一个磁盘。 独立磁盘本身并不能发挥太大作用。 若要充分利用 Azure 磁盘，必须将其与在 Azure 中运行的虚拟机相关联。 Azure 磁盘可用于在本地服务器上使用磁盘的所有内容。 你可将其用作操作系统磁盘、操作系统的交换空间，或者应用程序的专用存储空间。 Azure 磁盘其中一个有趣的用途是，可在云中创建一个文件服务器，以在可能使用 Azure 文件共享的相同位置使用。 当需要 Azure 文件当前不支持的部署选项（例如，NFS 协议支持或高级存储）时，在 Azure 虚拟机中部署文件服务器则是一种非常行之有效的获取 Azure 中文件存储的方法。 

    但是，相比使用 Azure 文件共享，通过将 Azure 磁盘作为后端存储来运行文件服务器的方式，由于多方面的原因，其经济成本通常会更高。 首先，除了为磁盘存储付费之外，还必须为运行一个或多个 Azure VM 的成本付费。 其次，你还必须管理用于运行文件服务器的 VM。 例如，负责操作系统升级。 最后，如果你最终需要在本地缓存数据，则还要自行安装和管理复制技术（例如，分布式文件系统复制 (DFSR)）来实现此目的。

    要同时充分利用 Azure 文件和托管在 Azure 虚拟机中的文件服务器（除了将 Azure 磁盘作为后端存储），其中一种方法是：在云 VM 上托管的文件服务器上安装 Azure 文件同步。 如果 Azure 文件共享与文件服务器位于同一个区域，则可启用云分层并将卷可用空间百分比设置为最大值 (99%)。 这可最大程度地减少重复数据。 而且，你还可以在文件服务器上使用任何你需要的应用程序，例如，需要 NFS 协议支持的应用程序。

    有关在 Azure 中设置高性能和高可用性文件服务器的选项的信息，请参阅[在 Microsoft Azure 中部署 IaaS VM 来宾群集](https://blogs.msdn.microsoft.com/clustering/2017/02/14/deploying-an-iaas-vm-guest-clusters-in-microsoft-azure/)。 有关 Azure 文件和 Azure 磁盘之间差异的深入描述，请参阅[确定何时使用 Azure Blob 存储、Azure 文件或 Azure 磁盘](../common/storage-decide-blobs-files-disks.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)。 若要详细了解 Azure 磁盘，请参阅 [Azure 托管磁盘概述](../../virtual-machines/windows/managed-disks-overview.md)。

* <a id="get-started"></a>
**如何开始使用 Azure 文件？**  
   开始使用 Azure 文件非常简单。 首先，[创建文件共享](storage-how-to-create-file-share.md)，然后再将其装载到首选操作系统中： 

    * [在 Windows 中装载](storage-how-to-use-files-windows.md)
    * [在 Linux 中装载](storage-how-to-use-files-linux.md)
    * [在 macOS 中装载](storage-how-to-use-files-mac.md)

   有关部署 Azure 文件共享以替换组织中生产文件共享的详细指南，请参阅[规划 Azure 文件部署](storage-files-planning.md)。

* <a id="redundancy-options"></a>
**Azure 文件支持哪些存储冗余选项？**  
    目前，Azure 文件支持本地冗余存储 (LRS)、区域冗余存储 (ZRS) 和异地冗余存储 (GRS)。 将来我们计划支持读取访问权限异地冗余存储 (RA-GRS)，但目前还没有可分享的日程表。

* <a id="tier-options"></a>
**Azure 文件支持哪些存储层？**  
    Azure 文件目前仅支持标准存储层。 当前我们暂无有关高级存储和冷存储支持的日程表可供分享。 
    
    > [!NOTE]
    > 你无法使用仅限 Blob 存储帐户或高级存储帐户创建 Azure 文件共享。

* <a id="give-us-feedback"></a>
**我非常希望可以将某项特定功能添加到 Azure 文件。你们会添加它吗？**  
    Azure 文件团队非常乐于听取你针对我们服务提供的任何反馈。 请在 [Azure 文件 UserVoice](https://feedback.azure.com/forums/217298-storage/category/180670-files) 上进行功能请求投票！ 希望我们提供的众多新功能能够满足你的需求。

## <a name="azure-file-sync"></a>Azure 文件同步

* <a id="afs-region-availability"></a>
**Azure 文件同步（预览版）支持哪些区域？**  
    目前，Azure 文件同步在以下区域中可用：澳大利亚东部、澳大利亚东南部、加拿大中部、加拿大东部、美国中部、亚洲东部、美国东部、美国东部 2、北欧、东南亚、英国南部、英国西部、西欧和美国西部。 在我们努力全面推出的过程中，我们将增加对更多地区的支持。 有关详细信息，请参阅[地区可用性](storage-sync-files-planning.md#region-availability)。

* <a id="cross-domain-sync"></a>
**是否可以在同一个同步组中同时包含已加入域的服务器和未加入域的服务器？**  
    是的。 同步组可以包含具有不同的 Active Directory 成员身份的服务器终结点，即使它们未加入域。 虽然从严格意义上讲这种配置可用，但不建议将此作为常规配置，因为在某个服务器上为文件和文件夹定义的访问控制列表 (ACL) 可能无法由同步组中的其他服务器实施。 为获得最佳结果，建议在同一个 Active Directory 林中的服务器之间、在不同 Active Directory 林中但已建立信任关系的服务器之间，或未加入域的服务器之间进行同步。 我们建议你避免混合使用这些配置。

* <a id="afs-change-detection"></a>
**我通过 SMB 或门户在 Azure 文件共享中直接创建了一个文件。多久后该文件才会同步到同步组中的服务器上？**  
    [!INCLUDE [storage-sync-files-change-detection](../../../includes/storage-sync-files-change-detection.md)]

* <a id="afs-conflict-resolution"></a>**如果在两个服务器上几乎同时对同一文件进行了更改后，会发生什么情况？**  
    Azure 文件同步会使用简单的冲突解决策略：同时在两台服务器上对文件进行的更改都会保留。 最新写入的更改保留原始文件名称。 较早的文件将“源”计算机和冲突编号追加到名称中。 它遵循以下分类： 
   
    \<FileNameWithoutExtension\>-\<MachineName\>\[-#\].\<ext\>  

    例如，如果 CentralServer 是较早写入的位置，则 CompanyReport.docx 的第一个冲突将变为 CompanyReport-CentralServer.docx。 第二个冲突将被命名为 CompanyReport-CentralServer-1.docx。

* <a id="afs-storage-redundancy"></a>
**Azure 文件同步是否支持异地冗余存储？**  
    是的，Azure 文件支持本地冗余存储 (LRS) 和异地冗余存储 (GRS)。 如果配对区域之间出现 GRS 故障转移，建议仅将新区域视为数据的备份。 Azure 文件同步不会自动开始与新的主区域进行同步。 

* <a id="sizeondisk-versus-size"></a>
**使用 Azure 文件共享后，为什么文件的占用空间属性与大小属性不一致？**  
    Windows 文件资源管理器公开了两个属性来表示文件的大小：即“大小”和“占用空间”。 这些属性的含义略有不同。 “大小”表示文件的完整大小。 “占用空间”表示存储在磁盘上的文件流的大小。 这些属性的值存在差异的原因有多种，例如压缩、使用重复数据删除，或使用 Azure 文件同步进行的云分层。如果文件被分层到 Azure 文件共享，则占用空间为零，因为该文件流存储在 Azure 文件共享中，而未存储在磁盘上。 另外，文件也可能会被部分分层（或部分召回）。 在部分分层文件中，该文件的一部分位于磁盘上。 应用程序（例如，多媒体播放器或压缩工具）对文件进行了部分读取时可能会发生此情况。 

* <a id="is-my-file-tiered"></a>
**如何分辨文件是否已被分层？**  
    有多种查看文件是否已被分层到 Azure 文件共享的方法：
    
   *  **查看文件上的文件属性。**
     若要执行此操作，请右键单击文件，转到“详细信息”，然后向下滚动至“特性”属性。 分层的文件具有以下属性集：     
        
        | 属性字母 | 属性 | 定义 |
        |:----------------:|-----------|------------|
        | A | 存档 | 指示备份软件应备份此文件。 无论文件被分层还是完全存储在磁盘上，始终都会设置此属性。 |
        | P | 稀疏文件 | 指示该文件为稀疏文件。 稀疏文件是 NTFS 提供的专用化文件类型，用于在占用空间流上的文件几乎为空时提高使用效率。 Azure 文件同步将使用稀疏文件，因为文件会被完全分层或部分召回。 在完全分层文件中，文件流存储在云中。 在部分召回的文件中，文件的一部分已在磁盘上。 如果文件被完全召回到磁盘，Azure 文件同步会将其从稀疏文件转换为常规文件。 |
        | L | 重分析点 | 指示该文件包含重分析点。 重分析点是供文件系统筛选器使用的特殊指针。 Azure 文件同步使用重分析点来定义 Azure 文件同步文件系统筛选器 (StorageSync.sys) 存储文件的云位置。 这样即可支持无缝访问。 用户无需知道是否使用了 Azure 文件同步或如何获取在 Azure 文件共享中的文件访问权限。 如果文件被完全召回，则 Azure 文件同步将从此文件中删除重分析点。 |
        | O | 脱机 | 指示文件的部分或全部内容未存储在磁盘上。 如果文件被完全召回，Azure 文件同步将删除此属性。 |

        ![文件的“属性”对话框（“详细信息”选项卡被选中）](media/storage-files-faq/azure-file-sync-file-attributes.png)
        
        你可以通过向文件资源管理器的表显示添加“属性”字段，查看文件夹中所有文件的属性。 若要执行此操作，请右键单击现有的列（例如“大小”），选择“更多”，然后从下拉列表中选择“属性”。
        
   * “使用 `fsutil` 检查文件上的重分析点”。
       如前面的选项中所述，分层的文件始终具有重分析点集。 重分析指针是 Azure 文件同步文件系统筛选器 (StorageSync.sys) 的特殊指针。 若要查看文件是否包含重分析点，你可以在提升的命令提示符或 PowerShell 窗口中运行 `fsutil` 实用程序：
    
        ```PowerShell
        fsutil reparsepoint query <your-file-name>
        ```

        如果文件包含重分析点，则应能看到“重分析标记值: 0x8000001e”。 该十六进制值是 Azure 文件同步拥有的重分析点值。输出还会包含表示 Azure 文件共享中文件路径的重分析数据。

        > [!WARNING]  
        > 同时，`fsutil reparsepoint` 实用程序命令还包含删除重分析点的功能。 除非 Azure 文件同步工程团队要求，否则请不要执行此命令。 运行此命令可能会导致数据丢失。 

* <a id="afs-recall-file"></a>**我想要使用的一个文件已被分层。如何将文件召回到磁盘以在本地使用？**  
    将文件召回到磁盘的最简单方法是打开此文件。 Azure 文件同步文件系统筛选器 (StorageSync.sys) 将会从 Azure 文件共享中无缝下载此文件，你无需执行任何操作。 对于可被部分读取的文件类型（如多媒体文件或 .zip 文件），打开文件后不会下载整个文件。

    此外，你也可以使用 PowerShell 来强制召回文件。 在需要同时召回多个文件（例如，一个文件夹内的所有文件）的情况下，可能更适合使用此选项。 打开已安装 Azure 文件同步的服务器节点的 PowerShell 会话，然后运行以下 PowerShell 命令：
    
    ```PowerShell
    Import-Module "C:\Program Files\Azure\StorageSyncAgent\StorageSync.Management.ServerCmdlets.dll"
    Invoke-StorageSyncFileRecall -Path <file-or-directory-to-be-recalled>
    ```

* <a id="afs-force-tiering"></a>
**如何强制将文件或目录分层？**  
    启用云分层功能后，它会根据上次访问和修改时间自动分层文件，以实现云终结点上指定的卷可用空间百分比， 但有时你可能需要手动强制分层文件。 如果你要保存在长时间内计划不再次使用的大型文件，并且想要将卷上现有可用空间用于其他文件和文件夹，则可使用此方法。 可使用以下 PowerShell 命令强制分层：

    ```PowerShell
    Import-Module "C:\Program Files\Azure\StorageSyncAgent\StorageSync.Management.ServerCmdlets.dll"
    Invoke-StorageSyncCloudTiering -Path <file-or-directory-to-be-tiered>
    ```

* <a id="afs-effective-vfs"></a>
**当卷上有多个服务器终结点时，如何解释卷可用空间？**  
    如果卷上有多个服务器终结点，有效卷可用空间阈值为在该卷上的所有服务器终结点中指定的最大卷可用空间。 将根据使用模式对文件进行分层，而不考虑它们属于哪一个服务器终结点。 例如，如果卷上有两个服务器终结点 Endpoint1 和 Endpoint2，其中 Endpoint1 的卷可用空间阈值为 25%，Endpoint2 的卷可用空间阈值为 50%，那么这两个服务器终结点的卷可用空间阈值将为 50%。

* <a id="afs-files-excluded"></a>
**会被 Azure 文件同步自动排出的文件或文件夹有哪些？**  
    默认情况下，Azure 文件同步会排除以下文件：
    * desktop.ini
    * thumbs.db
    * ehthumbs.db
    * ~$\*.\*
    * \*.laccdb
    * \*.tmp
    * 635D02A9D91C401B97884B82B3BCDAEA.\*

    默认情况下，还会排除以下文件夹：

    * \系统卷信息
    * \$RECYCLE.BIN
    * \SyncShareState

* <a id="afs-os-support"></a>
**我是否可以将 Azure 文件同步与 Windows Server 2008 R2、Linux 或我的网络连接存储 (NAS) 设备一起使用？**  
    Azure 文件同步当前仅支持 Windows Server 2016 和 Windows Server 2012 R2。 目前，我们暂无可分享的其他计划，但我们愿意根据客户需求支持其他平台。 请在 [Azure 文件 UserVoice](https://feedback.azure.com/forums/217298-storage/category/180670-files) 上告知你想要我们支持的平台。

* <a id="afs-tiered-files-out-of-endpoint"></a>
**为什么分层文件存在于服务器终结点命名空间之外？**  
    在 Azure 文件同步代理版本 3 之前，Azure 文件同步阻止将分层文件移到服务器终结点之外但位于服务器终结点所在卷上的其他位置。 复制操作、非分层文件的移动操作以及将分层文件移到其他卷的操作不受影响。 这种行为的原因是由于这样的隐含假设：文件资源管理器和其他 Windows API 在同一卷上的移动操作是（几乎）即时重命名操作。 这意味着，移动会使文件资源管理器或其他移动方法（如命令行或 PowerShell）看起来没有响应，而 Azure 文件同步会从云中召回数据。 从 [Azure 文件同步代理版本 3.0.12.0](storage-files-release-notes.md#agent-version-30120) 开始，Azure 文件同步将允许将分层文件移到服务器终结点之外。 我们通过允许分层文件作为服务器终结点之外的分层文件存在，然后在后台召回该文件以避免前面提到的负面影响。 这意味着在同一卷上的移动是即时的，在移动完成后，我们要做将文件召回到磁盘的所有工作。 

* <a id="afs-do-not-delete-server-endpoint"></a>
**我在服务器上遇到 Azure 文件同步问题（同步、云分层等）。是否应删除并重新创建服务器终结点？**  
    [!INCLUDE [storage-sync-files-remove-server-endpoint](../../../includes/storage-sync-files-remove-server-endpoint.md)]

## <a name="security-authentication-and-access-control"></a>安全性、身份验证和访问控制
* <a id="ad-support"></a>
**Azure 文件是否支持基于 Active Directory 的身份验证和访问控制？**  
    Azure 文件提供了两种方法来管理访问控制：

    - 你可以使用共享访问签名 (SAS) 生成在指定时间间隔内有效的具有特定权限的令牌。 例如，可以生成在 10 分钟后到期、对特定文件具有只读访问权限的令牌。 只要拥有此有效令牌，就可以在 10 分钟内拥有对给定文件的只读访问权限。 目前，仅通过 REST API 或客户端库支持共享的访问签名密钥。 你必须使用存储帐户密钥通过 SMB 装载 Azure 文件共享。

    - Azure 文件同步会保留所有自定义 ACL 或 DACL（无论基于 Active Directory 或本地目录），并复制到其同步到的所有服务器终结点。 由于 Windows 服务器已经可以使用 Active Directory 进行身份验证，因此，在全面支持基于 Active Directory 的身份验证和实现对 ACL 的支持前，Azure 文件同步是一个有效的临时选择。

    当前，Azure 文件不直接支持 Active Directory。

* <a id="encryption-at-rest"></a>
**如何确保已静态加密 Azure 件共享？**  
    Azure 存储服务加密默认在所有区域启用。 对于这些区域，你无需执行任何操作来启用加密。 对其他区域，请参阅[服务器端加密](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)。

* <a id="access-via-browser"></a>
**如何使用 Web 浏览器提供对特定文件的访问权限？**  
    你可以使用共享访问签名生成在指定时间间隔内有效的、具有特定权限的令牌。 例如，可以生成一个在设定时段内对特定文件具有只读访问权限的令牌。 只要拥有此 URL，就可以在令牌有效期间，直接通过任意 Web 浏览器访问文件。 你可以从类似存储资源管理器的 UI 轻松生成共享的访问签名密钥。

* <a id="file-level-permissions"></a>
**能否对共享中的文件夹指定只读或只写权限？**  
    如果使用 SMB 装载文件共享，则不具有文件夹级的控制权限。 但是，如果使用 REST API 或客户端库创建共享访问签名，则可以在共享内的文件夹上指定只读或只写权限。

* <a id="ip-restrictions"></a>
**是否对 Azure 文件共享实现 IP 限制？**  
    是的。 可以在存储帐户级别对 Azure 文件共享的权限进行限制。 有关详细信息，请参阅[配置 Azure 存储防火墙和虚拟网络](../common/storage-network-security.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)。

* <a id="data-compliance-policies"></a>
**Azure 文件支持哪些数据符合性策略？**  
   Azure 文件所依据的存储体系结构与 Azure 存储中的其他存储服务使用的相同。 Azure 文件实施的数据符合性策略也与其他 Azure 存储服务使用的相同。 有关 Azure 存储数据符合性的更多信息，可以下载并参阅 [Microsoft Azure 数据保护文档](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409)和 [Microsoft 信任中心](https://microsoft.com/en-us/trustcenter/default.aspx)。

## <a name="on-premises-access"></a>本地访问
* <a id="expressroute-not-required"></a>
**必须使用 Azure ExpressRoute 才能在本地连接到 Azure 文件或使用 Azure 文件同步吗？**  
    不是。 ExpressRoute 不是访问 Azure 文件共享的必要条件。 如果要直接在本地装载 Azure 文件共享，则只需打开端口 445（TCP 出站）即可进行 Internet 访问（这是 SMB 用于进行通信的端口）。 如果正在使用 Azure 文件同步，则只需端口 443（TCP 出站）即可进行 HTTPS 访问（无需 SMB）。 但是，你可以将 ExpressRoute 与这些访问选项中任意一项一起使用。

* <a id="mount-locally"></a>
**如何才能在本地计算机上装载 Azure 文件共享？**  
    可以使用 SMB 协议装载文件共享，只要端口 445（TCP 出站）处于打开状态，且客户端支持 SMB 3.0 协议（例如，如果使用的是 Windows 10 或 Windows Server 2016）。 如果端口 445 被组织的策略或 ISP 阻止，则可使用 Azure 文件同步访问 Azure 文件共享。

## <a name="backup"></a>备份
* <a id="backup-share"></a>
**如何备份我的 Azure 文件共享？**  
    可以使用定期[共享快照](storage-snapshots-files.md)来防止意外删除。 此外，也可以使用 AzCopy、RoboCopy 或能够备份已装载文件共享的第三方备份工具。 Azure 备份提供 Azure 文件的备份。 深入了解[通过 Azure 备份服务备份 Azure 文件共享](https://docs.microsoft.com/en-us/azure/backup/backup-azure-files)。

## <a name="share-snapshots"></a>共享快照
### <a name="share-snapshots-general"></a>共享快照：常规问题
* <a id="what-are-snaphots"></a>
**什么是文件共享快照？**  
    可以使用 Azure 文件共享快照创建只读版本的文件共享。 另外，也可以使用 Azure 文件将早期版本的内容复制回 Azure 或本地中的同一个共享或备用位置中，以做进一步修改。 若要了解有关共享快照的详细信息，请参阅[共享快照概述](storage-snapshots-files.md)。

* <a id="where-are-snapshots-stored"></a>
**共享快照存储在何处？**  
    共享快照与文件共享存储在同一个存储帐户中。

* <a id="snapshot-perf-impact"></a>
**使用共享快照是否会产生任何性能影响？**  
    共享快照没有任何性能开销。

* <a id="snapshot-consistency"></a>
**共享快照是否与应用程序一致？**  
    否，共享快照与应用程序不一致。 执行共享快照前，用户必须将应用程序中的写入刷新到共享中。

* <a id="snapshot-limits"></a>
**对我可使用的共享快照数有限制吗？**  
    是的。 Azure 文件可以最多保留 200 张共享快照。 共享快照不计入共享配额，因此，对所有共享快照使用的总空间没有单独的共享限制。 存储帐户限制仍然适用。 在达到 200 个共享快照之后，必须删除旧的共享快照才可创建新的共享快照。
* <a id="snapshot-cost"></a>
**共享快照的费用是多少？**  
    快照按标准事务和标准存储收费。 快照在本质上是递增的。 基本快照即是共享本身。 所有的后续快照均是递增的，并且只会存储与之前快照的不同之处。 这意味着，如果工作负荷改动极小，则帐单上显示的增量更改也很小。 有关标准 Azure 文件的定价信息，请参阅[定价页](https://azure.microsoft.com/pricing/details/storage/files/)。 目前，查看共享快照已用大小的方法是比较计费的容量与使用的容量。 我们致力于开发改进报告的工具。


### <a name="create-share-snapshots"></a>创建共享快照
* <a id="file-snaphsots"></a>
**是否可以创建单个文件的共享快照？**  
    可在文件共享级别上创建共享快照。 你可以从文件共享快照还原单个文件，但是不能创建文件级别的共享快照。 但是，如果你已执行共享级别的共享快照，并且想要列出已更改特定文件的共享快照，则可以在已装载 Windows 的共享上的“以前的版本”下执行此操作。 
    
    如需文件快照功能，请通过 [Azure 文件 UserVoice](https://feedback.azure.com/forums/217298-storage/category/180670-files) 告知我们。

* <a id="encypted-snapshots"></a>
**是否可以创建加密文件共享的共享快照？**  
    可以对已启用静态加密的 Azure 文件共享执行共享快照。 可以从共享快照中将文件还原到加密文件共享中。 如果共享已加密，则共享快照也会加密。

* <a id="geo-redundant-snaphsots"></a>
**共享快照具有异地冗余吗？**  
    共享快照与捕获它们的 Azure 文件共享具有相同的冗余。 如果已为帐户选择异地冗余存储，则共享快照也会在配对区域中进行冗余存储。

### <a name="manage-share-snapshots"></a>管理共享快照
* <a id="browse-snapshots-linux"></a>
**是否可以在 Linux 中浏览共享快照？**  
    可以使用 Azure CLI 2.0 在 Linux 上创建、列出、浏览和还原共享快照。

* <a id="copy-snapshots-to-other-storage-account"></a>
**是否可以将共享快照复制到不同的存储帐户？**  
    可以将文件从共享快照复制到其他位置，但不能复制到共享快照本身。

### <a name="restore-data-from-share-snapshots"></a>从共享快照还原数据
* <a id="promote-share-snapshot"></a>
**是否可以将共享快照提升到基本共享中？**  
    只能将数据从共享快照复制到任何其他目标位置， 不能将共享快照提升到基本共享中。

* <a id="restore-snapshotted-file-to-other-share"></a>
**是否可以将数据从共享快照还原到不同的存储帐户？**  
    是的。 可以将共享快照文件复制到原始位置或备用位置，其中包括位于同一区域或不同区域的相同/不同的存储帐户。 你还可以将文件复制到本地位置或任何其他云。    
  
### <a name="clean-up-share-snapshots"></a>清除共享快照
* <a id="delete-share-keep-snapshots"></a>
**是否可以删除共享，而不删除共享快照？**  
    如果共享上有活动的共享快照，则无法删除此共享。 你可以使用一个 API 将共享快照连同共享一起删除。 此外，也可以在 Azure 门户中删除共享快照和共享。

* <a id="delete-share-with-snapshots"></a>
**如果删除存储帐户，共享快照会怎样？**  
    删除存储帐户后，共享快照也将被删除。

## <a name="billing-and-pricing"></a>计费和定价
* <a id="vm-file-share-network-traffic"></a>
**Azure VM 与 Azure 文件共享之间的网络流量是否作为外部带宽计入订阅费用？**  
    如果文件共享和 VM 位于同一 Azure 区域，则它们之间的流量是不会额外收费的。 如果文件共享和 VM 位于不同的区域，则它们之间的流量会作为外部带宽收费。

* <a id="share-snapshot-price"></a>
**共享快照的费用是多少？**  
     在预览版期间，共享快照容量可免费使用， 但会收取标准存储出口和事务费用。 公开发布后，共享快照的容量和事务均将收费。
     
     共享快照在本质上是递增的。 基本共享快照即是共享本身。 所有的后续共享快照均是递增的，并且只会存储与之前共享快照的不同之处。 你只需为更改的内容付费。 如果你的共享包含 100 GiB 数据，但自执行上次共享快照以来只更改了 5 GiB 数据，则共享快照只额外使用了 5 GiB 数据，而你要为 105 GiB 付费。 有关事务和标准出口费用的更多信息，请参阅[定价页](https://azure.microsoft.com/pricing/details/storage/files/)。

## <a name="scale-and-performance"></a>缩放和性能
* <a id="files-scale-limits"></a>
**Azure 文件存在哪些缩放限制？**  
    有关 Azure 文件的可伸缩性和性能目标的信息，请参阅 [Azure 文件可伸缩性和性能目标](storage-files-scale-targets.md)。

* 
  <a id="need-larger-share">
    </a>
  

  **我需要大于 Azure 文件目前提供的文件共享的文件共享。我是否可以增加 Azure 文件共享的大小？**  
  不是。 Azure 文件共享的上限是 5 TiB。 当前，这是硬限制，无法调整。 我们正致力于寻找将共享大小提升至 100 TiB 的解决方案，但当前尚无可供分享的时间表。

* <a id="open-handles-quota"></a>
**多少个客户端可以同时访问同一文件？**   
    单个文件有 2000 个打开句柄配额。 当你拥有 2000 个打开句柄时，会显示一条错误消息，指示已达到此配额。

* <a id="zip-slow-performance"></a>
**解压 Azure 文件中的文件时性能较慢。我该怎样做？**  
    若要将大量文件传输到 Azure 文件，建议使用 AzCopy（Windows 版；Linux 和 Unix 预览版）或 Azure Powershell。 这些工具已针对网络传输进行了优化。

* <a id="slow-perf-windows-81-2012r2"></a>
**为什么在 Windows Server 2012 R2 或 Windows 8.1 上装载了 Azure 文件共享后性能较慢？**  
    在 Windows Server 2012 R2 和 Windows 8.1 上装载 Azure 文件共享后，有一个已知的问题。 在 2014 年 4 月的 Windows 8.1 和 Windows Server 2012 R2 累积更新中已修补了此问题。 请确保 Windows Server 2012 R2 和 Windows 8.1 的所有实例均应用了此修补程序，以获得最佳性能。 （你应始终通过 Windows 更新获取 Windows 修补程序。）有关更多信息，请查看相关的 Microsoft 识库文章[从 Windows 8.1 或 Server 2012 R2 访问 Azure 文件时性能降低](https://support.microsoft.com/kb/3114025)。

## <a name="features-and-interoperability-with-other-services"></a>功能以及与其他服务的互操作性
* <a id="cluster-witness"></a>
**是否可以将 Azure 文件共享作为 Windows 服务器故障转移群集的文件共享见证？**  
    Azure 文件共享目前不支持此配置。 有关如何为 Azure Blob 存储设置此服务的详细信息，请参阅[部署故障转移群集的云见证](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness)。

* <a id="containers"></a>
**是否可以在 Azure 容器实例上装载 Azure 文件共享？**  
    是，当信息超出容器实例生存期时，通过 Azure 文件共享来保存信息不失为一种绝佳选择。 有关更多信息，请参阅[使用 Azure 容器实例装载 Azure 文件共享](../../container-instances/container-instances-mounting-azure-files-volume.md)。

* <a id="rest-rename"></a>
**REST API 中是否有重命名操作？**  
    现在不行。

* <a id="nested-shares"></a>
**是否可以设置嵌套共享？也就是说，能否在共享下使用共享？**  
    不是。 文件共享是可以装载的虚拟驱动程序，因此不支持嵌套共享。

* <a id="ibm-mq"></a>
**如何将 Azure 文件与 IBM MQ 配合使用？**  
    IBM 已发布相关文档，帮助 IBM MQ 客户通过 IBM 服务配置 Azure 文件。 有关更多信息，请参阅[如何通过 Microsoft Azure 文件服务设置 IBM MQ 多实例队列管理器](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service)。

## <a name="see-also"></a>另请参阅
* [在 Windows 中排查 Azure 文件问题](storage-troubleshoot-windows-file-connection-problems.md)
* [在 Linux 中排查 Azure 文件问题](storage-troubleshoot-linux-file-connection-problems.md)
* [对 Azure 文件同步（预览版）进行故障排除](storage-sync-files-troubleshoot.md)
