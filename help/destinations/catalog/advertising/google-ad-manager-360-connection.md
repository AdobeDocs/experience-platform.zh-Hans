---
title: (Beta) [!DNL Google Ad Manager 360] 连接
description: Google Ad Manager 360是Google的一个广告投放平台，它使发布者能够通过视频和移动应用程序管理其网站上的广告显示。
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 4%

---

# (Beta)[!DNL Google Ad Manager 360]连接

## 概述 {#overview}

此 [!DNL Google Ad Manager 360] 连接允许批量上传 [!DNL publisher provided identifiers] (PPID)到 [!DNL Google Ad Manager 360]，通过 [!DNL Google Cloud Storage].

有关发布者提供的标识符如何在Google Ad Manager 360中工作的更多详细信息，请参阅 [Google官方文档](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>此目标目前为测试版，仅适用于有限数量的客户。 要请求访问 [!DNL Google Ad Manager 360] 连接，请联系您的Adobe代表并提供您的 [!DNL organization ID].

此 [!DNL Google Ad Manager 360] 目标导出 [!DNL CSV] 文件到您的 [!DNL Google Cloud Storage] 桶。 导出 [!DNL CSV] 文件，您必须将这些文件导入 [!DNL Google Ad Manager 360] 帐户。

## 目标详情 {#specifics}

请注意以下特定于的详细信息 [!DNL Google Ad Manager 360] 目标。

* 激活的受众是在Google平台中以编程方式创建的，并在CSV文件中填充。

## 支持的身份 {#supported-identities}

[!DNL This integration] 支持激活下表中描述的标识。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | 选择要将受众发送到的此目标身份 [!DNL Google Ad Manager 360] |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍可以导出到此目标的所有受众。

所有目标都支持激活通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md).

此外，此目标还支持激活下表中描述的受众。

| 受众类型 | 描述 |
---------|----------|
| 自定义上传 | 从CSV文件引入到Experience Platform中的受众。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及适用的架构字段（例如PPID），如在 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标将文件导出到下游平台，增量为3、6、8、12或24小时。 详细了解 [基于文件的批处理目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

### 允许列表 {#allow-listing}

必须先将添加到允许列表，然后才能设置您的第一个 [!DNL Google Ad Manager 360] Platform的目标。 在创建目标之前，请确保完成如下所述的允许列表流程。

>[!NOTE]
>
>此规则的例外情况适用于现有 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 客户。 如果您已在Audience Manager中创建了到此Google目标的连接，则无需再次完成允许列表过程，您可以继续后续步骤。

1. 请按照 [Google Ad Manager文档](https://support.google.com/admanager/answer/3289669?hl=en) 将Adobe添加为链接的数据管理平台(DMP)。
2. 在 [!DNL Google Ad Manager] 界面，转到 **[!UICONTROL 管理员]** > **[!UICONTROL 全局设置]** > **[!UICONTROL 网络设置]**，并启用 **[!UICONTROL API访问]** 滑块。


## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). 在目标配置工作流中，填写下面两节中列出的字段。

### 向目标进行身份验证 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL 访问密钥ID]**：由61个字符组成的字母数字字符串，用于验证您的 [!DNL Google Cloud Storage] Platform帐户。
* **[!UICONTROL 访问密钥]**：由40个字符组成的base64编码字符串，用于验证您的 [!DNL Google Cloud Storage] Platform帐户。

有关这些值的更多信息，请参见 [Google Cloud Storage HMAC密钥](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 指南。 有关如何生成您自己的访问密钥ID和秘密访问密钥的步骤，请参阅 [[!DNL Google Cloud Storage] 源概述](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="将受众 ID 附加到受众名称"
>abstract="选择此选项可让 Google Ad Manager 360 中的受众名称包含来自 Experience Platform 的受众 ID，如下所示：`Audience Name (Audience ID)`"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：填写此目标的首选名称。
* **[!UICONTROL 描述]**：可选。 例如，您可以提及要将此目标用于哪个营销活动。
* **[!UICONTROL 文件夹路径]**：输入将托管导出文件的目标文件夹的路径。
* **[!UICONTROL 存储段名称]**：输入 [!DNL Google Cloud Storage] 要由此目标使用的存储段。
* **[!UICONTROL 帐户ID]**：输入您的 [!DNL Audience Link ID] 来自您的 [!DNL Google] 帐户。 这是与您的关联的特定标识符 [!DNL Google Ad Manager] 网络(不是您的 [!DNL Network code])。 您可在下找到此内容 **[!UICONTROL 管理员>全局设置]** 在 [!DNL Google Ad Manager] 界面。
* **[!UICONTROL 帐户类型]**：选择一个选项，具体取决于 [!DNL Google] 帐户：
   * 使用 `AdX buyer` 对象 [!DNL Google AdX]
   * 使用 `DFP by Google` 对象 [!DNL DoubleClick] 发布者
* **[!UICONTROL 将受众ID附加到受众名称]**：选择此选项可使Google Ad Manager 360中的受众名称包含Experience Platform中的受众ID，如下所示： `Audience Name (Audience ID)`.

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

参见 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众激活到此目标的说明。

在身份映射步骤中，您可以看到以下预填充的映射：

| 预填充的映射 | 描述 |
|---------|----------|
| `ECID` -> `ppid` | 这是唯一一个用户可编辑的预填充映射。 您可以从Platform中选择任何属性或身份命名空间并将其映射到 `ppid`. |
| `metadata.segment.alias` -> `list_id` | 将Experience Platform受众名称映射到Google平台中的受众ID。 |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | 告知Google平台何时从区段中删除不合格的用户。 |

以下项需要这些映射 [!DNL Google Ad Manager 360] 和，由Adobe Experience Platform自动为所有 [!DNL Google Ad Manager 360] 连接。

![显示Google Ad Manager 360映射步骤的UI图像。](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## 导出的数据 {#exported-data}

要验证数据是否已成功导出，请查看 [!DNL Google Cloud Storage] 存储桶并确保导出的文件包含预期的用户档案人口。

## 故障排除 {#troubleshooting}

如果您在使用此目标时遇到任何错误，并且需要联系Adobe或Google，请随时保留以下ID。

这些是Adobe的Google帐户ID：

* **[!UICONTROL 帐户ID]**： 87933855
* **[!UICONTROL 客户ID]**： 89690775