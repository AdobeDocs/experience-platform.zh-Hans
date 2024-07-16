---
title: XDM单个潜在客户配置文件类
description: 了解Experience Data Model (XDM)中的XDM Individual Prospect Profile类。
exl-id: 10fd9d16-4123-4ad4-971f-b715231ee6a9
source-git-commit: f4ddcf14de7a5cec42b5ebc521203cfdd1498a9f
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# [!UICONTROL XDM单个潜在客户配置文件]类

在Experience Data Model (XDM)中，[!UICONTROL XDM Individual Profile]类捕获通常来自漏斗顶端客户获取用例的数据合作伙伴的目标客户配置文件。

>[!NOTE]
>
>要将XDM单个潜在客户配置文件中的字段设置为身份，您必须首先创建至少一个合作伙伴ID命名空间。 阅读[标识类型部分](../../identity-service/features/namespaces.md)，了解有关合作伙伴 ID 命名空间的更多信息。

![XDM潜在客户类的架构图。](../images/classes/individual-prospect-profile.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_repo` | 对象 | 此类使您能够引入来自数据供应商的潜在客户配置文件，以漏斗客户获取用例。 |
| `_repo.createDate` | [!UICONTROL 日期时间] | 在存储库中创建资源的服务器日期和时间。 创建时间可以是首次上传资源文件时，也可以是服务器将目录作为新资源的父级时。 日期时间属性应符合ISO 8601标准。 例如，“2004-10-23T12:00:00-06:00”。 |
| `_repo.modifyDate` | [!UICONTROL 日期时间] | 在存储库中上次修改资源的服务器日期和时间，例如，在上传新版本的资产或添加或删除目录的子资源时。 日期时间属性应符合ISO 8601标准。 示例形式为“2004-10-23T12:00:00-06:00”。 |
| `_id` | [!UICONTROL 字符串] | 系统为记录生成的唯一字符串标识符。 此字段用于跟踪单个记录的唯一性，防止数据重复，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此它在数据摄取期间不提供显式值。 但是，您可以根据需要选择提供自己的唯一ID值。 |
| `createdByBatchID` | [!UICONTROL 字符串] | 导致创建记录的摄取批次的ID。 |
| `modifiedByBatchID` | [!UICONTROL 字符串] | 导致更新记录的上次摄取批次的ID。 |
| `partnerID` | [!UICONTROL 字符串] | 通常，用于标识单个潜在客户的唯一假名标识符。 请参阅有关[身份类型](../../identity-service/features/namespaces.md#identity-type)的文档，以了解有关合作伙伴ID以及Adobe Experience Platform中可用的其他身份类型的更多信息。 |
| `repositoryCreatedBy` | [!UICONTROL 字符串] | 创建记录的用户的ID。 |
| `repositoryLastModifiedBy` | [!UICONTROL 字符串] | 上次修改记录的用户的ID。 创建记录时，`modifiedByUser`值设置为`createdByUser`值。 |

{style="table-layout:auto"}
