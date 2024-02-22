---
solution: Data Collection
audience: user
user-guide-title: Adobe Experience Platform Web SDK 帮助
breadcrumb-title: Web SDK 指南
user-guide-description: 通过边缘网络与 Experience Cloud 服务交互。
feature: Web SDK
source-git-commit: 82eede9e59338e8438c361d58b476960b7faa5cb
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 23%

---


# Adobe Experience Platform Web SDK {#edge}

* [Platform Web SDK概述](home.md)
* 基础知识 {#fundamentals}
   * [支持的用例](fundamentals/supported-use-cases.md)
   * [先决条件](fundamentals/prerequisite.md)
   * [安装SDK](fundamentals/installing-the-sdk.md)
   * [配置SDK](fundamentals/configuring-the-sdk.md)
   * [执行命令](fundamentals/executing-commands.md)
   * [跟踪事件](fundamentals/tracking-events.md)
   * [配置页面顶部和底部事件](fundamentals/top-bottom-page-events.md)
   * [调试](fundamentals/debugging.md)
   * [配置CSP](fundamentals/configuring-a-csp.md)
   * [与多个属性交互](fundamentals/interacting-with-multiple-properties.md)
   * [用户代理客户端提示](fundamentals/user-agent-client-hints.md)
* 标识 {#identity}
   * [概述](identity/overview.md)
   * [第一方设备Id](identity/first-party-device-ids.md)
   * [移动到Web和跨域ID共享](identity/id-sharing.md)
* 数据收集 {#data-collection}
   * [自动收集的信息](data-collection/automatic-information.md)
   * [跟踪链接](data-collection/track-links.md)
   * [收集商业、产品和订单数据](data-collection/collect-commerce-data.md)
   * Adobe Analytics {#adobe-analytics}
      * [将Adobe Analytics与平台Web SDK结合使用](data-collection/adobe-analytics/analytics-overview.md)
      * [映射Analytics变量](data-collection/adobe-analytics/manually-mapping-variables.md)
      * [自动映射的变量](data-collection/adobe-analytics/automatically-mapped-vars.md)
      * [将数据发送到Analytics](data-collection/adobe-analytics/sending-data-to-analytics.md)
* 个性化 {#personalization}
   * [管理显示事件](personalization/display-events.md)
   * [呈现个性化内容](personalization/rendering-personalization-content.md)
   * [通过混合实施进行个性化](personalization/hybrid-personalization.md)
   * [管理闪烁](personalization/manage-flicker.md)

   * Adobe Target {#adobe-target}
      * [概述](personalization/adobe-target/target-overview.md)
      * [单页应用程序实施](personalization/adobe-target/spa-implementation.md)
      * [访问响应令牌](personalization/adobe-target/accessing-response-tokens.md)
      * [使用mbox第三方ID](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [将at.js库与Web SDK进行比较](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Analytics for Target (A4T)日志记录 {#a4t}
         * [概述](personalization/adobe-target/analytics-logging/overview.md)
         * [客户端日志记录](personalization/adobe-target/analytics-logging/client-side.md)
         * [服务器端日志记录](personalization/adobe-target/analytics-logging/server-side.md)
   * offer decisioning {#offer-decisioning}
      * [概述](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [概述](personalization/ajo/overview.md)
      * [单页应用程序实施](personalization/ajo/web-spa-implementation.md)
      * [配置Web应用程序内消息传送](personalization/web-in-app-messaging.md)
* 同意 {#consent}
   * [支持同意](consent/supporting-consent.md)
   * IAB透明度和同意框架2.0 {#iab-tcf}
      * [概述](consent/iab-tcf/overview.md)
      * [与标记集成](consent/iab-tcf/with-launch.md)
      * [集成而不使用标记](consent/iab-tcf/without-launch.md)
* [Web SDK标记扩展](web-sdk-tag-extension-overview.md)
* [发行说明](release-notes.md)
* [常见问题](web-sdk-faq.md)
* [资源](resources.md)
