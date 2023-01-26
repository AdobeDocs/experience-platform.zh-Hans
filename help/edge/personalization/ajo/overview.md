---
title: 将Adobe Journey Optimizer与Platform Web SDK结合使用
description: 了解如何使用Experience PlatformWeb SDK渲染个性化内容(使用Adobe Journey Optimizer)
keywords: ajo;ajo web;adobe journey optimizer;renderDecisions;surfaces；决策；建议；范围；模式
exl-id: e608952c-9598-11ed-b382-d72064651cac
source-git-commit: 1b0f1e2e1625f6994a6e09bd086e4b63a3e8d4ab
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# 使用 [!DNL Adobe Journey Optimizer] 和 [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 可以提供和呈现在中管理的个性化体验 [!DNL Adobe Journey Optimizer] 到web渠道。 你可以使用WYSIWYG编辑器， [!DNL Adobe Journey Optimizer] [Web Campaign UI](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)，以创建、激活和交付 [!DNL Journey Optimizer Web] 营销活动和个性化体验。

>[!IMPORTANT]
>
>阅读 [Adobe Journey Optimizer Web渠道文档](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html) 有关入门的信息 [!DNL Journey Optimizer Web] 体验创作和报告。

## 术语 {#terminology}

**[!UICONTROL 曲面]**:Web曲面是由URL标识的Web属性，其中 [!DNL Adobe Journey Optimizer] 将交付体验内容。

**[!UICONTROL 建议]**:在 [!DNL Adobe Journey Optimizer]，建议与从 [!DNL Journey Optimizer Campaign].

## 启用 [!DNL Adobe Journey Optimizer] {#enable-ajo}

开始使用 [!DNL Adobe Journey Optimizer]，请执行以下步骤。

1. 通过 [先决条件](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) 从 [!DNL Adobe Journey Optimizer] [Web体验指南](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)，具体而言：
   * 设置 [!DNL Adobe Experience Cloud Visual Editing Helper].
   * 启用 [!DNL Adobe Journey Optimizer] 在 [数据流](../../datastreams/overview.md).
   * 启用 [!UICONTROL 边缘活动合并策略] 选项。

2. 添加 `renderDecisions` 选项。 已设置 `renderDecisions` to `true` 用于在您的网页表面上自动呈现已交付的Journey Optimizer内容主张。

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. （可选）在事件中指定其他曲面。 默认情况下，Web SDK将自动为当前网页生成Web曲面，并将其包含在对边缘网络的请求中。 如果需要，可通过在 `personalization.surfaces` 的 `sendEvent` 命令，或在相应的 **[!UICONTROL 曲面]** [[!UICONTROL 发送事件] 操作](../../extension/action-types.md#send-event) 配置Web SDK扩展。

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
       "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extension-add-surface](./assets/extension-add-surface.png)

   事件曲面包含在 `query.personalization.surfaces` 请求字段：

   ```json
   {
   "events": [
       {
           "query": {
               "personalization": {
               "schemas": [
                   ...
               ],
               "decisionScopes": [
                   "__view__"
               ],
               "surfaces": [
                   "web://ajostage.weebly.com/"
               ]
               }
           },
           ...
       }
   ]
   }
   ```

4. 与其他个性化功能类似，您可以添加 **[预隐藏代码片段](../manage-flicker.md)** 以在获取体验时仅隐藏页面的某些部分。

## 创建Adobe Journey Optimizer Web体验 {#create-ajo-web-experiences}

关注 [Web营销活动创作](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) 说明 [!DNL Adobe Journey Optimizer] [Web体验指南](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) 创建 [!DNL Journey Optimizer Web] 营销活动和体验。

## 呈现个性化内容 {#rendering-personalized-content}

请参阅 [渲染个性化内容](../rendering-personalization-content.md) 以了解更多信息。

对web曲面的Adobe Journey Optimizer命题的处理方式与 `__view__` 决策范围建议。 具体而言，当 `renderDecisions` 选项设置为 `true` 在 `sendEvent` 命令，这些命令将由Web SDK自动呈现。

Journey Optimizer内容主张示例：

```json
{
    "scope": "web://ajostage.weebly.com/",
    "scopeDetails": {
        "correlationID": "ccfaf19c-6360-4aea-b464-0cf924db5da7",
        "characteristics": {
            "eventToken": "eyJtZXNzYWdlRXhlY3V0aW9uIjp7Im1lc3NhZ2VFeGVjdXRpb25JRCI6ImEzNDYxYTMzLTc5MjktNGQyNS1hNmMxLTVkYzM2YWY1NzRmMyIsIm1lc3NhZ2VJRCI6ImNjZmFmMTljLTYzNjAtNGFlYS1iNDY0LTBjZjkyNGRiNWRhNyIsIm1lc3NhZ2VUeXBlIjoibWFya2V0aW5nIiwiY2FtcGFpZ25JRCI6IjEzN2JmMzllLWM1ODgtNGI1My1iODQxLTJiMWZiZDYxM2JkYiIsImNhbXBhaWduVmVyc2lvbklEIjoiMTA1NzY1MmEtZWYwNS00YjE3LWExMmUtY2FlOTQyOTFhMWFjIiwiY2FtcGFpZ25BY3Rpb25JRCI6ImViNTlmODQ4LTk5ZDYtNGE1OC05YmU4LTk4MjIxODU0NmYzNiIsIm1lc3NhZ2VQdWJsaWNhdGlvbklEIjoiYzg2NzFjZmItNDdjYS00YTVjLTg4Y2YtNzYwZDFlZjU1MzQyIn0sIm1lc3NhZ2VQcm9maWxlIjp7ImNoYW5uZWwiOnsiX2lkIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWxzL3dlYiIsIl90eXBlIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWwtdHlwZXMvd2ViIn0sIm1lc3NhZ2VQcm9maWxlSUQiOiI2YTViY2I3ZC02MmYxLTQ5NDItODRkMC02MzE5ZjM5Zjk1ZGUifX0="
        },
        "decisionProvider": "AJO",
        "activity": {
            "id": "137bf39e-c588-4b53-b841-2b1fbd613bdb#eb59f848-99d6-4a58-9be8-982218546f36"
        }
    },
    "id": "002321c0-dff5-4153-b171-a9dfb70b9750",
    "items": [
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": "Welcome AJO!",
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setHtml",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "0a522f66-9e6a-4ded-b1d0-e9167f103290"
        },
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": {
                    "font-weight": "bold"
                },
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setStyle",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "66216ca5-5d0f-4239-a8c8-6bc4a5a7cbdb"
        }
    ]
}
```

## 调试 {#debugging}

要调试Adobe Journey Optimizer个性化实施，请使用 [[!DNL Web SDK] 调试](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html). [!DNL Adobe Journey Optimizer] 在对使用 [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). 使用 `AJO:` 前缀。

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)


