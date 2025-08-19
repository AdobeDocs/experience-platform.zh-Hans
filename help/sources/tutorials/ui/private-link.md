---
title: 在UI中为源使用Azure专用链接
description: 了解如何在Experience Platform UI中为源使用Azure专用链接。
badge: Beta 版
exl-id: 2882729e-2d46-48dc-9227-51dda5bf7dfb
source-git-commit: b88cf63e907b3f127f83304aa95f82300b47ce0b
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# 在UI中将[!DNL Azure Private Link]用于源

>[!AVAILABILITY]
>
>此功能处于测试阶段，当前仅支持以下源：
>
>* [[!DNL Azure Blob Storage]](../../connectors/cloud-storage/blob.md)
>* [[!DNL ADLS Gen2]](../../connectors/cloud-storage/adls-gen2.md)
>* [[!DNL Azure File Storage]](../../connectors/cloud-storage/azure-file-storage.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)

您可以使用[!DNL Azure Private Link]功能为要连接的Adobe Experience Platform源创建专用端点。 使用私有IP地址将源安全地连接到虚拟网络，消除对公共IP的需求，并减少攻击面。通过消除对复杂防火墙或网络地址转换配置的需求，简化网络设置，同时确保数据流量仅能到达批准的服务。

阅读本指南，了解如何在Experience Platform UI中使用源工作区来创建和使用专用端点。

## 创建专用端点

要开始使用[!DNL Azure Private Link]，请导航到Experience Platform UI的&#x200B;*[!UICONTROL 源]*&#x200B;目录，然后从源工作区的选项卡菜单中选择&#x200B;**[!UICONTROL 私有端点]**。

![具有“私有端点”的源目录。](../../images/tutorials/private-links/catalog.png)

使用界面可查看有关现有专用端点的信息，例如其ID、关联的源和当前状态。 要创建新的专用终结点，请选择&#x200B;**[!UICONTROL 创建专用终结点]**。

![已选择“创建专用终结点”的专用终结点接口。](../../images/tutorials/private-links/private-endpoints.png)

接下来，选择所需的源，然后输入以下属性的值：

| 属性 | 描述 |
| --- | --- |
| `name` | 专用端点的名称。 |
| `subscriptionId` | 与您的[!DNL Azure]订阅关联的ID。 有关详细信息，请参阅[!DNL Azure]上的[指南，从 [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id)中检索您的订阅和租户ID。 |
| `resourceGroupName` | [!DNL Azure]上资源组的名称。 资源组包含[!DNL Azure]解决方案的相关资源。 有关详细信息，请阅读有关[!DNL Azure]管理资源组[的](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal)指南。 |
| `resourceGroup` | 资源的名称。 在[!DNL Azure]中，资源引用虚拟机、Web应用和数据库等实例。 有关详细信息，请阅读[!DNL Azure]上的[指南，以了解 [!DNL Azure] 资源管理器](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview)。 |
| `fqdns` | 源的全限定域名。 **注意**：仅当使用[!DNL Snowflake]源时，才需要此属性。 |

{style="table-layout:auto"}

完成后，选择&#x200B;**[!UICONTROL 提交]**。

![在源UI工作区中创建新专用终结点的身份验证窗口。](../../images/tutorials/private-links/create-private-endpoint.png)

### 批准专用端点

新创建的端点将保持挂起状态，直到获得管理员批准。

要批准[!DNL Azure Blob]和[!DNL Azure Data Lake Gen2]源的专用终结点请求，请登录到[!DNL Azure Portal]。 在左侧导航中，选择&#x200B;**[!DNL Data storage]**，然后转到&#x200B;**[!DNL Security + networking]**&#x200B;选项卡并选择&#x200B;**[!DNL Networking]**。 接下来，选择&#x200B;**[!DNL Private endpoints]**&#x200B;以查看与您的帐户关联的专用端点列表及其当前连接状态。 要批准挂起的请求，请选择所需的终结点，然后单击&#x200B;**[!DNL Approve]**。

![包含待处理专用终结点列表的Azure门户。](../../images/tutorials/private-links/azure.png)

## 创建具有专用端点的帐户

导航到源目录并选择支持专用端点的源。 接下来，使用您的源创建一个新帐户，在帐户身份验证期间，选择&#x200B;**[!UICONTROL 私有终结点]**&#x200B;切换开关。 提供源的身份验证凭据，然后选择&#x200B;**[!UICONTROL 连接到源]**&#x200B;允许几分钟以建立连接。

>[!NOTE]
>
>如果启用了[!UICONTROL 私有终结点]选项，Experience Platform将检查所选源是否存在批准的私有终结点。 如果未找到批准的端点，您将无法建立连接。

![已启用私有终结点的新帐户身份验证步骤。](../../images/tutorials/private-links/new-account.png)

接下来，导航到源的[!UICONTROL 现有帐户]界面。 使用此界面可查看现有帐户及其相应状态的列表。 您可以选择筛选器图标![筛选器图标](../../../images/icons/filter.png)以仅显示已启用与专用终结点连接的帐户。

![源工作流程中的现有帐户接口仅显示为专用终结点连接启用的筛选帐户。](../../images/tutorials/private-links/existing-private-endpoints.png)

选择要使用的帐户，然后启用&#x200B;**[!UICONTROL 交互式创作]**。 此切换激活[!UICONTROL 交互式创作]，这是一项[!DNL Azure]功能，允许您测试连接、浏览文件夹列表和预览数据。 专用终结点连接需要启用[!UICONTROL 交互式创作]。 请注意，您无法手动关闭此切换开关；它在60分钟后自动禁用。

[!UICONTROL 交互式创作]需要几分钟才能启用。 启用该设置后，选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续执行下一步，并选择要摄取的数据。

![已选择现有帐户并启用交互式创作。](../../images/tutorials/private-links/interactive-authoring.png)

## 后续步骤

现在您已经成功创建了私有端点，接下来可以创建源连接和数据流，并使用私有端点摄取数据。 有关如何在UI中创建数据流的信息，请阅读以下指南：

* [为云存储源创建数据流](../ui/dataflow/batch/cloud-storage.md)
* [为数据库源创建数据流](../ui/dataflow/databases.md)
