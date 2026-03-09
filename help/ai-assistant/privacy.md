---
title: AI助手中的隐私、安全和管理（旧版）
description: 了解AI助手（旧版）的隐私、安全和治理实践。
exl-id: 371e065d-c2dd-4233-b78e-a42757fce853
source-git-commit: 077c42f2190316a00168bbeca685c08677c2b13a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# AI助手中的隐私、安全和管理（旧版）

Adobe Experience Platform中的AI助手（旧版）构建时将隐私、安全和治理放在最前面。

请阅读本文档，了解您可以期待从AI Assistant（旧版）获得的以客户信任为中心的功能：

* 目前，即使用于培训目的，人工智能助理（旧版）也不使用任何个人数据。
* AI助手（旧版）不知道消费者数据。
* AI助手（旧版）将遵循所有现有[访问控制](../access-control/home.md)策略。
   * 任何基于属性的新访问控制策略最多在24小时后反映在AI助手（旧版）中*
* AI Assistant（旧版）在与Adobe Experience Platform Healthcare Shield结合使用时是HIPAA就绪功能。
* 您可以查看以前与AI助手（旧版）进行的交互的日志，保留策略为30天。
* AI助手（旧版）在响应用户提示时以特定于沙盒的数据和公共Adobe文档为基础。 数据不会在沙盒之间共享。
* 您提供给AI助手（旧版）的提示不会共享给其他客户。

**这意味着，如果向字段和对象添加任何新标签或创建任何新策略，则需要AI助手（旧版）最多24小时才能兑现它们。 在这24小时内，新受限制访问的用户仍然可以访问这些字段和对象。*
