---
title: 将Adobe Journey Optimizer与Platform Web SDK一起使用
description: 了解如何使用Adobe Journey Optimizer通过Experience PlatformWeb SDK呈现个性化内容
keywords: ajo；ajo web；adobe journey optimizer；renderDecisions；表面；决策；建议；范围；架构
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 1%

---

# 使用 [!DNL Adobe Journey Optimizer] 使用 [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 可以投放和渲染在中管理的个性化体验 [!DNL Adobe Journey Optimizer] 到Web渠道。 您可以使用WYSIWYG编辑器， [!DNL Adobe Journey Optimizer] [Web Campaign UI](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)，以创建、激活和交付您的 [!DNL Journey Optimizer Web] 营销活动和个性化体验。

>[!IMPORTANT]
>
>阅读 [Adobe Journey Optimizer Web渠道文档](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html?lang=zh-Hans) ，以了解有关入门的信息 [!DNL Journey Optimizer Web] 体验创作和报告。

## 术语 {#terminology}

**[!UICONTROL 表面]**：Web表面是由其中的 [!DNL Adobe Journey Optimizer] 体验内容将被交付。

**[!UICONTROL 建议]**：在 [!DNL Adobe Journey Optimizer]，建议与从中选择的体验相关联 [!DNL Journey Optimizer Campaign].

## 正在启用 [!DNL Adobe Journey Optimizer] {#enable-ajo}

开始使用 [!DNL Adobe Journey Optimizer]，请按照以下步骤操作。

1. 浏览 [先决条件](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) 从 [!DNL Adobe Journey Optimizer] [Web体验指南](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)，具体来说：
   * 设置 [!DNL Adobe Experience Cloud Visual Editing Helper].
   * 启用 [!DNL Adobe Journey Optimizer] 在您的 [数据流](../../../datastreams/overview.md).
   * 启用 [!UICONTROL Active-On-Edge合并策略] 选项。

2. 添加 `renderDecisions` 选项添加到您的事件。 设置 `renderDecisions` 到 `true` 用于在网页表面上自动呈现交付的Journey Optimizer内容建议。

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. （可选）在事件中指定其他表面。 默认情况下，Web SDK将自动为当前网页生成Web表面，并将其包含在对Edge Network的请求中。 如果需要，可以通过在 `personalization.surfaces` 的选项 `sendEvent` 命令，或在对应 **[!UICONTROL 曲面]** [[!UICONTROL 发送事件] 操作](../../../tags/extensions/client/web-sdk/action-types.md#send-event) web SDK扩展的配置。

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
           "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extension-add-surface](./assets/extension-add-surface.png)

   事件表面包含在 `query.personalization.surfaces` 请求字段：

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

4. 与其他个性化功能类似，您可以添加 **[预隐藏代码片段](../manage-flicker.md)** 以在提取体验时仅隐藏页面的某些部分。

## 创建Adobe Journey Optimizer Web体验 {#create-ajo-web-experiences}

请遵循 [Web营销活动创作](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) 中的说明 [!DNL Adobe Journey Optimizer] [Web体验指南](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) 创建 [!DNL Journey Optimizer Web] 营销活动和体验。

## 呈现个性化内容 {#rendering-personalized-content}

请参阅相关文档 [呈现个性化内容](../rendering-personalization-content.md) 以了解更多信息。

用于Web表面的Adobe Journey Optimizer建议的处理方式与 `__view__` 决策范围建议。 具体来说，当 `renderDecisions` 选项设置为 `true` 在 `sendEvent` 命令这些内容将由Web SDK自动呈现。

Journey Optimizer内容建议示例：

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

要调试Adobe Journey Optimizer个性化实施，请使用 [Web SDK调试](/help/web-sdk/use-cases/debugging.md). [!DNL Adobe Journey Optimizer] 在使用进行故障诊断时，可以使用调试跟踪 [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). 使用检查事件 `AJO:` 前缀。

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)
