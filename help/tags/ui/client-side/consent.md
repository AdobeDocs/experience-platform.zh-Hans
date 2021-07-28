---
title: 部署用于管理客户同意的JavaScript标记
description: 了解如何在Adobe Experience Platform中管理各种Adobe解决方案的客户选择加入和选择退出信号。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 77%

---

# 部署JavaScript标记以管理客户同意

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../term-updates.md)。

欧盟[《通用数据保护条例》(GDPR)](https://gdpr-info.eu/art-7-gdpr/) 和 [ePrivacy](https://medium.com/mydata/consent-lost-gdpr-and-found-eprivacy-e85cf881ffb) 法规要求公司能够管理其用户的知情同意。Adobe客户在为任何给定访客执行Adobe解决方案之前，可能会要求访客选择加入。 访客应该能够管理其“选择启用”和“选择禁用”状态。

Adobe Experience Cloud客户需要对这些要求进行多种实施。 有些客户使用企业级同意管理器，而其他客户则构建自己的同意管理器。

Adobe Experience Platform扩展开发人员使用扩展和规则生成器来定义选择启用和选择禁用解决方案。

本文档介绍了有关如何在获得同意之前阻止触发 Adobe 标记的信息。

## Advertising Cloud

Adobe Experience Platform不会自动触发[!DNL Advertising Cloud]。 仅当您在规则操作中明确给出指示时，[!DNL Advertising Cloud] 才会触发。可使用规则条件确定触发的时间和内容。例如，要使用 Cookie 确定“选择启用”状态，可设置一个数据元素来读取该 Cookie 并将其用作规则中的条件，以便确定何时触发 Track Conversion 操作。

与同意管理器（例如 OneTrust）的集成可以设置和跟踪客户的同意 Cookie，然后可以在规则生成器中使用它们。

## Analytics

在 [!DNL Analytics] 扩展配置设置的 Link Tracking 部分中，确保&#x200B;*未*&#x200B;选择以下设置：

* Track download links
* Track outbound links

未选择这些设置时，Platform不会自动触发[!DNL Adobe Analytics]。 仅当您在规则操作中明确给出指示时，[!DNL Analytics] 才会触发。可使用规则条件确定触发的时间和内容。例如，要使用 Cookie 确定“选择启用”状态，可设置一个数据元素来读取该 Cookie 并将其用作规则中的条件，以便确定何时触发 Send Beacon 操作。

另外，您可以考虑使用 [Adobe 选择启用对象](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hans)来控制此标记的触发，以便与您的同意管理平台相一致。

与同意管理器（例如 OneTrust）的集成可以设置和跟踪客户的同意 Cookie，然后可以在规则生成器中使用它们。

## Audience Manager

如果将 DIL 置于客户页面上，则 DIL 当前会设置为自动触发。请考虑使用 [Adobe 选择启用对象](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html)来控制此标记的触发，以便与您的同意管理平台相一致。

[!DNL Adobe] 建议您在 [!DNL Analytics] 内使用服务器端转发。

## Experience Cloud ID

如果将 [!DNL Experience Cloud ID] 置于客户页面上，则其当前会自动触发。

请考虑使用 [Adobe 选择启用对象](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html)来控制此标记的触发，以便与您的同意管理平台相一致。

## Target

Adobe Experience Platform不会自动触发[!DNL Target]。 仅当您在规则操作中明确给出指示时，[!DNL Target] 才会触发。可使用规则条件确定触发的时间和内容。例如，要使用 Cookie 确定“选择启用”状态，可设置一个数据元素来读取该 Cookie 并将其用作规则中的条件，以便确定何时触发 Load [!DNL Target] 操作。

另外，您可以考虑使用 [Adobe 选择启用对象](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html)来控制此标记的触发，以便与您的同意管理平台相一致。

与同意管理器（例如 OneTrust）的集成可以设置和跟踪客户的同意 Cookie，然后可以在规则生成器中使用它们。
