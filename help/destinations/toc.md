---
audience: user
user-guide-title: 目标指南
user-guide-description: 针对跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例，激活您的已知和未知数据。
description: 本文档列出了Adobe Experience Platform目标的目录
feature: Destinations
source-git-commit: 30e75b8fbaa4a8269a32f82ade435b67767630c5
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 7%

---


# 目标 {#destinations}

* [目标概述](./home.md)
* [目标类型和类别](./destination-types.md)
* API教程 {#api}
   * [使用流服务API连接到流目标并激活数据](./api/streaming-destinations.md)
   * [连接到批量云存储和电子邮件营销目标，并使用流程服务API激活数据](./api/connect-activate-batch-destinations.md)
   * [（测试版）通过临时激活API将受众区段激活到批量目标](./api/ad-hoc-activation-api.md)
   * [更新目标数据流](./api/update-destination-dataflows.md)
   * [删除目标帐户](./api/delete-destination-account.md)
   * [删除目标数据流](./api/delete-destination-dataflow.md)
* UI指南 {#ui}
   * [目标工作区](./ui/destinations-workspace.md)
   * [创建新目标连接](./ui/connect-destination.md)
   * 将受众数据激活到目标{#activate}
      * [激活概述](./ui/activation-overview.md)
      * [将受众数据激活到流区段导出目标](./ui/activate-segment-streaming-destinations.md)
      * [将受众数据激活到流配置文件导出目标](./ui/activate-streaming-profile-destinations.md)
      * [激活受众数据以批量配置文件导出目标](./ui/activate-batch-profile-destinations.md)
      * [将受众数据激活到用户档案请求目标](./ui/activate-profile-request-destinations.md)
      * [为同一页面和下一页面个性化配置个性化目标](./ui/configure-personalization-destinations.md)
      * [（测试版）使用Experience PlatformUI将文件按需导出到批量目标](./ui/export-file-now.md)
   * [查看目标详细信息](./ui/destination-details-page.md)
   * [更新目标帐户](./ui/update-accounts.md)
   * [删除目标帐户](./ui/delete-destination-account.md)
   * [编辑激活数据流](./ui/edit-activation.md)
   * [删除目标](./ui/delete-destinations.md)
   * [监视数据流](./ui/monitor-dataflows.md)
   * [订阅上下文关联目标警报](ui/alerts.md)
* 目标目录 {#catalog}
   * [目标目录概述](./catalog/overview.md)
   * Adobe目标{#adobe}
      * [Adobe目标概述](./catalog/adobe/overview.md)
      * [Marketo Engage连接](./catalog/adobe/marketo-engage.md)
      * [Experience Platform区段共享](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
   * 广告目标{#advertising}
      * [广告目标概述](./catalog/advertising/overview.md)
      * [Adobe Advertising Cloud连接](./catalog/advertising/adobe-advertising-cloud-connection.md)
      * [Adobe Advertising Cloud扩展](./catalog/advertising/adobe-advertising-cloud.md)
      * [Awin广告商转化标记扩展](./catalog/advertising/awin-conversiontag.md)
      * [Awin广告商Mastertag扩展](./catalog/advertising/awin-mastertag.md)
      * [Bing Ads通用事件跟踪(UET)扩展](./catalog/advertising/bing-ads.md)
      * [分支扩展](./catalog/advertising/branch.md)
      * [(Beta)Criteo连接](./catalog/advertising/criteo.md)
      * [DoubleClick Floodlight（测试版）扩展](./catalog/advertising/doubleclick-floodlight.md)
      * [Facebook Pixel扩展](./catalog/advertising/facebook-pixel.md)
      * [Flashtalking OneTag扩展](./catalog/advertising/flashtalking.md)
      * [Google Ads连接](./catalog/advertising/google-ads-destination.md)
      * [Google Ads扩展](./catalog/advertising/google-ads-extension.md)
      * [Google Ad Manager连接](./catalog/advertising/google-ad-manager.md)
      * [（测试版）Google Ad Manager 360连接](./catalog/advertising/google-ad-manager-360-connection.md)
      * [Google客户匹配连接](./catalog/advertising/google-customer-match.md)
      * [Google Display &amp; Video 360连接](./catalog/advertising/google-dv360.md)
      * [Google扩展](./catalog/advertising/gtag-advertising.md)
      * [linkedIn Insight Tag扩展](./catalog/advertising/linkedin.md)
      * [Microsoft Bing连接](./catalog/advertising/bing.md)
      * [Pinterest转化跟踪扩展](./catalog/advertising/pinterest-extension.md)
      * [Pinterest客户列表连接](./catalog/advertising/pinterest.md)
      * [（测试版）Snapchat Ads连接](./catalog/advertising/snap-inc.md)
      * [交易台连接](./catalog/advertising/tradedesk.md)
      * [（测试版）交易台CRM连接](./catalog/advertising/tradedesk-emails.md)
      * [Twitter通用网站标记扩展](./catalog/advertising/twitter-uwt.md)
      * [Yahoo/Verizon DataX连接](./catalog/advertising/datax.md)
   * Analytics目标 {#analytics}
      * [Analytics目标概述](./catalog/analytics/overview.md)
      * [Adform网站跟踪扩展](./catalog/analytics/adform.md)
      * [Adobe Analytics 扩展](./catalog/analytics/adobe-analytics.md)
      * [Adobe Media Analytics for Audio and Video 扩展](./catalog/analytics/adobe-video-analytics.md)
      * [Clicktale扩展](./catalog/analytics/clicktale.md)
      * [Contentsquare扩展](./catalog/analytics/contentsquare.md)
      * [分贝扩展](./catalog/analytics/decibel.md)
      * [Demandbase扩展](./catalog/analytics/demandbase.md)
      * [DialogTech扩展](./catalog/analytics/dialogtech.md)
      * [Google全局网站标记扩展](./catalog/analytics/gtag-analytics.md)
      * [Google Universal Analytics扩展](./catalog/analytics/google-universal-analytics.md)
      * [JW Player Analytics（测试版）扩展](./catalog/analytics/jw-player-analytics.md)
      * [Nielsen BSDK扩展](./catalog/analytics/nielsen-bsdk.md)
      * [Nielsen IMA处理程序扩展](./catalog/analytics/nielsen-ima.md)
      * [Nielsen VideoJS播放器处理程序扩展](./catalog/analytics/nielsen-videojs.md)
      * [Parse.ly Analytics扩展](./catalog/analytics/parsely.md)
      * [量度扩展](./catalog/analytics/quantum-metric.md)
      * [SessionCam扩展](./catalog/analytics/sessioncam.md)
      * [TMMData扩展](./catalog/analytics/tmmdata.md)
      * [Yext转化跟踪扩展](./catalog/analytics/yext.md)
   * 云存储目标 {#cloud-storage}
      * [云存储目标概述](./catalog/cloud-storage/overview.md)
      * [Amazon Kinesis连接](./catalog/cloud-storage/amazon-kinesis.md)
      * [Amazon S3连接](./catalog/cloud-storage/amazon-s3.md)
      * [Azure Blob连接](./catalog/cloud-storage/azure-blob.md)
      * [Azure事件中心连接](./catalog/cloud-storage/azure-event-hubs.md)
      * [SFTP连接](./catalog/cloud-storage/sftp.md)
      * [云存储允许列表目标的IP地址](./catalog/cloud-storage/ip-address-allow-list.md)
   * 客户关系管理(CRM)目标 {#crm}
      * [Salesforce CRM连接](./catalog/crm/salesforce.md)
   * 数据管理平台目标 {#data-management}
      * [数据管理平台(DMP)目标概述](./catalog/data-management/overview.md)
      * [Audience ManagerDIL扩展](./catalog/data-management/aam-dil-extension.md)
   * 电子邮件目标 {#email}
      * [Bizible扩展](./catalog/email/bizible.md)
      * [Marketo扩展](./catalog/email/marketo.md)
      * [Marketo Munchkin 扩展](./catalog/email/marketo-munchkin.md)
      * [PebblePost扩展](./catalog/email/pebblepost.md)
   * 电子邮件营销目标 {#email-marketing}
      * [电子邮件营销目标概述](./catalog/email-marketing/overview.md)
      * [Adobe Campaign连接](./catalog/email-marketing/adobe-campaign.md)
      * [OracleEloqua连接](./catalog/email-marketing/oracle-eloqua.md)
      * [OracleResponsys连接](./catalog/email-marketing/oracle-responsys.md)
      * [(API)SalesforceMarketing Cloud连接](./catalog/email-marketing/salesforce-marketing-cloud-exact-target.md)
      * [（文件）SalesforceMarketing Cloud连接](./catalog/email-marketing/salesforce-marketing-cloud.md)
      * [SendGrid连接](./catalog/email-marketing/sendgrid.md)
   * 标记扩展 {#launch-extensions}
      * [标记扩展概述](./catalog/launch-extensions/overview.md)
   * 移动参与目标 {#mobile-engagement}
      * [移动设备参与目标概述](./catalog/mobile-engagement/overview.md)
      * [飞艇属性连接](./catalog/mobile-engagement/airship-attributes.md)
      * [Airship Tags连接](./catalog/mobile-engagement/airship-tags.md)
      * [Braze连接](./catalog/mobile-engagement/braze.md)
   * 个性化目标 {#personalization}
      * [个性化目标概述](./catalog/personalization/overview.md)
      * [Adobe Target连接](./catalog/personalization/adobe-target-connection.md)
      * [Adobe Target 扩展](./catalog/personalization/adobe-target.md)
      * [Adobe Target v2 扩展](./catalog/personalization/adobe-target-v2.md)
      * [Beemray扩展](./catalog/personalization/beemray.md)
      * [自定义个性化连接](./catalog/personalization/custom-personalization.md)
      * [D&amp;B Visitor Intelligence扩展](./catalog/personalization/dnb.md)
      * [Experience Cloud ID 服务扩展](./catalog/personalization/adobe-ecid.md)
      * [Gainsight扩展](./catalog/personalization/gainsight.md)
      * [KickFire扩展](./catalog/personalization/kickfire.md)
      * [Marketo Web个性化扩展](./catalog/personalization/marketo-web-personalization.md)
      * [Pega客户决策中心连接](./catalog/personalization/pega.md)
   * 社交目标{#social}
      * [社交目标概述](./catalog/social/overview.md)
      * [AdobeLivefyre扩展](./catalog/social/adobe-livefyre.md)
      * [Facebook连接](./catalog/social/facebook.md)
      * [linkedIn匹配的受众连接](./catalog/social/linkedin.md)
      * [[!DNL Twitter Custom Audiences] 连接](./catalog/social/twitter.md)
   * 流目标 {#streaming}
      * [HTTP API连接](./catalog/streaming/http-destination.md)
      * [流目允许列表标的IP地址](./catalog/streaming/ip-address-allow-list.md)
   * 调查目标 {#survey}
      * [Survey目标概述](./catalog/survey/overview.md)
      * [Foresee扩展目标](./catalog/survey/foresee.md)
      * [InMoment扩展](./catalog/survey/inmoment.md)
      * [Qualtrics网站反馈扩展](./catalog/survey/qualtrics.md)
      * [QuestionPro截距调查扩展](./catalog/survey/web-intercept-surveys.md)
   * 客户目标之声 {#voice}
      * [客户目标之声概述](./catalog/voice/overview.md)
      * [确认数字反馈扩展](./catalog/voice/confirmit-digital-feedback.md)
      * [Invoca标记扩展](./catalog/voice/invoca.md)
      * [Medallia连接](./catalog/voice/medallia-connector.md)
      * [Medallia扩展](./catalog/voice/medallia.md)
      * [Talk URL Inbox扩展](./catalog/voice/talkurl.md)
* 目标 SDK {#destination-sdk}
   * [概述](./destination-sdk/overview.md)
   * [集成先决条件](./destination-sdk/integration-prerequisites.md)
   * [快速入门](./destination-sdk/getting-started.md)
   * Destination SDK功能 {#functionality}
      * [配置选项](./destination-sdk/configuration-options.md)
      * [流目标配置](./destination-sdk/destination-configuration.md)
      * [（测试版）基于文件的目标配置](./destination-sdk/file-based-destination-configuration.md)
      * [流目标服务器和模板规范](./destination-sdk/server-and-template-configuration.md)
      * [（测试版）基于文件的目标服务器和文件规范](./destination-sdk/server-and-file-configuration.md)
      * [消息格式](./destination-sdk/message-format.md)
      * [受众元数据管理](./destination-sdk/audience-metadata-management.md)
      * 身份验证 {#authentication}
         * [身份验证配置](./destination-sdk/authentication-configuration.md)
         * [OAuth 2身份验证](./destination-sdk/oauth2-authentication.md)
      * 开发人员工具 {#developer-tools}
         * [创建和测试消息转换模板](./destination-sdk/create-template.md)
         * [测试目标配置](./destination-sdk/test-destination.md)
   * API操作 {#api}
      * [Destination SDK（目标创作）API引用](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)
      * [目标端点API操作](./destination-sdk/destination-configuration-api.md)
      * [目标服务器端点API操作](./destination-sdk/destination-server-api.md)
      * [受众元数据端点API操作](./destination-sdk/audience-metadata-api.md)
      * [凭据端点API操作](./destination-sdk/credentials-configuration-api.md)
      * [发布端点API操作](./destination-sdk/destination-publish-api.md)
      * 开发人员工具参考 {#developer-tools-reference}
         * 流目标测试API {#streaming-destination-testing-api}
            * [获取示例模板API操作](./destination-sdk/sample-template-api.md)
            * [渲染模板API操作](./destination-sdk/render-template-api.md)
            * [目标测试API操作](./destination-sdk/destination-testing-api.md)
            * [配置文件生成API操作示例](./destination-sdk/sample-profile-generation-api.md)
         * 基于文件的目标测试API {#file-based-destination-testing-api}
            * [基于文件的目标测试API概述](./destination-sdk/file-based-destination-testing-overview.md)
            * [根据源架构生成示例用户档案](./destination-sdk/file-based-sample-profile-generation-api.md)
            * [使用示例用户档案测试基于文件的目标](./destination-sdk/file-based-destination-testing-api.md)
            * [查看详细的激活结果](./destination-sdk/file-based-destination-results-api.md)
            * [验证模板化客户字段](./destination-sdk/file-based-render-template-api.md)
   * 指南 {#guides}
      * [使用Destination SDK配置流目标](./destination-sdk/configure-destination-instructions.md)
      * [（测试版）使用Destination SDK配置基于文件的目标](./destination-sdk/configure-file-based-destination-instructions.md)
      * [提交以供审核在Destination SDK中创作的目标](./destination-sdk/submit-destination.md)
   * 参考 {#reference}
      * [流目标的速率限制和重试策略](./destination-sdk/rate-limiting-retry-policy.md)
      * [支持的转换函数](./destination-sdk/supported-functions.md)
   * 记录目标 {#document-destination}
      * [在Adobe Experience Platform中记录您的目标](./destination-sdk/docs-framework/documentation-instructions.md)
      * [使用GitHub Web界面创建目标文档页面](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [在本地环境中使用文本编辑器创建目标文档页面](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [文档自助模板](./destination-sdk/docs-framework/self-service-template.md)
      * [创作最佳实践](./destination-sdk/docs-framework/authoring-best-practices.md)
* [常见问题解答](./destinations-faq.md)
* [平台发行说明](https://www.adobe.com/go/platform-release-notes-en)
