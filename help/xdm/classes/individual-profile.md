---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；单个配置文件；字段；架构；架构；标识映射；标识映射；架构设计；映射；并集架构；并集架构
solution: Experience Platform
title: XDM Individual Profile Class
topic-legacy: overview
description: This document provides an overview of the XDM Individual Profile class.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 79fcc44ec5e08f63bfd5eed6e90d7538273f4dab
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] is a standard Experience Data Model (XDM) class which forms a singular representation (or &quot;profile&quot;) of an individual person. Specifically, the class (and its compatible field groups) captures the attributes and interests of both identified and partially identified individuals that interact with your brand.

配置文件可以包含匿名行为信号（如浏览器Cookie）和高度识别的配置文件，其中包含详细信息（如名称、出生日期、位置和电子邮件地址）。 As a profile grows, it becomes a robust repository of personal information, identities, contact details, and communication preferences for an individual. 有关在平台生态系统中使用此类的更多高级信息，请参阅[XDM概述](../home.md#data-behaviors)。

[!DNL XDM Individual Profile]类本身提供了几个系统生成的值，这些值在摄取数据时自动填充，而所有其他字段必须通过使用[兼容的架构字段组](#field-groups)来添加：

![](../images/classes/individual-profile.png)

| 属性 | 描述 |
| --- | --- |
| `_repo` | An object containing the following [!UICONTROL DateTime] fields: <ul><li>`createDate`:在数据存储中创建资源的日期和时间，例如首次摄取数据时。</li><li>`modifyDate`:上次修改资源的日期和时间。</li></ul> |
| `_id` | A unique string identifier for the record. 此字段用于跟踪单个记录的唯一性，防止重复数据，并在下游服务中查找该记录。 在某些情况下，`_id`可以是[通用唯一标识符(UUID)](https://tools.ietf.org/html/rfc4122)或[全局唯一标识符(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0)。<br><br>如果从源连接流式传输数据或直接从Parquet文件摄取数据，则应通过关联使记录具有唯一性的特定字段组合（如主ID、时间戳、记录类型等）来生成此值。连接值必须是带有`uri-reference`格式的字符串，这意味着必须删除任何冒号字符。 之后，连接值应使用SHA-256或您选择的其他算法进行哈希处理。<br><br>It is important to distinguish that **this field does not represent an identity related to an individual person**, but rather the record of data itself. Identity data relating to a person should be relegated to [identity fields](../schema/composition.md#identity) provided by compatible field groups instead. |
| `createdByBatchID` | 导致创建记录的摄取批次的ID。 |
| `modifiedByBatchID` | 导致记录更新的上次摄取的批处理的ID。 |
| `personID` | 与此记录相关的个人的唯一标识符。 This field does not necessarily represent an identity related to the person unless it is also designated as an [identity field](../schema/composition.md#identity). |
| `repositoryCreatedBy` | 创建记录的用户的ID。 |
| `repositoryLastModifiedBy` | 上次修改记录的用户ID。 |

{style=&quot;table-layout:auto&quot;}

## 兼容的字段组 {#field-groups}

>[!NOTE]
>
>多个字段组的名称已更改。 See the document on [field group name updates](../field-groups/name-updates.md) for more information.

Adobe提供了多个用于[!DNL XDM Individual Profile]类的标准字段组。 The following is a list of some commonly used field groups for the class:

* [[!UICONTROL 人口统计详细信息]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL 忠诚度详细信息]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL 个人联系详细信息]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL 隐私/个性化/营销首选项（同意）]](../field-groups/profile/consents.md)
* [[!UICONTROL 区段成员资格详细信息]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Work Contact Details]](../field-groups/profile/work-contact-details.md)

有关[!DNL XDM Individual Profile]的所有兼容字段组的完整列表，请参阅[XDM GitHub存储库](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile)。
