---
title: 部署JavaScript标记以管理客户同意
description: 了解如何在Adobe Experience Platform中管理各种Adobe解决方案的客户选择启用和选择禁用信号。
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 79%

---

# 部署JavaScript标记以管理客户同意

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

《通用数据保护条例》(GDPR)等隐私法规要求公司能够管理其用户的同意。 在为任何给定访客执行Adobe解决方案之前，Adobe客户可能会要求访客选择启用。 访客应该能够管理其“选择启用”和“选择禁用”状态。

Adobe Experience Cloud客户需要以各种方式实施这些要求。 有些客户使用企业级同意管理器，而其他客户则构建自己的同意管理器。

Adobe Experience Platform扩展开发人员使用扩展和规则生成器，来定义“选择启用”和“选择禁用”解决方案。

本文档介绍了有关如何在获得同意之前阻止触发 Adobe 标记的信息。

## Advertising Cloud

Adobe Experience Platform不会自动触发[!DNL Advertising Cloud]。 仅当您在规则操作中明确给出指示时，[!DNL Advertising Cloud] 才会触发。可使用规则条件确定触发的时间和内容。例如，要使用 Cookie 确定“选择启用”状态，可设置一个数据元素来读取该 Cookie 并将其用作规则中的条件，以便确定何时触发 Track Conversion 操作。

与同意管理器（例如 OneTrust）的集成可以设置和跟踪客户的同意 Cookie，然后可以在规则生成器中使用它们。

## Analytics

在 [!DNL Analytics] 扩展配置设置的 Link Tracking 部分中，确保&#x200B;*未*&#x200B;选择以下设置：

* Track download links
* Track outbound links

未选择这些设置时，Experience Platform不会自动触发[!DNL Adobe Analytics]。 仅当您在规则操作中明确给出指示时，[!DNL Analytics] 才会触发。可使用规则条件确定触发的时间和内容。例如，要使用 Cookie 确定“选择启用”状态，可设置一个数据元素来读取该 Cookie 并将其用作规则中的条件，以便确定何时触发 Send Beacon 操作。

另外，您可以考虑使用 [Adobe 选择启用对象](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hans)来控制此标记的触发，以便与您的同意管理平台相一致。

与同意管理器（例如 OneTrust）的集成可以设置和跟踪客户的同意 Cookie，然后可以在规则生成器中使用它们。

## Audience Manager

如果将 DIL 置于客户页面上，则 DIL 当前会设置为自动触发。请考虑使用 [Adobe 选择启用对象](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hans)来控制此标记的触发，以便与您的同意管理平台相一致。

[!DNL Adobe] 建议您在 [!DNL Analytics] 内使用服务器端转发。

## Experience Cloud ID

如果将 [!DNL Experience Cloud ID] 置于客户页面上，则其当前会自动触发。

请考虑使用 [Adobe 选择启用对象](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hans)来控制此标记的触发，以便与您的同意管理平台相一致。

## 目标

Adobe Experience Platform不会自动触发[!DNL Target]。 仅当您在规则操作中明确给出指示时，[!DNL Target] 才会触发。可使用规则条件确定触发的时间和内容。例如，要使用 Cookie 确定“选择启用”状态，可设置一个数据元素来读取该 Cookie 并将其用作规则中的条件，以便确定何时触发 Load [!DNL Target] 操作。

另外，您可以考虑使用 [Adobe 选择启用对象](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hans)来控制此标记的触发，以便与您的同意管理平台相一致。

与同意管理器（例如 OneTrust）的集成可以设置和跟踪客户的同意 Cookie，然后可以在规则生成器中使用它们。
