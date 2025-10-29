---
title: Audience Analysis目标
description: 在Customer Journey Analytics中查看客户符合条件的受众。
badgeLimitedAvailability: label="限量发布版" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
hide: true
hidefromtoc: true
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 3%

---

# Audience Analysis目标

[!UICONTROL Audience Analysis]目标允许您将Adobe Experience Platform受众数据扩充到[Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hans)。 您可以选择要在生成的扩充数据中包含的受众。 然后，受众资格将作为维度出现在[Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html?lang=zh-Hans)报表中。

>[!AVAILABILITY]
>
>此目标处于有限测试阶段。 如果您有兴趣使用此目标，请联系您的Adobe客户团队。

## 先决条件

使用此目标之前需要执行以下操作：

* 您必须进行配置才能使用Audience Analysis目标。 如果您尚未配置为使用此目标，请联系您的Adobe客户团队。
* 您必须进行配置才能使用Customer Journey Analytics。
* 您必须在Adobe Experience Platform中至少创建一个受众。

## 支持的身份

Audience Analysis支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。 通常使用Experience Cloud ID (ECID)。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 有关详细信息，请参阅[ECID](/help/identity-service/features/ecid.md)上的以下文档。 |
| phone_sha256 | 使用SHA256算法散列的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以便在激活时自动对[!DNL Experience Platform]数据进行哈希处理。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以便在激活时自动对[!DNL Experience Platform]数据进行哈希处理。 |
| extern_id | 自定义用户标识 | 当源身份是自定义命名空间时，请选择此目标身份。 |

{style="table-layout:auto"}

## 支持的受众

使用此目标时，支持以下类型的受众：

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您正在导出具有Audience Analysis目标中所用标识符（姓名、电话号码或其他）的受众所有成员。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 当基于受众评估在Experience Platform中更新用户档案时，连接器会将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 配置新目标

>[!IMPORTANT]
> 
>要创建目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要创建此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 目标详细信息

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL Name]**：目标名称。
* **[!UICONTROL Description]**：目标描述。
* **[!UICONTROL Datastream ID]**：要与符合条件的受众扩充的数据流ID。 您可以在[数据流管理器](/help/datastreams/overview.md)中获取此ID。
* **[!UICONTROL Integration alias]**：集成别名。

### 警报

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

* **[!UICONTROL Activation Skipped Rate Exceed]**：当激活跳过率超过阈值时通知。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

### 治理策略和实施行动

此可选部分允许您定义数据管理策略，并确保在发送和激活受众时使用的数据符合要求。

完成选择目标所需的营销操作后，选择&#x200B;**[!UICONTROL Create]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

创建目标后，您可以为该目标激活所需的受众。

1. 如果您不在创建的目标中，则可以通过导航到&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Browse]**&#x200B;来再次找到它。
1. 选择 **[!UICONTROL Activate audiences]**。
1. 选择要为其分析资格的所需受众。 完成后，选择&#x200B;**[!UICONTROL Next]**。
1. 查看目标配置和受众设置，然后选择&#x200B;**[!UICONTROL Finish]**。

您可以通过导航回&#x200B;**[!UICONTROL Activate audiences]**&#x200B;页面来添加更多要在将来分析的受众。 激活受众后，您无法删除这些受众。
