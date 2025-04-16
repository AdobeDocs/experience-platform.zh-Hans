---
title: 未经身份验证的访客的异地重定位
description: 了解如何使用ECID重新定位未经身份验证的用户
feature: Use Cases, Customer Acquisition
source-git-commit: 672b15b0c36efbf3b7d62ec616f254fffe3dbb81
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# 未经验证的重定位 {#unauthenticated-retargeting}

随着第三方Cookie失效，企业正在过渡到无Cookie解决方案以实现个性化参与和重新定位。 异地重定位使企业能够根据以前的互动接触高意图用户，而无需依赖客户端JavaScript。

## 为何要考虑重新定位未经身份验证的访客 {#why-use-case}

通过集成Adobe Experience Platform的Web SDK和服务器端事件转发，您可以简化事件流和数据转发。 这样可以使用ECID (Experience Cloud ID)无缝地重新定位未经身份验证的用户，从而确保跨平台的一致参与。 使用此解决方案，您可以通过根据未经身份验证的用户过去的交互情况有效地重新定位他们来增加转化机会。

## 先决条件和规划 {#prerequisites-and-planning}

在继续部署Web SDK和事件转发配置之前，请确保以下各项：

1. **具有Web SDK设置的Adobe**：必须实施Adobe Web SDK以方便事件收集和数据转发。

2. **Adobe Experience Platform Edge Network配置**：确保将Edge Network配置为支持实时事件转发以进行异地重定位。

3. **ECID同步**：确保ECID跨平台同步，以实现无缝的受众匹配。

## 如何实现异地重定位 {#achieve-offsite-retargeting}

1. **部署Web SDK**：在您的网站上实施Adobe Web SDK以捕获实时事件数据，包括页面查看、点击和其他行为等用户交互。

2. **启用事件转发**：在Platform内配置事件转发以发送收集的用户数据，确保为受众激活有效传输数据。

3. **配置服务器端激活**：使用Adobe的服务器端功能激活基于ECID的重定向受众，确保跨平台准确地定位受众。

4. **创建重定位受众**：利用Platform的受众分段工具，根据用户行为（如查看、交互或放弃的购物车）定义重点受众。

5. **激活受众**：创建重定位受众后，请激活这些受众以提供个性化内容，确保根据用户以前与您的网站的交互情况重新吸引用户。

## 使用计算属性创建受众 {#create-audience}

要有效地重新定位意图较高的用户，请根据其过去与您的网站的交互创建受众。 使用Platform通过计算属性来划分用户。

1. **识别关键行为**：选择要跟踪的用户操作，如页面查看次数或点击次数。

2. **创建受众**：使用受众分段工具根据行为对用户进行分组。

3. **同步ECID**：确保ECID跨平台同步，以实现准确的受众匹配。

## 激活受众 {#activate-audience}

创建受众后，请跨平台激活该受众以吸引用户。

1. **审核受众**：确保受众区段反映正确的行为。

2. **创建激活规则**：根据操作设置用户参与的时间和方式条件。

3. **推送到平台**：激活受众。

4. **监视性能**：跟踪受众性能并根据需要进行调整。

## 配置异地重定位扩展 {#configure-extension}

### 部署Web SDK

确保Adobe Web SDK已正确集成到您的网站中。 此SDK允许收集实时事件数据，这对于高效重定位至关重要。

### 启用事件转发

在Platform内设置事件转发，将收集的用户行为数据发送到重定位平台。 事件转发可确保有效传输数据，从而使企业能够在不依赖Cookie的情况下定位高意图用户。

### 附加到重定位规则

请确保将异地重定位扩展附加到Adobe Experience Platform数据收集中的有效事件规则。 通常，应创建全局规则以触发关键操作，如`page load`或特定用户交互。

要了解有关配置该扩展的更多信息，请阅读[事件转发](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)文档。

## 其他用例 {#other-use-cases}

本文档概述了成功开发和利用Web SDK和事件转发设置的主要用例和技术注意事项。 通过遵循概述的过程并确保满足必要的先决条件，您可以显着改进他们的数据跟踪和分析功能。

您可以进一步探索通过Real-Time CDP中的合作伙伴数据支持启用的用例：

- [使用合作伙伴数据参与并获取新客户](./prospecting.md)。
- [通过合作伙伴帮助的访客识别功能个性化现场体验](./offsite-retargeting.md)。
- [使用合作伙伴提供的属性补充第一方配置文件](./supplement-first-party-profiles.md)。