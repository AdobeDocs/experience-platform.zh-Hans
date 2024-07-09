---
title: Audience Analysis目标
description: 在Customer Journey Analytics中查看客户符合条件的受众。
badgeLimitedAvailability: label="限量发布版" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 3%

---

# Audience Analysis目标

此 [!UICONTROL 受众分析] 目标允许您将Adobe Experience Platform受众数据扩充到 [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hans). 您可以选择要在生成的扩充数据中包含的受众。 然后，受众资格可用作中的维度 [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html) 报表。

>[!AVAILABILITY]
>
>此目标处于有限测试阶段。 如果您有兴趣使用此目标，请联系您的Adobe客户团队。

## 先决条件

使用此目标之前需要执行以下操作：

* 您必须进行配置才能使用Audience Analysis目标。 如果您尚未配置为使用此目标，请与您的Adobe客户团队联系。
* 您必须进行配置才能使用Customer Journey Analytics。
* 您必须在Adobe Experience Platform中至少创建一个受众。

## 支持的身份

Audience Analysis支持激活下表中描述的标识。 了解有关 [身份](/help/identity-service/features/namespaces.md). 通常使用Experience CloudID (ECID)。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 请参阅以下文档： [ECID](/help/identity-service/features/ecid.md) 以了解更多信息。 |
| phone_sha256 | 使用SHA256算法散列的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。 |
| extern_id | 自定义用户标识 | 当源身份是自定义命名空间时，请选择此目标身份。 |

{style="table-layout:auto"}

## 支持的受众

使用此目标时，支持以下类型的受众：

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ {\f13 } | 受众 [已导入](../../../segmentation/ui/audience-portal.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出具有Audience Analysis目标中所用标识符（姓名、电话号码或其他）的受众所有成员。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 当基于受众评估在Experience Platform中更新用户档案时，连接器将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 配置新目标

>[!IMPORTANT]
> 
>要创建目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要创建此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 目标详细信息

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：目标名称。
* **[!UICONTROL 描述]**：目标描述。
* **[!UICONTROL 数据流ID]**：要与符合条件的受众扩充的数据流ID。 您可以在以下位置获取此ID： [数据流管理器](/help/datastreams/overview.md).
* **[!UICONTROL 集成别名]**：集成别名。

### 警报

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

* **[!UICONTROL 激活跳过率超过]**：在激活跳过率超过阈值时通知。

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

### 治理策略和实施行动

此可选部分允许您定义数据管理策略，并确保在发送和激活受众时使用的数据符合要求。

完成选择目标所需的营销操作后，选择 **[!UICONTROL 创建]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

创建目标后，您可以为该目标激活所需的受众。

1. 如果您不在创建的目标中，则可以通过导航到 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]**.
1. 选择 **[!UICONTROL 激活受众]**.
1. 选择要为其分析资格的所需受众。 完成后，选择 **[!UICONTROL 下一个]**.
1. 查看目标配置和受众设置，然后选择 **[!UICONTROL 完成]**.

您可以通过导航回 **[!UICONTROL 激活受众]** 页面。 激活受众后，您无法删除这些受众。
