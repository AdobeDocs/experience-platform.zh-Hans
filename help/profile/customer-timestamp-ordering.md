---
title: 客户时间戳排序
description: 了解如何向数据集添加客户时间戳排序，以确保用户档案数据的一致性。
badgePrivateBeta: label="私人测试版" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c5789b872be49c3bd4a1ca61a2d44392ebd4a746
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# 客户时间戳排序

在Adobe Experience Platform中，在通过流式摄取摄取引入数据到配置文件存储区时，无法自动保证数据顺序。 通过客户时间戳订购，您可以保证最新消息（根据提供的客户时间戳）将保留在配置文件存储中。 因此，这可以使您的配置文件数据保持一致，并使您的配置文件数据与源系统保持同步。

要启用客户时间戳订购，您需要使用 `lastUpdatedDate` 中的字段 [外部源系统审计属性数据类型](../xdm/data-types/external-source-system-audit-attributes.md) 并提供沙盒和数据集信息，与您的Adobe技术客户经理或Adobe客户关怀团队联系。

## 约束

在此专用测试版中，使用客户时间戳订购时存在以下限制：

- 您只能将客户时间戳排序与 **配置文件属性** 引入于 **流式摄取**.
- 您只能在以下位置使用客户时间戳排序： **非生产** 沙箱。
- 您只能将客户时间戳排序应用于 **5** 每个沙盒的数据集。
- 此 `lastUpdatedDate` 字段必须在 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 格式。
- 已摄取的所有数据行 **必须** 包含 `lastUpdatedDate` 字段。 如果此字段缺失或格式不正确，摄取将失败。
- 为客户时间戳排序启用的任何数据集 **必须** 是一个新数据集，没有以前摄取的任何数据。
- 对于任何给定的配置文件片段，仅限包含更近的行 `lastUpdatedDate` 将被摄取。 如果行不包含更近的 `lastUpdatedDate`，则会丢弃该行。

## 推荐

在实施客户时间戳订购时，请牢记以下注意事项：

- 您负责同步所有内部系统上的时钟，将数据发送到配置文件存储区。
- 在ISO 8061格式的时间戳中，您的精度应该为毫秒级。
- 配合使用数据准备和客户时间戳订购可以 **强烈建议**，它会创建所有已摄取行的副本及其时间戳，以便在出现问题时更好地调试。
