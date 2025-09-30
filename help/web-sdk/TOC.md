---
solution: Data Collection
audience: user
user-guide-title: Adobe Experience Platform Web SDK 帮助
breadcrumb-title: Web SDK 指南
user-guide-description: 通过边缘网络与 Experience Cloud 服务交互。
feature: Web SDK
role: Developer
source-git-commit: c697d0e924545caf430382385797bde340b57d94
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 27%

---


# Adobe Experience Platform Web SDK {#web-sdk}

* [Web SDK 概述](home.md)
* [发行说明](release-notes.md)
* Web SDK安装 {#install}
   * [概述](install/overview.md)
   * [使用标记扩展安装Web SDK](install/extension.md)
   * [使用JavaScript库安装Web SDK](install/library.md)
   * [使用NPM包安装Web SDK](install/npm.md)
   * [使用NPM包创建自定义Web SDK内部版本](install/create-custom-build.md)
* 命令 {#commands}
   * configure {#configure}
      * [概述](commands/configure/overview.md)
      * [autoCollectPropositionInteractions](commands/configure/autocollectpropositioninteractions.md)
      * [clickCollectionEnabled](commands/configure/clickcollectionenabled.md)
      * [clickCollection](commands/configure/clickcollection.md)
      * [上下文](commands/configure/context.md)
      * [datastreamId](commands/configure/datastreamid.md)
      * [debugEnabled](commands/configure/debugenabled.md)
      * [defaultconsent](commands/configure/defaultconsent.md)
      * [downloadlinkqualifier](commands/configure/downloadlinkqualifier.md)
      * [edgbasePath](commands/configure/edgebasepath.md)
      * [edgeDomain](commands/configure/edgedomain.md)
      * [idMigrationEnabled](commands/configure/idmigrationenabled.md)
      * [流媒体](commands/configure/streamingmedia.md)
      * [onBeforeEventSend](commands/configure/onbeforeeventsend.md)
      * [onBeforeLinkClickSend](commands/configure/onbeforelinkclicksend.md)
      * [orgId](commands/configure/orgid.md)
      * [预隐藏样式](commands/configure/prehidingstyle.md)
      * [pushNotifications](commands/configure/pushnotifications.md)
      * [Targetmigrationenabled](commands/configure/targetmigrationenabled.md)
      * [thirdPartyCookiesEnabled](commands/configure/thirdpartycookiesenabled.md)
   * sendEvent {#sendevent}
      * [概述](commands/sendevent/overview.md)
      * [数据](commands/sendevent/data.md)
      * [文档卸载](commands/sendevent/documentunloading.md)
      * [个性化](commands/sendevent/personalization.md)
      * [renderDecisions](commands/sendevent/renderdecisions.md)
      * [类型](commands/sendevent/type.md)
      * [xdm](commands/sendevent/xdm.md)
   * [appendIdentityToUrl](commands/appendidentitytourl.md)
   * [applyPropositions](commands/applypropositions.md)
   * [applyResponse](commands/applyresponse.md)
   * [createMediaSession](commands/createmediasession.md)
   * [getIdentity](commands/getidentity.md)
   * [getLibraryInfo](commands/getlibraryinfo.md)
   * [getMediaAnalyticsTracker](commands/getmediaanalyticstracker.md)
   * [setConsent](commands/setconsent.md)
   * [setDebug](commands/setdebug.md)
   * [sendMediaEvent](commands/sendmediaevent.md)
   * [sendPushSubscription](commands/sendPushSubscription.md)
   * [subscribeRulesetItems](commands/subscriberulesetitems.md)
   * [配置数据流覆盖](commands/datastream-overrides.md)
   * [命令响应](commands/command-responses.md)

* 身份标识 {#identity}
   * [概述](identity/overview.md)
   * [第一方设备 ID](identity/first-party-device-ids.md)
   * [移动到Web和跨域ID共享](identity/id-sharing.md)

* 个性化 {#personalization}
   * [管理显示事件](personalization/display-events.md)
   * [呈现个性化内容](personalization/rendering-personalization-content.md)
   * [通过混合实施的Personalization](personalization/hybrid-personalization.md)
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
   * Offer Decisioning {#offer-decisioning}
      * [概述](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [概述](personalization/ajo/overview.md)
      * [单页应用程序实施](personalization/ajo/web-spa-implementation.md)
      * [在Web SDK中配置Web应用程序内消息传送支持](personalization/web-in-app-messaging.md)

* 同意 {#consent}
   * IAB透明度和同意框架2.0 {#iab-tcf}
      * [概述](consent/iab-tcf/overview.md)
      * [与标记集成](consent/iab-tcf/with-tags.md)
      * [集成而不使用标记](consent/iab-tcf/without-tags.md)

* 用例 {#use-cases}
   * [概述](use-cases/overview.md)
   * [使用Web SDK将数据发送到Adobe Analytics](use-cases/adobe-analytics.md)
   * [用户代理客户端提示](use-cases/client-hints.md)
   * [收集商业数据](use-cases/collect-commerce-data.md)
   * [配置CSP](use-cases/configuring-a-csp.md)
   * [调试方法](use-cases/debugging.md)
   * [使用多个Web SDK实例](use-cases/multiple-instances.md)
   * [配置顶页面事件和底页面事件](use-cases/top-bottom-page-events.md)
* [监控挂钩](monitoring-hooks.md)
* [常见问题](faq.md)
* [资源](resources.md)
