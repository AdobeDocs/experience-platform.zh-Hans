---
keywords: 广告；交易台；广告交易台
title: 交易台连接
description: Trade Desk是一个自助服务平台，供广告购买者跨显示器、视频和移动库存源执行重定位和面向受众的数字活动。
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 564ee7fbd45677c35057c56de049158f3282d7ad
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 3%

---

# [!DNL The Trade Desk]连接

## 概述 {#overview}


>[!IMPORTANT]
>
> 从2025年7月开始，对目标服务进行[内部升级](../../../release-notes/2025/july-2025.md#destinations)后，在到&#x200B;**的数据流中，您可能会遇到激活的配置文件数**&#x200B;减少[!DNL The Trade Desk]的情况。
> &#x200B;> 导致此下降的原因是，针对此目标平台的所有激活引入了&#x200B;**ECID映射要求**。 有关详细信息，请参阅此页面中的[强制映射](#mandatory-mappings)部分。
>
>**更改内容：**
>
>* 现在，所有配置文件激活的ECID (Experience Cloud ID)映射都是&#x200B;**必需的**。
>* 没有ECID映射的配置文件将从现有激活数据流中&#x200B;**删除**。
>
>**您需要执行的操作：**
>
>* 查看您的受众数据，以确认用户档案具有有效的ECID值。
>* 监控您的激活量度以验证预期的配置文件计数。


使用此目标连接器将配置文件数据发送到[!DNL The Trade Desk]。 此连接器将数据发送到[!DNL The Trade Desk]第一方终结点。 Adobe Experience Platform与[!DNL The Trade Desk]之间的集成不支持将数据导出到[!DNL The Trade Desk]第三方端点。

[!DNL The Trade Desk]是一个自助服务平台，供广告购买者跨显示、视频和移动库存源执行重定位和面向受众的数字营销活动。

若要将配置文件数据发送到[!DNL The Trade Desk]，您必须先连接到目标，如本页的以下部分所述。

## 用例 {#use-cases}

作为营销人员，我希望能够使用基于[!DNL Trade Desk IDs]或设备ID构建的受众来创建重定位或面向受众的数字营销活动。

## 支持的身份 {#supported-identities}

[!DNL The Trade Desk]支持根据下表所示的标识激活受众。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

以下是[!DNL The Trade Desk]目标支持的标识。 这些标识可用于激活[!DNL The Trade Desk]的受众。

下表中的所有标识都是强制映射。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |
| ECID | Experience Cloud ID | 此身份是集成正常工作的必备条件，但不会用于受众激活。 |
| 交易台ID | [!DNL The Trade Desk]平台中的广告商ID | 在根据交易台的专有ID激活受众时，请使用此标识。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在将受众的所有成员导出到目标。 |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
>如果您希望使用[!DNL The Trade Desk]创建您的第一个目标，并且以前未在Experience Cloud ID服务(使用Adobe Audience Manager或其他应用程序)中启用[ID同步功能](https://experienceleague.adobe.com/zh-hans/docs/id-service/using/id-service-api/methods/idsync)，请联系Adobe Consulting或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了[!DNL The Trade Desk]集成，则您设置的ID同步将会转移到Experience Platform。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户ID]**：您的[!DNL The Trade Desk] [!UICONTROL 帐户ID]。
* **[!UICONTROL 服务器位置]**：询问您的[!DNL The Trade Desk]代表您应该使用哪个区域服务器。 以下是可供您选择的可用区域服务器：

   * **[!UICONTROL APAC]**
   * **[!UICONTROL 中国]**
   * **[!UICONTROL 东京]**
   * **[!UICONTROL 英国/欧盟]**
   * **[!UICONTROL 美国东岸]**
   * **[!UICONTROL 美国西海岸]**

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md)。

在[受众计划](../../ui/activate-segment-streaming-destinations.md#scheduling)步骤中，必须手动将受众映射到目标平台中其对应的ID或友好名称。

在映射受众时，Adobe建议您使用Experience Platform受众名称或其更短的形式，以便轻松使用。 但是，目标中的受众ID或名称不需要与Experience Platform帐户中的受众ID或名称匹配。 您在映射字段中插入的任何值都将反映在目标中。

### 强制映射 {#mandatory-mappings}

[支持的标识](#supported-identities)部分中描述的所有目标标识都是必需的，必须在受众激活过程中映射。 这包括：

* **GAID** (Google Advertising ID)
* **IDFA** (广告商的Apple ID)
* **ECID** (Experience Cloud ID)
* **交易台ID**

无法映射所有必需的标识，因而无法完成激活工作流。 每个标识在集成中均用于特定目的，而目标需要所有这些标识才能正常工作。

![显示必需映射的屏幕截图](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

## 导出的数据 {#exported-data}

要验证数据是否已成功导出到[!DNL The Trade Desk]目标，请检查您的[!DNL The Trade Desk]帐户。 如果激活成功，则会在您的帐户中填充受众。
