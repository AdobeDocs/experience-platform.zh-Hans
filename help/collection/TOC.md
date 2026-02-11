---
audience: user
solution: Data Collection
user-guide-title: 数据收集
breadcrumb-title: 数据收集
user-guide-description: 了解如何将数据发送到Adobe Experience Platform。
feature: Data Collection
role: Developer
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 32%

---


# 数据收集 {#collection}

+ [概述](home.md)
+ [权限](permissions.md)
+ BrightScript {#brightscript}
   + [BrightScript概述](brightscript/brs-overview.md)
+ JavaScript {#js}
   + [Web SDK JavaScript概述](js/js-overview.md)
   + [发行说明](js/release-notes.md)
   + 安装 {#install}
      + [安装概述](js/install/overview.md)
      + [基础代码](js/install/base-code.md)
      + [库](js/install/library.md)
      + [npm](js/install/npm.md)
      + [自定义内部版本](js/install/create-custom-build.md)
   + 命令 {#commands}
      + [appendIdentityToUrl](js/commands/appendidentitytourl.md)
      + [applyPropositions](js/commands/applypropositions.md)
      + [applyResponse](js/commands/applyresponse.md)
      + configure {#configure}
         + [概述](js/commands/configure/overview.md)
         + [autoCollectPropositionInteractions](js/commands/configure/autocollectpropositioninteractions.md)
         + [clickCollection](js/commands/configure/clickcollection.md)
         + [clickCollectionEnabled](js/commands/configure/clickcollectionenabled.md)
         + [上下文](js/commands/configure/context.md)
         + [对话](js/commands/configure/conversation.md)
         + [datastreamId](js/commands/configure/datastreamid.md)
         + [debugEnabled](js/commands/configure/debugenabled.md)
         + [defaultconsent](js/commands/configure/defaultconsent.md)
         + [downloadlinkqualifier](js/commands/configure/downloadlinkqualifier.md)
         + [edgbasePath](js/commands/configure/edgebasepath.md)
         + [edgeConfigOverrides](js/commands/configure/edgeconfigoverrides.md)
         + [edgeDomain](js/commands/configure/edgedomain.md)
         + [idMigrationEnabled](js/commands/configure/idmigrationenabled.md)
         + [onBeforeEventSend](js/commands/configure/onbeforeeventsend.md)
         + [onBeforeLinkClickSend](js/commands/configure/onbeforelinkclicksend.md)
         + [orgId](js/commands/configure/orgid.md)
         + [预隐藏样式](js/commands/configure/prehidingstyle.md)
         + [pushNotifications](js/commands/configure/pushnotifications.md)
         + [流媒体](js/commands/configure/streamingmedia.md)
         + [Targetmigrationenabled](js/commands/configure/targetmigrationenabled.md)
         + [thirdPartyCookiesEnabled](js/commands/configure/thirdpartycookiesenabled.md)
      + [createMediaSession](js/commands/createmediasession.md)
      + [getIdentity](js/commands/getidentity.md)
      + [getLibraryInfo](js/commands/getlibraryinfo.md)
      + [getMediaAnalyticsTracker](js/commands/getmediaanalyticstracker.md)
      + sendEvent {#sendevent}
         + [概述](js/commands/sendevent/overview.md)
         + [数据](js/commands/sendevent/data.md)
         + [文档卸载](js/commands/sendevent/documentunloading.md)
         + [edgeConfigOverrides](js/commands/sendevent/edgeconfigoverrides.md)
         + [事件类型](js/commands/sendevent/eventtype.md)
         + [个性化](js/commands/sendevent/personalization.md)
         + [renderDecisions](js/commands/sendevent/renderdecisions.md)
         + [xdm](js/commands/sendevent/xdm.md)
      + [sendMediaEvent](js/commands/sendmediaevent.md)
      + [sendPushSubscription](js/commands/sendpushsubscription.md)
      + [setConsent](js/commands/setconsent.md)
      + [setDebug](js/commands/setdebug.md)
      + [subscribeRulesetItems](js/commands/subscriberulesetitems.md)
      + [命令响应](js/commands/command-responses.md)
   + [监控挂钩](js/monitoring-hooks.md)
   + [常见问题](js/faq.md)
+ 标记客户端JavaScript {#tags}
   + [概述](tags/overview.md)
   + [buildInfo](tags/buildinfo.md)
   + [公司](tags/company.md)
   + [_container](tags/container.md)
   + [cookie](tags/cookie.md)
   + [environment](tags/environment.md)
   + [getVar](tags/getvar.md)
   + [getVisitorId](tags/getvisitorid.md)
   + [logger](tags/logger.md)
   + [监视器(_M)](tags/monitors.md)
   + [setDebug](tags/setdebug.md)
   + [setVar](tags/setvar.md)
   + [跟踪](tags/track.md)
+ 用例 {#use-cases}
   + [概述](use-cases/overview.md)
   + [客户端提示](use-cases/client-hints.md)
   + [客户端状态](use-cases/client-state.md)
   + [收集商业数据](use-cases/collect-commerce-data.md)
   + [配置CSP](use-cases/configuring-a-csp.md)
   + [调试](use-cases/debugging.md)
   + [事件去重](use-cases/event-duplication.md)
   + 身份标识 {#identity}
      + [概述](use-cases/identity/id-overview.md)
      + [第一方设备 ID](use-cases/identity/first-party-device-ids.md)
      + [ID共享](use-cases/identity/id-sharing.md)
   + [多个SDK实例](use-cases/multiple-instances.md)
   + 个性化 {#personalization}
      + [概述](use-cases/personalization/pers-overview.md)
      + [显示事件](use-cases/personalization/display-events.md)
      + [管理闪烁](use-cases/personalization/manage-flicker.md)
      + [呈现个性化内容](use-cases/personalization/rendering-personalization-content.md)
      + [排名最前和排名最前的页面事件](use-cases/personalization/top-bottom-page-events.md)
