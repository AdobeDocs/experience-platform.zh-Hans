---
title: 使用AI助手发现XDM字段
description: 请阅读本文档，了解如何使用AI Assistant进行Experience Data Model (XDM)字段发现。
badge: Alpha
hide: true
hidefromtoc: true
exl-id: 041034c6-da45-437f-ad46-f9c2ded9f82c
source-git-commit: 58cf5d90d70239a4b47c600bd3a7a37129b07dc3
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# 使用AI助手发现XDM字段

>[!AVAILABILITY]
>
>此功能已Alpha，可能不可用于您的组织。 要参与Alpha计划并访问此功能，请联系您的Adobe客户团队。

您可以使用AI Assistant搜索和发现Experience Data Model (XDM)字段，然后使用这些字段在Experience Platform中创建目标受众。

请阅读下表，了解AI Assistant中XDM字段发现支持的查询和提示模式。

>[!TIP]
>
>虽然在不同的用例中查询和提示模式可能相同，但问题的确切表述将因用于给定沙盒的XDM字段和架构而异。

| 查询类型 | 查询/提示模式 | 示例 |
| --- | --- | --- |
| 按数据域或区域的XDM字段发现 | 显示用于表示{DATA_DOMAIN/AREA}的XDM字段。 | <ul><li>显示用于表示同意数据的XDM字段。</li><li>显示用于表示电子邮件订阅信息的XDM字段。</li></ul> |
| 按常规字段名称发现XDM字段 | <ul><li>显示与{DATA_DOMAIN/AREA}相关的XDM字段。</li><li>哪些XDM字段包含{GENERAL_FIELD_NAME}。</li></ul> | <ul><li>显示与订单相关的XDM字段。</li><li>显示与交互详细信息相关的XDM字段。</li><li>哪个XDM字段包含访客ID？</li><li>哪个XDM字段包含产品类别？</li></ul> |
| 按数据模型谱系发现XDM字段 | <ul><li>向我显示包含{GENERAL_FIELD_NAME}的{FIELD_GROUP/CLASS_NAME}的所有字段。</li><li>XDM字段{GENERAL_FIELD_NAME}的{FIELD_GROUP/CLASS_NAME}是什么？</li></ul> | <ul><li>显示包含产品数据的字段组的所有字段。</li><li>显示包含分析数据的字段组的所有字段。</li><li>XDM字段名字的类是什么？</li><li>XDM字段电子邮件订阅的类是什么？</li></ul> |
| 提示获取增强的描述以及字段名称 | {FIELD_DISCOVERY_QUERY}。 还包括增强的描述。 | <ul><li>显示用于表示同意数据的XDM字段。 还包括字段的增强型描述。</li><li>显示与交互详细信息相关的XDM字段。 还包括字段的增强型描述。</li></ul> |

{style="table-layout:auto"}
