---
title: （测试版） [!DNL Google Ad Manager 360] 连接
description: Google Ad Manager 360是Google的一个广告服务平台，它为出版商提供了通过视频和移动设备应用程序管理其网站上广告显示的方法。
source-git-commit: 60ae86ed6e741bd7739086105bfe70952841d454
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 2%

---

# （测试版） [!DNL Google Ad Manager 360] 连接

## 概述 {#overview}

的 [!DNL Google Ad Manager 360] 连接允许批量上传 [!DNL publisher provided identifiers] (PPID)输入 [!DNL Google Ad Manager 360]，通过 [!DNL Google Cloud Storage].

有关发布者提供的标识符如何在Google Ad Manager 360中工作的更多详细信息，请参阅 [官方Google文档](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>此目标当前为测试版，仅适用于数量有限的客户。 请求对 [!DNL Google Ad Manager 360] 连接时，请联系您的Adobe代表并提供 [!DNL IMS Organization ID].

的 [!DNL Google Ad Manager 360] 目标导出 [!DNL CSV] 文件 [!DNL Google Cloud Storage] 存储段。 导出 [!DNL CSV] 文件，必须将它们导入 [!DNL Google Ad Manager 360] 帐户。

## 目标详情 {#specifics}

请注意以下特定于 [!DNL Google Ad Manager 360] 目标。

* 激活的受众是在Google平台中以编程方式创建的，并填充在CSV文件中。

## 支持的身份 {#supported-identities}

[!DNL This integration] 支持激活下表所述的身份。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | 选择此目标标识以将受众发送到 [!DNL Google Ad Manager 360] |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，在 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 批次]** | 批量目标可将文件以3、6、8、12或24小时为增量导出到下游平台。 有关更多信息 [批量基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 先决条件 {#prerequisites}

### 允许列表 {#allow-listing}

>[!NOTE]
>
>允许列表在设置第一个 [!DNL Google Ad Manager] 目标。 请确保已完成下述允许列表流程 [!DNL Google] 创建目标之前。

在创建 [!DNL Google Ad Manager 360] 目标，您必须联系 [!DNL Google] Adobe添加到允许的数据提供程序列表，以及将帐户添加到允许列表。 联系人 [!DNL Google] 并提供以下信息：

* **帐户ID**:Adobe的帐户ID与Google。 帐户ID:87933855。
* **客户ID**:Adobe的客户帐户ID和Google。 客户ID:89690775。
* **网络ID**:这是你的帐户 [!DNL Google Ad Manager]
* **受众链接ID**:这是你的帐户 [!DNL Google Ad Manager]
* 您的帐户类型。 由Google或AdX购买者提供的DFP。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。 例如，您可以提及您使用此目标的促销活动。
* **[!UICONTROL 存储段名称]**:输入 [!DNL Google Cloud Storage] 存储段供此目标使用。
* **[!UICONTROL 文件夹路径]**:输入将托管导出文件的目标文件夹的路径。

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

在身份映射步骤中，您可以看到以下预填充的映射：

| 预填充映射 | 描述 |
|---------|----------|
| `ECID` -> `ppid` | 这是用户唯一可编辑的预填充映射。 您可以从Platform中选择任何属性或身份命名空间，并将它们映射到 `ppid`. |
| `metadata.segment.alias` -> `list_id` | 将Experience Platform区段名称映射到Google平台中的区段ID。 |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | 告知Google平台何时从区段中删除取消资格的用户。 |

这些映射是 [!DNL Google Ad Manager 360] 并且由Adobe Experience Platform自动为所有 [!DNL Google Ad Manager 360] 连接。

![显示Google Ad Manager 360映射步骤的UI图像。](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## 导出的数据 {#exported-data}

要验证数据是否已成功导出，请检查 [!DNL Google Cloud Storage] 存储段，并确保导出的文件包含预期的用户档案群体。
