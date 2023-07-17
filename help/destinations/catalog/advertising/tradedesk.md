---
keywords: 广告；交易台；广告交易台
title: 交易台连接
description: Trade Desk是一个自助服务平台，供广告购买者跨显示器、视频和移动库存源执行重定位和面向受众的数字活动。
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 1c9725c108d55aea5d46b086fbe010ab4ba6cf45
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 2%

---

# [!DNL The Trade Desk] 连接

## 概述 {#overview}

[!DNL The Trade Desk] 目标可帮助您将配置文件数据发送到 [!DNL The Trade Desk].

[!DNL The Trade Desk] 是一个自助服务平台，供广告购买者跨显示器、视频和移动库存源执行重定位和面向受众的数字活动。

要将配置文件数据发送到 [!DNL Trade Desk]，您必须先连接到目标。

## 用例 {#use-cases}

作为营销人员，我希望能够使用由构建的受众 [!DNL Trade Desk IDs] 或设备ID以创建重定位或面向受众的数字营销活动。

## 支持的身份 {#supported-identities}

[!DNL The Trade Desk] 支持激活下表中描述的标识。 详细了解 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| 交易台ID | Trade Desk平台中的广告商ID |

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
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在将受众的所有成员导出到目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
>如果您希望使用创建您的第一个目标 [!DNL The Trade Desk] 且尚未启用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 在过去(使用Adobe Audience Manager或其他应用程序)的Experience CloudID服务中，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前已设置 [!DNL The Trade Desk] Audience Manager中的集成，您设置的ID同步会转移到平台。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 必须提供以下信息，才能使用此目标：

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户ID]**：您的 [!DNL Trade Desk] [!UICONTROL 帐户ID].
* **[!UICONTROL 服务器位置]**：询问您的 [!DNL Trade Desk] 代表您应该使用哪个区域服务器。 这些是您可以从以下位置选择的可用区域服务器：
   * **[!UICONTROL 欧洲]**
   * **[!UICONTROL 新加坡]**
   * **[!UICONTROL 东京]**
   * **[!UICONTROL 北美东部]**
   * **[!UICONTROL 北美西部]**
   * **[!UICONTROL 拉丁美洲]**

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

参见 [将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

在 [受众计划](../../ui/activate-segment-streaming-destinations.md#scheduling) 步骤，您必须手动将受众映射到目标平台中它们对应的ID或友好名称。

在映射区段时，我们建议您使用Platform受众名称或它的较短形式，以方便使用。 但是，目标中的受众ID或名称不需要与Platform帐户中的受众ID或名称匹配。 您在映射字段中插入的任何值都将反映在目标中。

如果您使用多个设备映射(Cookie ID， [!DNL IDFA]， [!DNL GAID])，确保对所有三个映射使用相同的映射值。 [!DNL The Trade Desk] 会将所有这些请求汇总到单个区段中，并带有设备级别的细分。

![区段映射ID](../../assets/common/segment-mapping-id.png)

## 导出的数据 {#exported-data}

验证数据是否已成功导出到 [!DNL The Trade Desk] 目标，检查您的 [!DNL Trade Desk] 帐户。 如果激活成功，则会在您的帐户中填充受众。
