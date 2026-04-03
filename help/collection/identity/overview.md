---
title: 数据收集中的身份
description: 了解数据收集如何在Web实施中使用ECID、核心ID、第一方持久性和identityMap。
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# 数据收集中的身份

Adobe数据收集使用身份信号来识别回访访客，并在体验之间传输上下文。 当访客访问您的网站时，Edge Network会生成一个Experience Cloud ID (ECID)，并将其保留在第一方Cookie中。 该ECID是跨Adobe Experience Cloud应用程序使用的主要设备标识符，是Analytics、个性化和受众激活构建的基础。 在您的实施中，您可以通过[`getIdentity`](/help/collection/js/commands/getidentity.md)命令在客户端访问访客的ECID。 在数据流级别，您可以使用用于数据收集[的](/help/datastreams/data-prep.md)数据准备在到达下游服务之前将ECID映射到自定义XDM字段中。

ECID可识别设备，而不是人员。 要将活动绑定到已知人员，您可以使用XDM [`identityMap`](./identity-map.md)在ECID之外发送其他标识符，如CRM ID或哈希电子邮件。 Adobe建议只要有个人级别的命名空间，就将其设置为[主身份](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map)。

在默认ECID之外，数据收集还支持其他身份信号，具体取决于您的实施：

* **第一方设备ID (FPID)**：在您控制的基础架构上生成并管理的设备标识符。 Edge Network使用FPID [为ECID](./fpid.md)提供种子，这样在浏览器限制缩短Adobe管理的Cookie的生命周期时，您就可以在拥有的属性上获得更强的Cookie持久性。
* **核心ID**：在第三方Cookie可用时参与第三方身份工作流的基于Demdex的单独标识符。 CORE ID与ECID不同，可以通过[`getIdentity`](/help/collection/js/commands/getidentity.md)进行检索。 有关第一方和第三方身份上下文如何协同工作的详细信息，请参阅[统一身份支持](./unified-identity-support.md)。

如果要从访客API升级或协调旧的标识行为，请参阅[`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md)以迁移现有的AMCV Cookie。

## 第一方和第三方收藏集 {#first-party-and-third-party-collection}

Web SDK始终将标识[Cookie](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk)（如`kndctr_` Cookie）设置为域上的第一方Cookie，无论哪个端点接收数据收集请求。 收集端点（实施将数据发送到的域）是一个单独的选择，它影响浏览器和网络策略处理请求本身的方式。

**第一方收集**&#x200B;使用指向Adobe的Edge Network的CNAME，通过贵组织控制的域（例如，`data.example.com`）路由数据收集请求。 由于该请求驻留在您的域中，因此不太可能被广告拦截器或浏览器网络限制阻止。 第一方集合也是从您自己的服务器基础结构设置[第一方设备ID](./fpid.md)的先决条件，这是可用的最持久标识策略。 Adobe建议使用[Adobe管理的证书计划](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert)来配置实施的第一方收藏集。

**第三方收藏集**&#x200B;将请求直接发送到Adobe拥有的[`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md)（如`example.data.adobedc.net`）。 虽然身份Cookie仍被设置为域中的第一方，但请求本身会转到第三方域，而一些浏览器和广告拦截器可以限制该域。

## 选择正确的身份模式 {#choose-your-path}

* **加强拥有的属性上的标识持久性**：在浏览器限制缩短Cookie生命周期并且您需要在您控制的网站上更连续地进行分析和个性化时，使用[第一方设备ID](./fpid.md)。
* **将标识从应用程序传递到移动Web**：当访客在移动应用程序中启动并在WebView或移动网页中继续时，请使用[移动到Web的标识共享](./mobile-to-web.md)。
* **跨域保持标识连续**：当访客在您组织拥有的Web资产之间移动并且您希望一致的报告和个性化时，请使用[跨域共享](./cross-domain-sharing.md)。
* **将第一方持久性与第三方激活相结合**：当您需要持久的第一方标识以及支持的第三方激活流时，请使用[统一标识支持](./unified-identity-support.md)。
* **发送人员级别标识符**：使用[`identityMap`](./identity-map.md)在ECID旁边发送CRM ID、经过哈希处理的电子邮件和其他人员级别标识符，以便下游服务能够将活动与已知人员拼合在一起。
* **了解同意如何影响身份**：阅读[同意和身份](./consent.md)，了解`defaultConsent`和`setConsent`如何控制Web SDK何时生成ECID、设置Cookie以及发送数据。

如需帮助诊断身份问题，如访客虚增、ECID不一致或FPID问题，请参阅[身份疑难解答](./troubleshooting.md)。
