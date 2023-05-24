---
title: 部署JavaScript標籤以管理客戶同意
description: 瞭解如何在Adobe Experience Platform中管理各種Adobe解決方案的客戶選擇加入和選擇退出訊號。
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: 3bb0fc7b2807889d0a759e81c8ff728de3c0cbde
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 78%

---

# 部署JavaScript標籤以管理客戶同意

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

一般資料保護規範(GDPR)等法律隱私權法規要求公司能夠管理其使用者的同意宣告。 Adobe客戶在為任何特定訪客執行Adobe解決方案之前，可能會要求訪客選擇加入。 访客应该能够管理其“选择启用”和“选择禁用”状态。

Adobe Experience Cloud客戶對這些需求要求進行各種不同實施。 有些客户使用企业级同意管理器，而其他客户则构建自己的同意管理器。

Adobe Experience Platform擴充功能開發人員可使用擴充功能和規則產生器，定義選擇加入和選擇退出解決方案。

本文档介绍了有关如何在获得同意之前阻止触发 Adobe 标记的信息。

## Advertising Cloud

Adobe Experience Platform無法引發 [!DNL Advertising Cloud] 自動。 仅当您在规则操作中明确给出指示时，[!DNL Advertising Cloud] 才会触发。可使用规则条件确定触发的时间和内容。例如，要使用 Cookie 确定“选择启用”状态，可设置一个数据元素来读取该 Cookie 并将其用作规则中的条件，以便确定何时触发 Track Conversion 操作。

与同意管理器（例如 OneTrust）的集成可以设置和跟踪客户的同意 Cookie，然后可以在规则生成器中使用它们。

## Analytics

在 [!DNL Analytics] 扩展配置设置的 Link Tracking 部分中，确保&#x200B;*未*&#x200B;选择以下设置：

* Track download links
* Track outbound links

未選取這些設定時，平台不會引發 [!DNL Adobe Analytics] 自動。 仅当您在规则操作中明确给出指示时，[!DNL Analytics] 才会触发。可使用规则条件确定触发的时间和内容。例如，要使用 Cookie 确定“选择启用”状态，可设置一个数据元素来读取该 Cookie 并将其用作规则中的条件，以便确定何时触发 Send Beacon 操作。

另外，您可以考虑使用 [Adobe 选择启用对象](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hans)来控制此标记的触发，以便与您的同意管理平台相一致。

与同意管理器（例如 OneTrust）的集成可以设置和跟踪客户的同意 Cookie，然后可以在规则生成器中使用它们。

## Audience Manager

如果将 DIL 置于客户页面上，则 DIL 当前会设置为自动触发。请考虑使用 [Adobe 选择启用对象](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hans)来控制此标记的触发，以便与您的同意管理平台相一致。

[!DNL Adobe] 建议您在 [!DNL Analytics] 内使用服务器端转发。

## Experience Cloud ID

如果将 [!DNL Experience Cloud ID] 置于客户页面上，则其当前会自动触发。

请考虑使用 [Adobe 选择启用对象](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hans)来控制此标记的触发，以便与您的同意管理平台相一致。

## Target

Adobe Experience Platform無法引發 [!DNL Target] 自動。 仅当您在规则操作中明确给出指示时，[!DNL Target] 才会触发。可使用规则条件确定触发的时间和内容。例如，要使用 Cookie 确定“选择启用”状态，可设置一个数据元素来读取该 Cookie 并将其用作规则中的条件，以便确定何时触发 Load [!DNL Target] 操作。

另外，您可以考虑使用 [Adobe 选择启用对象](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hans)来控制此标记的触发，以便与您的同意管理平台相一致。

与同意管理器（例如 OneTrust）的集成可以设置和跟踪客户的同意 Cookie，然后可以在规则生成器中使用它们。
