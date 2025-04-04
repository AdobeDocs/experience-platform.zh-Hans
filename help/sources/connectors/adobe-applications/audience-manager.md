---
keywords: Experience Platform；主页；热门主题；Audience Manager连接器；Audience Manager；Audience Manager
solution: Experience Platform
title: Audience Manager Source概述
description: Adobe Audience Manager源将在Audience Manager中收集的第一方数据流式传输到Adobe Experience Platform。
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 1%

---

# Audience Manager源

>[!IMPORTANT]
>
>在初始设置时，Adobe Audience Manager源会返回一条错误消息，说明具有给定`namespaceCode={VALUE}`的身份命名空间不存在。 **注意**：在后端，`namespaceCode`用于引用身份符号。 要完成集成，您必须：
>
>- [在身份服务中创建具有指定身份符号(`VALUE`)的自定义命名空间](../../../identity-service/features/namespaces.md#create-custom-namespaces) 。
>- 重新摄取您的数据。

Adobe Audience Manager源可流式处理在Adobe Audience Manager中收集的第一方数据，以便在Adobe Experience Platform中激活。 Audience Manager源向Experience Platform摄取两种类型的数据：

- **实时数据：**&#x200B;在Audience Manager数据收集服务器上实时捕获的数据。 这些数据用于Audience Manager以填充基于规则的特征，并且会在最短延迟时间内出现在Experience Platform中。
- **配置文件数据：** Audience Manager使用实时和已载入的数据获取客户配置文件。 这些配置文件用于在区段实现时填充身份图和特征。

Audience Manager源将这些数据类型映射到Experience Data Model (XDM)架构，然后将它们发送到Experience Platform。 实时数据作为XDM ExperienceEvent数据发送，而配置文件数据作为XDM个人配置文件数据发送。

有关详细信息，请参阅[在UI中创建Audience Manager源连接](../../tutorials/ui/create/adobe-applications/audience-manager.md)指南。

## 什么是Experience Data Model (XDM)？

XDM是一个公开记录的规范，它提供了一个标准化框架，Experience Platform可按该框架组织客户体验数据。

遵守XDM标准可以统一合并客户体验数据，从而更轻松地提供数据和收集信息。

有关如何在Experience Platform中使用XDM的更多信息，请阅读[XDM系统概述](../../../xdm/home.md)。 要详细了解如何在配置文件之间构建XDM架构和事件结构，请阅读架构组合的[基础知识](../../../xdm/schema/composition.md)。

## XDM架构示例

以下是映射到Experience Platform中的XDM ExperienceEvent和XDM Individual Profile的Audience Manager结构示例。

### ExperienceEvent — 用于实时数据和已载入数据

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM个人资料 — 用于个人资料数据

![](images/aam-profile-xdm-for-profile-data.png)

有关如何将字段从Audience Manager映射到XDM的信息，请阅读有关[Audience Manager映射字段](./mapping/audience-manager.md)的文档。

## Experience Platform上的数据管理

### 数据集

数据集是用于数据集合的存储和管理结构，通常是表，包含架构（列）和字段（行），并通过数据连接提供。 Audience Manager数据由实时数据、入站数据和配置文件数据组成。 要查找Audience Manager数据集，请在UI中使用搜索函数，并为每种类型的数据提供命名约定。

默认情况下，配置文件禁用Audience Manager数据集，用户能够根据自己的用例启用或禁用数据集。 建议不要禁用将用于配置文件中区段成员资格的数据集。

>[!NOTE]
>
>AAM Real-time是唯一进入数据湖的数据集。 所有其他Audience Manager数据集将转至[!DNL Profile]（如果已为[!DNL Profile]启用）。 如果未为[!DNL Profile]启用这些变量，则它们不会收到任何数据，并将显示为空。

| 数据集名称 | 描述 | 类 |
| --- | --- | --- |
| AAM Real-time | 此数据集包含由Audience Manager DCS端点的直接点击收集的数据以及Audience Manager配置文件的标识映射。 将此数据集保留为配置文件摄取启用。 | 体验事件 |
| AAM实时配置文件更新 | 此数据集可实时定位Audience Manager特征和区段。 其中包括有关Edge区域路由、特征和区段成员资格的信息。 将此数据集保留为配置文件摄取启用。 数据在数据集中不可见为批次。 您可以启用&#x200B;**[!UICONTROL 配置文件]**&#x200B;切换功能，以便直接将数据摄取到配置文件。 | 记录 |
| AAM设备数据 | 在Audience Manager中聚合的设备数据及其ECID和相应的区段实现。 数据在数据集中不可见为批次。 您可以启用&#x200B;**[!UICONTROL 配置文件]**&#x200B;切换功能，以便直接将数据摄取到配置文件。 | 记录 |
| AAM设备配置文件数据 | 用于Audience Manager连接器诊断。 数据在数据集中不可见为批次。 您可以启用&#x200B;**[!UICONTROL 配置文件]**&#x200B;切换功能，以便直接将数据摄取到配置文件。 | 记录 |
| AAM已验证的用户档案 | 此数据集包含Audience Manager已验证的用户档案。 数据在数据集中不可见为批次。 您可以启用&#x200B;**[!UICONTROL 配置文件]**&#x200B;切换功能，以便直接将数据摄取到配置文件。 | 记录 |
| AAM已验证的用户档案元数据 | 用于Audience Manager连接器诊断。 数据在数据集中不可见为批次。 您可以启用&#x200B;**[!UICONTROL 配置文件]**&#x200B;切换功能，以便直接将数据摄取到配置文件。 | 记录 |
| AAM设备数据回填 | 来自引入过去设备数据的数据集。 这包含在Audience Manager中聚合的ECID和相应的区段实现。 数据在数据集中不可见为批次。 您可以启用&#x200B;**[!UICONTROL 配置文件]**&#x200B;切换功能，以便将数据直接摄取到配置文件。 | 记录 |
| AAM已验证的用户档案回填 | 数据集来自引入过去的身份验证数据。 这包含Audience Manager已验证的用户档案。 数据在数据集中不可见为批次。 您可以启用&#x200B;**[!UICONTROL 配置文件]**&#x200B;切换功能，以便将数据直接摄取到配置文件。 | 记录 |

### 连接

Adobe Audience Manager在“目录：Audience Manager连接”中创建了一个连接。 目录是在Adobe Experience Platform中记录数据位置和族系的系统。 连接是一个目录对象，它是特定于客户的连接器实例。 有关目录、连接和连接器的详细信息，请阅读[目录服务概述](../../../catalog/home.md)。

### 区段人口对用户档案的影响

首次将Audience Manager区段发送到Experience Platform时，区段人口大小会直接影响用户档案编号。 这意味着选择所有区段可能会导致配置文件超出您的许可证使用授权。 Experience Platform还会从配置文件摄取的历史数据中区分新数据。 具有100个基于第一方的身份的区段将创建100个配置文件。 但是，如果该区段的人口增至150且被摄取到Experience Platform，则用户档案的数量将仅增加50个，因为只有50个新用户档案。

您还可以通过[许可证使用情况仪表板](../../../dashboards/guides/license-usage.md)检查您帐户可用的配置文件使用情况。

## Experience Platform上Audience Manager数据的预期滞后时间是多少？

| Audience Manager数据 | 类型 | 延迟 | 注释 |
| --- | --- | --- | --- |
| 实时数据 | 活动 | &lt;25分钟 | 从Audience Manager Edge节点捕获到显示在数据湖中的时间。 |
| 实时数据 | 配置文件更新 | &lt;10分钟 | 进入实时客户档案的时间。 |
| 实时数据和已载入数据 | 配置文件更新 | 24到36小时 | 从通过DCS/PCS Edge数据和载入的数据捕获、被处理到用户配置文件，然后出现在Real-Time Customer Profile中的时间。 目前，此数据不会直接进入数据湖。 可以为Audience Manager配置文件数据集启用配置文件切换，以便将此数据直接摄取到Real-time Customer Profile。 |
