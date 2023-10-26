---
title: 沙盒工具API指南
description: Adobe Experience Platform中的沙盒工具允许您在沙盒之间导出和导入沙盒配置的快照。
source-git-commit: e4e89c5250885bef177ba0d678629261a361a66d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 1%

---

# [!DNL Sandbox] 工具API指南

此 [!DNL Sandbox] 工具API提供了多个端点，允许您在组织内可用的沙盒之间导出和导入快照。 所有交互都通过HTTP端点进行。 在导出快照之前，将检查源沙盒中的工件，即包中包含的对象。 发出导入请求时， [!DNL Azure Blob] 获取快照并将其用作模板，以便为目标沙盒生成几乎类似的工件。 请参阅 [沙盒工具](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) 文档，其中列出了支持的对象和限制。

这些端点概述如下。 有关详细信息，请参阅各个端点指南，并参阅 [快速入门指南](./getting-started.md) 有关所需标头的重要信息，请阅读示例API调用等。

## 包 {#packages}

沙盒工具包端点允许您管理包。 沙盒工具包是工件定义的集合，包括包ID、名称、描述、组织ID和创建者ID。 请参阅 [包端点指南](./packages.md) 有关在API中使用包的详细信息。

## 工具 {#tools}

沙盒工具端点允许您单独获取作业JSON数据。 请参阅 [工具端点指南](./tools.md) 有关在API中检索作业JSON数据的更多信息。

## 后续步骤 {#next-steps}

要开始使用沙盒工具API进行调用，请阅读 [快速入门指南](./getting-started.md) 然后选择其中一个端点指南以了解如何使用特定端点。
