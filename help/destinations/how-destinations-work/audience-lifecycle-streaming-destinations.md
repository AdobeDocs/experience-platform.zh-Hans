---
title: Experience Platform和流目标中的受众生命周期
description: 了解Experience Platform中的受众名称和映射如何反映在流式目标平台中。
source-git-commit: 6b4dfa714e078fb5b97900811aade081ffef0d78
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 2%

---


# 流目标中的受众生命周期

本页介绍Experience Platform中的受众名称更新和映射如何与流式目标平台同步。 在Experience Platform中修改受众名称或移除受众映射时，行为会因目标平台的功能而异。

了解这些差异对于管理受众生命周期操作和确保目标平台反映Experience Platform中受众的当前状态非常重要。

## 受众名称传播行为 {#audience-name-propagation}

在将受众激活到流目标时，会在初始激活期间将受众名称发送到目标。 但是，受众名称更新行为因目标而异：

* **[支持受众名称更新的目标](#name-update-supported)**：如果您在Experience Platform中更改受众名称，更新的名称将自动传播到这些目标。
* **[不支持受众名称更新的目标](#name-update-not-supported)**：如果您在Experience Platform中更改受众名称，则目标将继续使用初始激活的原始名称。

### 支持受众名称更新的目标 {#name-update-supported}

当您在Experience Platform中修改受众名称时，以下流目标支持自动受众名称更新：

* [Acxiom受众连接](../catalog/advertising/acxiom-audience-connection.md)
* [Adobe Campaign Managed Cloud](../catalog/email-marketing/adobe-campaign-managed-services.md)
* [Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [庞博拉](../catalog/advertising/bombora.md)
* [标准](../catalog/advertising/criteo.md)
* [Demandbase](../catalog/advertising/demandbase.md)
* [Demandbase人员](../catalog/advertising/demandbase-people.md)
* [Experience Cloud 受众](../catalog/adobe/experience-cloud-audiences.md)
* [Facebook自定义受众](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [（公司） LinkedIn匹配受众](../catalog/social/linkedin-b2b.md)
* [LinkedIn匹配的受众](../catalog/social/linkedin.md)
* [（旧版） (V2)Marketo Engage](../catalog/adobe/marketo-engage.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [发送网格](../catalog/email-marketing/sendgrid.md)
* [Snap Inc](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Twitter自定义受众](../catalog/social/twitter.md)
* [雅虎数据X](../catalog/advertising/datax.md)

### 不支持受众名称更新的目标 {#name-update-not-supported}

对于上面未列出的目标，受众名称在初始激活后保持静态。 如果需要更新这些目标的受众名称，您必须：

1. 在Experience Platform中使用所需的名称创建新受众
2. 将新受众激活到目标

>[!TIP]
>
>为避免混淆，请使用首次激活时的描述性受众名称，尤其是当激活到不支持受众名称更新的目标时。

## 支持受众移除的目标 {#support-removal}

当您从流目标中移除（取消映射）受众时，Experience Platform会尝试从目标平台中移除相应的受众。 但是，并非所有目标都支持此功能。

当您从目标取消映射受众时，以下流目标支持自动删除受众：

* [(API) Oracle Eloqua](../catalog/email-marketing/oracle-eloqua-api.md)
* [（公司） LinkedIn匹配受众](../catalog/social/linkedin-b2b.md)
* [（旧版） (V2)Marketo Engage](../catalog/adobe/marketo-engage.md)
* [Adobe Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Bombora帐户受众](../catalog/advertising/bombora.md)
* [标准](../catalog/advertising/criteo.md)
* [Experience Cloud 受众](../catalog/adobe/experience-cloud-audiences.md)
* [Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [HubSpot](../catalog/crm/hubspot.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [LinkedIn匹配的受众](../catalog/social/linkedin.md)
* [LiveRamp — 分发](../catalog/advertising/liveramp-distribution.md)
* [Mailchimp兴趣类别](../catalog/email-marketing/mailchimp-interest-categories.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [Salesforce Marketing Cloud帐户参与度](../catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)
* [发送网格](../catalog/email-marketing/sendgrid.md)
* [Snap Inc](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Twitter自定义受众](../catalog/social/twitter.md)
* [雅虎数据X](../catalog/advertising/datax.md)

### 不支持受众移除的目标

对于以上未列出的目标，当您从目标中取消映射受众时，Experience Platform只会删除映射。 目标平台中的受众将保持活动状态，直到您在合作伙伴平台中手动将其删除为止。
