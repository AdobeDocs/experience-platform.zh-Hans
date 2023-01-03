---
title: 数据登陆区目标
description: 了解如何连接到数据登陆区以激活区段和导出数据集。
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# （测试版）数据登陆区目标

>[!IMPORTANT]
>
>此目标当前为测试版，仅适用于数量有限的客户。 请求对 [!DNL Data Landing Zone] 连接时，请联系您的Adobe代表并提供 [!DNL Organization ID].


## 概述 {#overview}

[!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform配置的存储界面，授予您访问基于云的安全文件存储工具的权限，以便将文件导出到平台之外。 您有权访问 [!DNL Data Landing Zone] 容器，且所有容器中的数据总量仅限于随Platform产品和服务许可证提供的总数据量。 平台及其应用程序服务(例如 [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]和 [!DNL Real-Time Customer Data Platform] 已配置一个 [!DNL Data Landing Zone] 每个沙盒的容器。 您可以通过 [!DNL Azure Storage Explorer] 或命令行界面。

[!DNL Data Landing Zone] 支持基于SAS的身份验证，其数据受标准保护 [!DNL Azure Blob] 储存安全机制在存放和运输中。 基于SAS的身份验证使您能够安全地访问 [!DNL Data Landing Zone] 容器。 您无需进行网络更改即可访问 [!DNL Data Landing Zone] 容器，这意味着您无需为网络配置任何允许列表或跨区域设置。

平台对上传到 [!DNL Data Landing Zone] 容器。 七天后会删除所有文件。

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您正在导出区段的所有成员，以及在的 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 批次]** | 批量目标可将文件以3、6、8、12或24小时为增量导出到下游平台。 有关更多信息 [批量基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 管理 [!DNL Data Landing Zone]

您可以使用 [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) 管理 [!DNL Data Landing Zone] 容器。

在 [!DNL Azure Storage Explorer] UI中，选择左侧导航栏中的连接图标。 的 **选择资源** 窗口，为您提供连接到的选项。 选择 **[!DNL Blob container]** 连接到 [!DNL Data Landing Zone] 存储。

![选择资源](/help/sources/images/tutorials/create/dlz/select-resource.png)

接下来，选择 **共享访问签名URL(SAS)** 作为连接方法，然后选择 **下一个**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

选择连接方法后，必须提供 **显示名称** 和 **[!DNL Blob]容器SAS URL** 与 [!DNL Data Landing Zone] 容器。

>[!IMPORTANT]
>
>您必须使用Platform API检索数据登陆区凭据。 有关完整信息，请参阅 [检索数据登陆区凭据](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/create/cloud-storage/data-landing-zone.html?lang=en#retrieve-data-landing-zone-credentials).
>
> 要检索凭据并访问导出的文件，必须替换查询参数 `type=user_drop_zone` with `type=dlz_destination` 中描述的任何HTTP调用。

提供 [!DNL Data Landing Zone] SAS URL，然后选择 **下一个**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

的 **概要** 窗口，为您提供设置的概述，包括有关 [!DNL Blob] 端点和权限。 准备就绪后，选择 **连接**.

![摘要](/help/sources/images/tutorials/create/dlz/summary.png)

成功的连接会更新您的 [!DNL Azure Storage Explorer] UI [!DNL Data Landing Zone] 容器。

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

使用 [!DNL Data Landing Zone] 连接到的容器 [!DNL Azure Storage Explorer]，您现在可以开始将文件从Experience Platform导出到 [!DNL Data Landing Zone] 容器。 要导出文件，您需要建立与 [!DNL Data Landing Zone] 目标，如以下部分中所述。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). 在目标配置工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

因为 [!DNL Data Landing Zone] 是Adobe配置的存储，您无需执行任何步骤来对目标进行身份验证。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。 例如，您可以提及您使用此目标的促销活动。
* **[!UICONTROL 文件夹路径]**:输入将托管导出文件的目标文件夹的路径。
* **[!UICONTROL 文件类型]**:选择导出文件应使用的Experience Platform格式。 选择 [!UICONTROL CSV] 选项，您还 [配置文件格式选项](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 压缩格式]**:选择Experience Platform应用于导出文件的压缩类型。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

### 计划

在 **[!UICONTROL 计划]** 步骤 [设置导出计划](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) , [!DNL Data Landing Zone] 目标，您还 [配置导出文件的名称](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 映射属性和标识 {#map}

在 **[!UICONTROL 映射]** 步骤中，您可以选择要为配置文件导出的属性和标识字段。 您还可以选择将导出文件中的标头更改为任何您希望的友好名称。 有关更多信息，请查看 [映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) （在激活批处理目标UI教程中）。

## （测试版）导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读 [导出数据集教程](/help/destinations/ui/export-datasets.md).

## 验证数据导出是否成功 {#exported-data}

要验证数据是否已成功导出，请检查 [!DNL Data Landing Zone] 并确保导出的文件包含预期的用户档案群体。
