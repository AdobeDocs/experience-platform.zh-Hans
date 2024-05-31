---
title: 客户时间戳排序
description: 了解如何向数据集添加客户时间戳排序，以确保用户档案数据的一致性。
badgePrivateBeta: label="私人测试版" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: f73b7ac38c681ec5161e2b5e7075f31946a6563e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# 客户时间戳排序

在Adobe Experience Platform中，默认情况下，当通过流式摄取摄取引入数据到配置文件存储区时，无法保证数据顺序。 通过客户时间戳订购，您可以保证最新消息（根据提供的客户时间戳）将保留在配置文件存储中。 所有过时的消息随后将被丢弃，并且 **非** 可用于使用个人资料数据（如分段和目标）的下游服务。 因此，这可以使您的配置文件数据保持一致，并使您的配置文件数据与源系统保持同步。

要启用客户时间戳排序，请使用 `extSourceSystemAudit.lastUpdatedDate` 中的字段 [外部源系统审计属性数据类型](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/shared/external-source-system-audit-details.schema.md) 并提供沙盒和数据集信息，与您的Adobe技术客户经理或Adobe客户关怀团队联系。

## 约束

在此专用测试版中，使用客户时间戳订购时存在以下限制：

- 您只能将客户时间戳排序与 **配置文件属性** 引入于 **流式摄取** 配置文件存储区中的。
   - 有 **否** 订购为数据湖或Identity服务中的数据提供的保证。
- 您只能在以下位置使用客户时间戳排序： **非生产** 沙箱。
- 您只能将客户时间戳排序应用于 **5** 每个沙盒的数据集。
- 您 **无法** 使用流式更新插入在启用了客户时间戳排序的数据集中发送部分行更新。
- 此 `extSourceSystemAudit.lastUpdatedDate` 字段 **必须** 在 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 格式。 使用ISO 8601格式时， **必须** 格式为的完整日期时间 `yyyy-MM-ddTHH:mm:ss.sssZ` (例如， `2028-11-13T15:06:49.001Z`)。
- 已摄取的所有数据行 **必须** 包含 `extSourceSystemAudit.lastUpdatedDate` 字段作为顶级字段组。 这意味着该字段 **必须** 未嵌套在XDM架构中。 如果此字段缺失或格式不正确，则格式错误的记录将 **非** ，并将发送相应的错误消息。
- 为客户时间戳排序启用的任何数据集 **必须** 是一个新数据集，没有以前摄取的任何数据。
- 对于任何给定的配置文件片段，仅限包含更近的行 `extSourceSystemAudit.lastUpdatedDate` 将被摄取。 包含 `extSourceSystemAudit.lastUpdatedDate` 大于或等于此年龄的用户将被丢弃。

## 推荐

在实施客户时间戳订购时，请牢记以下注意事项：

- 您负责同步所有内部系统的时钟，将数据发送到配置文件存储区。
- 在ISO 8061格式的时间戳中，您的精度应该为毫秒级。
