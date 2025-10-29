---
title: Adform
description: Adform是程序化媒体购买和销售解决方案的领先提供商。 将Adform连接到Adobe Experience Platform后，您可以通过基于Experience Cloud ID (ECID)的Adform激活第一方受众。
last-substantial-update: 2025-10-23T00:00:00Z
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 3%

---


# Adform连接 {#adform}

## 概述 {#overview}

Adform是程序化媒体购买和销售解决方案的领先提供商。 将Adform连接到Adobe Experience Platform后，您可以通过基于Experience Cloud ID (ECID)的Adform激活第一方受众。

>[!IMPORTANT]
>
>目标连接器和文档页面由Adform团队创建和维护。 如有任何查询或更新请求，请直接通过`support@adform.com`联系他们。

## 用例 {#use-cases}

为了帮助您更好地了解应如何使用Adform目标以及何时使用，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### Adobe Real-Time CDP audience activation {#use-case-1}

使用此目标可根据Adobe Real-Time CDP ID (ECID)和Adform的ID Fusion将Experience Cloud受众发送到Adform以进行激活。 Adform的ID Fusion是Adform的ID解析服务，允许您根据Experience Cloud ID (ECID)激活第一方受众。

一种常见的情况是，根据Experience Cloud ID (ECID)将网站访客重新定位到您的网站或应用程序。 您只需通过现成的[事件流](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking)或[客户端](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/analytics/adform) Adform扩展将Experience Cloud ID (ECID)发送到Adform。 之后，您可以通过Adform激活目标与Adform共享受众 — 完全基于Experience Cloud ID (ECID)。

## 先决条件 {#prerequisites}

* 您必须是现有Adform客户才能使用此目标。
* 您需要拥有Adform Audience Base数据连接凭据。
   * 如果您没有Adform Audience Base数据连接凭据，请联系您的Adform代表。
* 要正确同步，您需要具有从实体到Adform站点跟踪的[事件流](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking)或[客户端](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/analytics/adform)连接。
   * 如果您没有从实体到Adform站点跟踪的事件流或客户端连接，请联系您的Adform代表。
   * Adform为[事件流](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking)和[客户端](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/analytics/adform)提供了Adobe Experience Cloud扩展。


## 支持的身份 {#supported-identities}

Adform支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 有关详细信息，请参阅[ECID](/help/identity-service/features/ecid.md)上的以下文档。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/overview.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Segment export]** | 您正在导出区段（受众）的所有成员，其中包含&#x200B;*YourDestination*&#x200B;目标中使用的标识符（姓名、电话号码或其他）。 |
| 导出频率 | **[!UICONTROL Batch]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证目标，请填写必填字段并选择&#x200B;**[!UICONTROL Connect to destination]**。

![对目标进行身份验证](../../assets/catalog/advertising/adform/authenticate-destination.png)

* **[!UICONTROL Account name]**：输入一个帐户名称，以后可以通过它识别此目标连接。
* **[!UICONTROL S3 Access Key ID]**：填写由Adform提供的S3访问密钥。
* **[!UICONTROL S3 Secret Access Key]**：填写由Adform提供的S3访问密钥。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![填写目标详细信息](../../assets/catalog/advertising/adform/configure-destination-details.png)

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Provider Name]**：您的Adform帐户名由Adform提供。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众区段激活到此目标的说明，请阅读[将受众数据激活到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)。

### 映射属性和身份 {#map}

* **ECID** (Experience Cloud ID)

在映射步骤中，仅使用[!DNL ECID]目标标识映射。 请勿包含任何其他标识字段，因为这样会阻止成功完成激活。

## 导出的数据/验证数据导出 {#exported-data}

目标连接器只将ECID身份导出到目标。 不导出任何其他标识。 要检查数据导出是否成功，请登录您的Adform受众基础帐户，并检查受众是否可用。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。

## 其他资源 {#additional-resources}

有关Adform受众基础的其他信息，请参阅[Adform受众基础文档](https://www.adformhelp.com/hc/en-us/categories/9738365991697-Data-Management-Platform)。