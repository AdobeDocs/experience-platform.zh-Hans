---
audience: user
user-guide-title: 标记帮助
breadcrumb-title: 标记
user-guide-description: 了解如何部署和管理分析、营销和广告标记以提升客户体验。
feature: Tags
solution: Data Collection
role: Developer
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 36%

---


# 标记 {#tags}

* [标记概述](./home.md)
* 快速入门{#get-started}
   * [快速入门指南](./quick-start/quick-start.md)
   * [实施指南](./quick-start/implementation-guides.md)
* UI指南{#ui}
   * [概述](./ui/managing-resources/overview.md)
   * 扩展 {#extensions}
      * [概述](./ui/managing-resources/extensions/overview.md)
      * [扩展升级](./ui/managing-resources/extensions/extension-upgrade.md)
   * [数据元素](./ui/managing-resources/data-elements.md)
   * [规则](./ui/managing-resources/rules.md)
   * [注释](./ui/managing-resources/notes.md)
   * [复制资源](./ui/managing-resources/copying-resources.md)
   * [比较资源修订版本](./ui/managing-resources/compare-resource-revisions.md)
   * [删除资源](./ui/managing-resources/delete-resources.md)
   * [从库中移除资源](./ui/managing-resources/remove-resources-from-library.md)
* 发布 {#publish}
   * [概述](./ui/publishing/overview.md)
   * [发布流](./ui/publishing/publishing-flow.md)
   * 主机 {#hosts}
      * [概述](./ui/publishing/hosts/hosts-overview.md)
      * [Adobe管理的主机](./ui/publishing/hosts/managed-by-adobe-host.md)
      * [SFTP主机](./ui/publishing/hosts/sftp-host.md)
   * 环境 {#environments}
      * [概述](./ui/publishing/environments.md)
      * [使用 Adobe Experience Platform Debugger 测试嵌入代码](./ui/publishing/embed-code-testing.md)
   * [内部版本](./ui/publishing/builds.md)
   * [库](./ui/publishing/libraries.md)
   * [自托管库](./ui/publishing/hosts/self-hosting-libraries.md)
   * [重新发布库](./ui/publishing/republish.md)
   * [Experience Platform标记（中国）](./ui/publishing/premium-cdn.md)
* 客户端信息 {#client-side}
   * [概述](./ui/client-side/overview.md)
   * [异步部署](./ui/client-side/asynchronous-deployment.md)
   * [卫星对象引用](./ui/client-side/satellite-object.md)
   * [部署JavaScript标记以管理客户同意](./ui/client-side/consent.md)
   * [内容安全策略(CSP)支持](./ui/client-side/content-security-policy.md)
   * [子资源完整性(SRI)支持](./ui/client-side/sri.md)
   * [传输层安全性](./ui/client-side/transport-layer-security.md)
* 事件转发{#event-forwarding}
   * [概述](./ui/event-forwarding/overview.md)
   * [快速入门](./ui/event-forwarding/getting-started.md)
   * [配置密钥](./ui/event-forwarding/secrets.md)
   * [监控(Beta)](./ui/event-forwarding/monitoring.md)
* 管理 {#admin}
   * [概述](./ui/administration/overview.md)
   * [公司和资产](./ui/administration/companies-and-properties.md)
   * [用户权限](./ui/administration/user-permissions.md)
* 扩展 {#extensions}
   * [概述](./extensions/overview.md)
   * 标记扩展（客户端） {#client}
      * [概述](./extensions/client/overview.md)
      * [可访问的网站速度指标](https://exchange.adobe.com/apps/ec/103053)
      * [Activity Map自定义程序](https://exchange.adobe.com/apps/ec/101531)
      * [操作页面刷新](https://exchange.adobe.com/apps/ec/102848)
      * [Adform网站跟踪](https://exchange.adobe.com/apps/ec/103195)
      * [Adobe Advertising Cloud](https://exchange.adobe.com/apps/ec/100155)
      * Adobe Analytics {#analytics}
         * [概述](./extensions/client/analytics/overview.md)
         * [共享模块](./extensions/client/analytics/shared-modules.md)
         * [发行说明](./extensions/client/analytics/release-notes.md)
      * [Adobe Analytics和Adobe Target](https://exchange.adobe.com/apps/ec/105363/6sense-for-analytics-and-target)
      * [Adobe Analytics和Microsoft Dynamics](https://exchange.adobe.com/apps/ec/102966)
      * [Adobe Analytics和Salesforce](https://exchange.adobe.com/apps/ec/101530)
      * Adobe Analytics产品字符串{#product-string}
         * [概述](./extensions/client/product-string/overview.md)
         * [发行说明](./extensions/client/product-string/release-notes.md)
      * [Adobe Analytics产品字符串生成器](https://exchange.adobe.com/apps/ec/101461)
      * [通过Adobe Experience Platform Web SDK的Adobe Analytics](https://exchange.adobe.com/apps/ec/108985/search-discovery-for-adobe-analytics-via-aep-web-sdk)
      * Adobe Audience Manager {#audience-manager}
         * [概述](./extensions/client/audience-manager/overview.md)
      * Adobe客户端数据层{#client-data-layer}
         * [概述](./extensions/client/client-data-layer/overview.md)
         * [发行说明](./extensions/client/client-data-layer/release-notes.md)
      * Adobe Content Analytics {#content-analytics}
         * [概述](./extensions/client/content-analytics/overview.md)
      * Adobe ContextHub {#contexthub}
         * [概述](./extensions/client/contexthub/overview.md)
      * [Adobe Experience Manager Forms](https://exchange.adobe.com/apps/ec/107493)
      * Adobe Experience Cloud ID 服务 {#id-service}
         * [概述](./extensions/client/id-service/overview.md)
         * [发行说明](./extensions/client/id-service/release-notes.md)
      * Adobe Experience Platform演示{#platform-demo}
         * [概述](./extensions/client/platform-demo/overview.md)
      * Adobe Experience Platform Web SDK {#web-sdk}
         * [概述](./extensions/client/web-sdk/overview.md)
         * [配置Web SDK标记扩展](./extensions/client/web-sdk/web-sdk-extension-configuration.md)
         * [事件类型](./extensions/client/web-sdk/event-types.md)
         * [操作类型](./extensions/client/web-sdk/action-types.md)
         * [数据元素类型](./extensions/client/web-sdk/data-element-types.md)
         * [访问ECID](./extensions/client/web-sdk/accessing-the-ecid.md)
         * [Web SDK插件](./extensions/client/web-sdk/web-sdk-plugins.md)
         * [Web SDK扩展发行说明](./extensions/client/web-sdk/web-sdk-ext-release-notes.md)
         * [Web SDK插件发行说明](./extensions/client/web-sdk/web-sdk-plugins-release-notes.md)
      * Adobe Experience Manager资产分析{#asset-insights}
         * [概述](./extensions/client/asset-insights/overview.md)
         * [发行说明](./extensions/client/asset-insights/release-notes.md)
      * [Adobe Fonts](https://exchange.adobe.com/apps/ec/101538)
      * Adobe Media Analytics for Audio and Video {#media-analytics}
         * [概述](./extensions/client/media-analytics/overview.md)
         * [发行说明](./extensions/client/media-analytics/release-notes.md)
      * Adobe Media Analytics (3.x SDK) {#media-analytics-3x}
         * [概述](./extensions/client/media-analytics-3x/overview.md)
         * [发行说明](./extensions/client/media-analytics-3x/release-notes.md)
      * Adobe隐私{#privacy}
         * [概述](./extensions/client/privacy/overview.md)
      * [Adobe报表包选择器](https://exchange.adobe.com/apps/ec/100640)
      * Adobe Target {#target}
         * [概述](./extensions/client/target/overview.md)
         * [发行说明](./extensions/client/target/release-notes.md)
      * Adobe Target v2 {#target-v2}
         * [概述](./extensions/client/target-v2/overview.md)
         * [发行说明](./extensions/client/target-v2/release-notes.md)
      * [Adobe Target Toolkit](https://exchange.adobe.com/apps/ec/100640)
      * [Advertising Cloud](https://exchange.adobe.com/apps/ec/100640)
      * [AEM资产分析](https://exchange.adobe.com/apps/ec/103406)
      * [Airbrake JS通告程序](https://exchange.adobe.com/apps/ec/103342)
      * [振幅](https://exchange.adobe.com/apps/ec/108010)
      * [阿波罗QAX](https://exchange.adobe.com/apps/ec/105068)
      * [Awin Advertiser MasterTag](https://exchange.adobe.com/apps/ec/103176)
      * [Awin转换标记](https://exchange.adobe.com/apps/ec/103240)
      * [Beemray Human Context](https://exchange.adobe.com/apps/ec/101063)
      * [Bing Ads通用事件跟踪](https://exchange.adobe.com/apps/ec/100154)
      * [分支](https://exchange.adobe.com/apps/ec/101382)
      * [!DNL BrightCove]视频跟踪{#brightcove}
         * [概述](./extensions/client/brightcove/overview.md)
         * [发行说明](./extensions/client/brightcove/release-notes.md)
      * [CallTrackingMetrics](https://exchange.adobe.com/apps/ec/107695)
      * [渠道Source标识符](https://exchange.adobe.com/apps/ec/101412)
      * [Cheetah体验](https://exchange.adobe.com/apps/ec/102759)
      * [Clicktale](https://exchange.adobe.com/apps/ec/100082)
      * 常用Analytics插件{#plugins}
         * [概述](./extensions/client/plugins/overview.md)
         * [发行说明](./extensions/client/plugins/release-notes.md)
      * [连接](https://exchange.adobe.com/apps/ec/104690)
      * [ContentSquare](https://exchange.adobe.com/apps/ec/100364)
      * [由Usercentrics CMP进行的Cookie同意管理v2](https://exchange.adobe.com/apps/ec/107037)
      * 核心{#core}
         * [概述](./extensions/client/core/overview.md)
         * [发行说明](./extensions/client/core/release-notes.md)
      * [自定义调试记录器](https://exchange.adobe.com/apps/ec/104698)
      * [客户认可](https://exchange.adobe.com/apps/ec/100688)
      * [数据元素助理(DEA)](https://exchange.adobe.com/apps/ec/101413)
      * [数据层管理器](https://exchange.adobe.com/apps/ec/101462)
      * [分贝](https://exchange.adobe.com/apps/ec/100913)
      * [Demandbase](https://exchange.adobe.com/apps/ec/101605)
      * [差分隐私](https://exchange.adobe.com/apps/ec/104535)
      * [Dynamic Media查看器](https://exchange.adobe.com/apps/ec/103048)
      * [EDDL帮助程序](https://exchange.adobe.com/apps/ec/107691)
      * [Flashtalking OneTag](https://exchange.adobe.com/apps/ec/101392)
      * [ForeSee](https://exchange.adobe.com/apps/ec/100164)
      * [Gainsight PX](https://exchange.adobe.com/apps/ec/103343)
      * [Genesys预测参与度](https://exchange.adobe.com/apps/ec/106148)
      * Google数据层{#google-data-layer}
         * [概述](./extensions/client/google-data-layer/overview.md)
         * [发行说明](./extensions/client/google-data-layer/release-notes.md)
      * [Google全局站点标记(gtag)](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag)
      * [InMoment](https://exchange.adobe.com/apps/ec/100847)
      * [JSON帮助程序](https://exchange.adobe.com/apps/ec/106449)
      * [JW播放器分析](https://exchange.adobe.com/apps/ec/101523)
      * [KickFire](https://exchange.adobe.com/apps/ec/101621)
      * [映射表](https://exchange.adobe.com/apps/ec/103136)
      * [!DNL Marketo Munchkin] {#marketo}
         * [概述](./extensions/client/marketo/overview.md)
         * [发行说明](./extensions/client/marketo/release-notes.md)
      * [主属性管理器](https://exchange.adobe.com/apps/ec/102992)
      * [Merkury标记](https://exchange.adobe.com/apps/ec/600027/merkury-tag)
      * [!DNL Meta Pixel] {#meta}
         * [概述](./extensions/client/meta/overview.md)
      * [监视](https://exchange.adobe.com/apps/ec/106544)
      * [Nielsen数字SDK](https://exchange.adobe.com/apps/ec/101361)
      * [OneTrust Cookie同意管理](https://exchange.adobe.com/apps/ec/100340)
      * [胡椒酱](https://exchange.adobe.com/apps/ec/103587)
      * [Persado连接](https://exchange.adobe.com/apps/ec/103745)
      * [Pinterest转化跟踪](https://exchange.adobe.com/apps/ec/100523)
      * [像素加载器](https://exchange.adobe.com/apps/ec/100152)
      * [Qualtrics网站反馈](https://exchange.adobe.com/apps/ec/101569)
      * [量子量度](https://exchange.adobe.com/apps/ec/101535)
      * [解决动量](https://exchange.adobe.com/apps/ec/108352)
      * [Rokt](https://exchange.adobe.com/apps/ec/107591)
      * [SDI调查](https://exchange.adobe.com/apps/ec/102991)
      * [SDI工具包](https://exchange.adobe.com/apps/ec/101460)
      * [会话摄像头](https://exchange.adobe.com/apps/ec/100517)
      * [存储扳手](https://exchange.adobe.com/apps/ec/102990)
      * 按循环水平线的[标记](https://exchange.adobe.com/apps/ec/106092)
      * [Tealium收集](https://exchange.adobe.com/apps/ec/104217)
      * [Tealium数据扩充](https://exchange.adobe.com/apps/ec/104217)
      * [TMMData基础平台](https://exchange.adobe.com/apps/ec/100148)
      * [TrustArc Cookie同意管理器](https://exchange.adobe.com/apps/ec/107037)
      * [Vimeo播放](https://exchange.adobe.com/apps/ec/108937)
      * [Web重要信息](https://exchange.adobe.com/apps/ec/106769)
      * [XDM编辑器](https://exchange.adobe.com/apps/ec/106062)
      * [Yext转化跟踪](https://exchange.adobe.com/apps/ec/103174)
      * [[!DNL Youtube] 播放](https://exchange.adobe.com/apps/ec/104160)
      * [!DNL YouTube]视频跟踪{#youtube}
         * [概述](./extensions/client/youtube/overview.md)
         * [发行说明](./extensions/client/youtube/release-notes.md)
   * 事件转发扩展（服务器端） {#server}
      * [概述](./extensions/server/overview.md)
      * Adobe Experience Platform Cloud Connector {#cloud-connector}
         * [概述](./extensions/server/cloud-connector/overview.md)
         * [发行说明](./extensions/server/cloud-connector/release-notes.md)
      * [!DNL AWS] {#aws}
         * [概述](./extensions/server/aws/overview.md)
      * [!DNL Braze] {#braze}
         * [概述](./extensions/server/braze/overview.md)
      * 适用于Google Analytics的[Cloud Connector](https://exchange.adobe.com/apps/ec/106542)
      * 核心{#core}
         * [概述](./extensions/server/core/overview.md)
      * [Epsilon事件API](https://exchange.adobe.com/apps/ec/109127)
      * Google Ads增强型转化{#google-ads-enhanced-conversions}
         * [概述](./extensions/server/google-ads-enhanced-conversions/overview.md)
      * Google Cloud Platform {#google-cloud-platform}
         * [概述](./extensions/server/google-cloud-platform/overview.md)
      * [!DNL LinkedIn Conversions API] {#linkedin}
         * [概述](./extensions/server/linkedin/overview.md)
      * [!DNL Mailchimp] Edge {#mailchimp}
         * [概述](./extensions/server/mailchimp/overview.md)
      * [!DNL Meta Conversions API] {#meta}
         * [概述](./extensions/server/meta/overview.md)
      * [!DNL Microsoft Azure] {#azure}
         * [概述](./extensions/server/azure/overview.md)
      * [!DNL Mixpanel] {#mixpanel}
         * [概述](./extensions/server/mixpanel/overview.md)
      * [Pega客户决策中心](https://exchange.adobe.com/apps/ec/107597)
      * [!DNL Pinterest] {#pinterest}
         * [概述](./extensions/server/pinterest/overview.md)
      * [!DNL Snapchat] {#snap}
         * [概述](./extensions/server/snap/overview.md)
      * [!DNL Snowflake] {#snowflake}
         * [概述](./extensions/server/snowflake/overview.md)
      * [!DNL Splunk] {#splunk}
         * [概述](./extensions/server/splunk/overview.md)
      * [!DNL Twitter] {#twitter}
         * [概述](./extensions/server/twitter/overview.md)
      * [!DNL Tiktok] Web事件API {#tiktok}
         * [概述](./extensions/server/tiktok/overview.md)
      * [!DNL The Trade Desk] {#thetradedesk}
         * [概述](./extensions/server/tradedesk/overview.md)
      * [!DNL Zendesk]事件API {#zendesk}
         * [概述](./extensions/server/zendesk/overview.md)
* 扩展开发 {#extension-dev}
   * [概述](./extension-dev/overview.md)
   * [快速入门](./extension-dev/getting-started.md)
   * [支持的浏览器](./extension-dev/browsers.md)
   * 提交流程 {#submit}
      * [概述](./extension-dev/submit/overview.md)
      * [组织设置](./extension-dev/submit/setup.md)
      * [授予用户访问权限](./extension-dev/submit/access.md)
      * [开发扩展](./extension-dev/submit/develop.md)
      * [创建 Exchange 列表](./extension-dev/submit/create-listing.md)
      * [创建扩展包zip](./extension-dev/submit/create-extension-package-zip.md)
      * [上载和实施端到端测试](./extension-dev/submit/upload-and-test.md)
      * [发布扩展](./extension-dev/submit/release.md)
   * [扩展配置](./extension-dev/configuration.md)
   * [扩展清单](./extension-dev/manifest.md)
   * Web扩展{#web}
      * [扩展流程](./extension-dev/web/flow.md)
      * [库模块格式](./extension-dev/web/format.md)
      * [视图](./extension-dev/web/views.md)
      * [事件类型](./extension-dev/web/event-types.md)
      * [条件类型](./extension-dev/web/condition-types.md)
      * [操作类型](./extension-dev/web/action-types.md)
      * [数据元素类型](./extension-dev/web/data-element-types.md)
      * [核心模块](./extension-dev/web/core.md)
      * [共享模块](./extension-dev/web/shared.md)
   * Edge扩展{#edge}
      * [扩展流程](./extension-dev/edge/flow.md)
      * [库模块格式](./extension-dev/edge/format.md)
      * [条件类型](./extension-dev/edge/condition-types.md)
      * [操作类型](./extension-dev/edge/action-types.md)
      * [数据元素类型](./extension-dev/edge/data-element-types.md)
      * [上下文参数](./extension-dev/edge/context.md)
   * [托管第三方库](./extension-dev/third-party-libraries.md)
   * [Turbine 自由变量](./extension-dev/turbine.md)
   * [向后兼容标准](./extension-dev/backwards-compatibility.md)
* Reactor API {#api}
   * [概述](./api/overview.md)
   * [身份验证和访问Reactor API](./api/getting-started.md)
   * 端点{#endpoints}
      * [公司](./api/endpoints/companies.md)
      * [属性](./api/endpoints/properties.md)
      * [数据元素](./api/endpoints/data-elements.md)
      * [规则](./api/endpoints/rules.md)
      * [规则组件](./api/endpoints/rule-components.md)
      * [扩展包](./api/endpoints/extension-packages.md)
      * [扩展包使用授权](./api/endpoints/extension-package-usage-authorizations.md)
      * [扩展](./api/endpoints/extensions.md)
      * [库](./api/endpoints/libraries.md)
      * [内部版本](./api/endpoints/builds.md)
      * [环境](./api/endpoints/environments.md)
      * [托管](./api/endpoints/hosts.md)
      * [应用程序配置](./api/endpoints/app-configurations.md)
      * [审核事件](./api/endpoints/audit-events.md)
      * [回调](./api/endpoints/callbacks.md)
      * [注释](./api/endpoints/notes.md)
      * [轮廓](./api/endpoints/profile.md)
      * [搜索](./api/endpoints/search.md)
      * [密钥](./api/endpoints/secrets.md)
   * 指南 {#guides}
      * [委托描述符ID](./api/guides/delegate-descriptor-ids.md)
      * [加密值](./api/guides/encrypting-values.md)
      * [错误处理](./api/guides/error-handling.md)
      * [共享专用扩展包](./api/guides/extension-packages.md)
      * [筛选响应](./api/guides/filtering.md)
      * [分页响应](./api/guides/pagination.md)
      * [排序响应](./api/guides/sorting.md)
      * [关系](./api/guides/relationships.md)
      * [搜索资源](./api/guides/search.md)
      * [密钥](./api/guides/secrets.md)
* [常见问题解答](./faq.md)
* [术语更新](./term-updates.md)
* [弃用对Internet Explorer 10和11的支持](./ie-deprecation.md)
* [Experience Platform 发行说明](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/release-notes/latest)

