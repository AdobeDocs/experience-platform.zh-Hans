---
title: （测试版） [!DNL Google Ad Manager 360] 连接
description: Google Ad Manager 360是Google的一个广告服务平台，它为出版商提供了通过视频和移动设备应用程序管理其网站上广告显示的方法。
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: 5174c65970aa8df9bc3f2c8d612c26c72c20e81f
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 4%

---

# （测试版） [!DNL Google Ad Manager 360] 连接

## 概述 {#overview}

的 [!DNL Google Ad Manager 360] 连接允许批量上传 [!DNL publisher provided identifiers] (PPID)输入 [!DNL Google Ad Manager 360]，通过 [!DNL Google Cloud Storage].

有关发布者提供的标识符如何在Google Ad Manager 360中工作的更多详细信息，请参阅 [官方Google文档](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>此目标当前为测试版，仅适用于数量有限的客户。 请求对 [!DNL Google Ad Manager 360] 连接时，请联系您的Adobe代表并提供 [!DNL organization ID].

的 [!DNL Google Ad Manager 360] 目标导出 [!DNL CSV] 文件 [!DNL Google Cloud Storage] 存储段。 导出 [!DNL CSV] 文件，必须将它们导入 [!DNL Google Ad Manager 360] 帐户。

## 目标详情 {#specifics}

请注意以下特定于 [!DNL Google Ad Manager 360] 目标。

* 激活的受众是在Google平台中以编程方式创建的，并填充在CSV文件中。

## 支持的身份 {#supported-identities}

[!DNL This integration] 支持激活下表所述的身份。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | 选择此目标标识以将受众发送到 [!DNL Google Ad Manager 360] |

{style="table-layout:auto"}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您正在导出区段的所有成员，以及在的 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 批次]** | 批量目标可将文件以3、6、8、12或24小时为增量导出到下游平台。 有关更多信息 [批量基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

### 允许列表 {#allow-listing}

在设置第一个允许列表之前，必须将其添加到允许列表 [!DNL Google Ad Manager 360] 目标。 在创建目标之前，请确保完成下面描述的允许列表流程。

>[!NOTE]
>
>此规则的例外情况是现有规则 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 客户。 如果您已在Audience Manager中创建到此Google目标的连接，则无需再次完成允许列表过程，您可以继续执行后续步骤。

1. 按照 [Google Ad Manager文档](https://support.google.com/admanager/answer/3289669?hl=en) 将Adobe添加为链接的数据管理平台(DMP)。
2. 在 [!DNL Google Ad Manager] 界面，转到 **[!UICONTROL 管理员]** > **[!UICONTROL 全局设置]** > **[!UICONTROL 网络设置]**，并启用 **[!UICONTROL API访问]** 滑块。


## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). 在目标配置工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL 访问密钥ID]**:由61个字符组成的字母数字字符串，用于验证您的 [!DNL Google Cloud Storage] 帐户到平台。
* **[!UICONTROL 密钥访问密钥]**:一个40个字符、base64编码的字符串，用于验证您的 [!DNL Google Cloud Storage] 帐户到平台。

有关这些值的更多信息，请参阅 [Google云存储HMAC密钥](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 的双曲余切值。 有关如何生成您自己的访问密钥ID和密钥的步骤，请参阅 [[!DNL Google Cloud Storage] 源概述](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="将分段 ID 附加到分段名称"
>abstract="选择此选项可让 Google Ad Manager 360 中的区段名称包含来自 Experience Platform 的区段 ID，如下所示：`Segment Name (Segment ID)`"

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。 例如，您可以提及您使用此目标的促销活动。
* **[!UICONTROL 文件夹路径]**:输入将托管导出文件的目标文件夹的路径。
* **[!UICONTROL 存储段名称]**:输入 [!DNL Google Cloud Storage] 存储段供此目标使用。
* **[!UICONTROL 帐户ID]**:输入 [!DNL Audience Link ID] 从 [!DNL Google] 帐户。 这是与 [!DNL Google Ad Manager] 网络 [!DNL Network code])。 您可以在 **[!UICONTROL 管理员>全局设置]** 在 [!DNL Google Ad Manager] 界面。
* **[!UICONTROL 帐户类型]**:根据 [!DNL Google] 帐户：
   * 使用 `AdX buyer` 表示 [!DNL Google AdX]
   * 使用 `DFP by Google` 表示 [!DNL DoubleClick] （发布者）
* **[!UICONTROL 将区段ID附加到区段名称]**:选择此选项，使Google Ad Manager 360中的区段名称包含来自Experience Platform的区段ID，如下所示： `Segment Name (Segment ID)`.

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

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

## 故障排除 {#troubleshooting}

如果您在使用此目标时遇到任何错误，并且需要联系到Adobe或Google，请保留以下ID。

这些是Adobe的Google帐户ID:

* **[!UICONTROL 帐户ID]**:87933855
* **[!UICONTROL 客户ID]**:89690775