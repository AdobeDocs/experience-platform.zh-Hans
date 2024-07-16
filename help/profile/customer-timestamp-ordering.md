---
title: 客户时间戳排序
description: 了解如何向数据集添加客户时间戳排序，以确保用户档案数据的一致性。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1cd9f0b5-6334-4815-860a-78596a9cea1a
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 客户时间戳排序

在Adobe Experience Platform中，默认情况下，当通过流式摄取摄取引入数据到配置文件存储区时，无法保证数据顺序。 通过客户时间戳订购，您可以保证最新消息（根据提供的客户时间戳）将保留在配置文件存储中。 所有过时消息将被丢弃，并且&#x200B;**不**&#x200B;可用于使用分段和目标等配置文件数据的下游服务。 因此，这可以使您的配置文件数据保持一致，并使您的配置文件数据与源系统保持同步。

要启用客户时间戳排序，请使用[外部Source系统审核属性字段组](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md)中的`extSourceSystemAudit.lastUpdatedDate`字段，然后与您的Adobe技术客户经理联系或向Adobe客户关怀部门提供您的沙盒和数据集信息。

## 约束

在此专用测试版中，使用客户时间戳订购时存在以下限制：

- 您只能在配置文件存储区中对通过&#x200B;**流式引入**&#x200B;引入的&#x200B;**配置文件属性**&#x200B;使用客户时间戳排序。
   - 为Data Lake或Identity Service中的数据提供了&#x200B;**否**&#x200B;订购保证。
- 您只能在&#x200B;**非生产**&#x200B;沙盒上使用客户时间戳排序。
- 您只能对每个沙盒的&#x200B;**5**&#x200B;数据集应用客户时间戳排序。
- 您&#x200B;**无法**&#x200B;在启用了客户时间戳排序的数据集中使用流式更新插入发送部分行更新。
- `extSourceSystemAudit.lastUpdatedDate`字段&#x200B;**必须**&#x200B;采用[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)格式。 使用ISO 8601格式时，它&#x200B;**必须**&#x200B;作为完整日期时间，格式为`yyyy-MM-ddTHH:mm:ss.sssZ`（例如，`2028-11-13T15:06:49.001Z`）。
- 摄取的数据的所有行&#x200B;**必须**&#x200B;包含`extSourceSystemAudit.lastUpdatedDate`字段作为顶级字段组。 这意味着此字段&#x200B;**不能**&#x200B;嵌套在XDM架构中。 如果此字段缺失或格式不正确，将&#x200B;**不摄取格式错误的记录**，并将发送相应的错误消息。
- 为客户时间戳排序&#x200B;**启用的任何数据集必须**&#x200B;是没有任何先前摄取的数据的新数据集。
- 对于任何给定的配置文件片段，将仅摄取包含更近的`extSourceSystemAudit.lastUpdatedDate`的行。 将丢弃包含`extSourceSystemAudit.lastUpdatedDate`的旧版本或相同版本的行。

## 推荐做法

在实施客户时间戳订购时，请牢记以下注意事项：

- 您负责同步所有内部系统的时钟，将数据发送到配置文件存储区。
- 在ISO 8061格式的时间戳中，您的精度应该为毫秒级。
