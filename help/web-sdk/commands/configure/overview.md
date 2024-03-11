---
title: 配置Adobe Experience Platform Web SDK
description: 使用Web SDK时，可使用configure命令设置所需的设置。
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# 配置Adobe Experience Platform Web SDK

Web SDK的配置已完成 `configure` 命令。 只要使用库或标记扩展，就必须执行配置Web SDK的重要且必需的步骤。

## 使用标记扩展配置Web SDK {#configure-tag-extension}

请按照以下步骤通过标记扩展配置Web SDK。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 转到 [Web SDK标记扩展配置页面](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) 有关所有配置选项的详细信息。

每当您使用扩展将数据发送到Adobe时，都会设置这些配置设置。

## 使用JavaScript库配置Web SDK {#configure-js}

运行 `configure` 命令。 调用任何其他Web SDK命令(例如 [`sendEvent`](../sendevent/overview.md).

此 [`edgeConfigId`](edgeconfigid.md) 和 [`orgId`](orgid.md) 属性为必填项。 所有其他属性都是可选的，具体取决于贵组织的实施要求。

有关每个受支持命令的详细信息，请参阅本用户指南的目录。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false,
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  "debugEnabled": true,
  "defaultConsent": "pending",
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  "edgeBasePath": "ee",
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "edgeDomain": "data.example.com",
  "idMigrationEnabled": false,
  "onBeforeEventSend": function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  "onBeforeLinkClickSend": function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  "prehidingStyle": "#container { opacity: 0 !important }",
  "targetMigrationEnabled": true,
  "thirdPartyCookiesEnabled": false
});
```
