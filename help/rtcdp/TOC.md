---
product: adobe experience platform
solution: Real-Time Customer Data Platform
audience: user
user-guide-title: Real-Time Customer Data Platform 指南
user-guide-description: 合并多个企业来源的已知数据和匿名数据，以创建客户轮廓、从这些轮廓创建受众，以及将这些受众激活到第三方目标。
role: Admin
source-git-commit: 74a73b568c850f8e749afea039afd2821858bd69
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 62%

---


# Real-Time Customer Data Platform 帮助 {#rtcdp}

* [Real-Time CDP文档](home.md)
* 快速入门 {#intro}
   * Real-Time CDP {#rtcdp-intro}
      * [Real-Time CDP 概述](overview.md)
      * [开始使用 Real-Time CDP](get-started.md)
      * [主页](home-page-dashboards.md)
   * Real-Time CDP B2B Edition {#rtcdpb2b-intro}
      * [Real-Time CDP B2B 版概述](b2b-overview.md)
      * [示例用例](./b2b-use-case.md)
      * [端到端教程](./b2b-tutorial.md)
      * [Real-Time CDP B2B 版护栏](b2b-guardrails.md)
      * [Real-Time CDP B2B edition架构升级](b2b-architecture-upgrade.md)
* Audience Manager和Real-Time CDP {#evolution}
   * [从 Audience Manager 的演变](aam-to-rtcdp.md)
* 帐户轮廓 {#account}
   * [账户资料概述](accounts/account-profile-overview.md)
   * [帐户轮廓 UI 指南](accounts/account-profile-ui-guide.md)
* 管理 {#admin}
   * [管理概述](administration/admin-overview.md)
* 受众和分段 {#segmentation}
   * [分段概述](segmentation/segmentation-overview.md)
   * [Audience Builder指南](segmentation/audience-builder.md)
   * [Real-Time CDP B2B 版本中的分段](segmentation/b2b.md)
   * [客户人工智能](segmentation/customer-ai.md)
* 数据集 {#datasets}
   * [数据集](datasets/dataset.md)
   * [Experience Platform上的数据质量](datasets/data-quality.md)
* 目标 {#destinations}
   * [目标概述](destinations/overview.md)
   * [Real-Time CDP B2B 版本中的目标](destinations/b2b.md)
* 护栏 {#guardrails}
   * [Real-Time CDP护栏概述](guardrails/overview.md)
   * [用于数据引入的护栏](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html?lang=zh-Hans){target="_blank"}
   * [&#x200B; [!DNL Edge Network API]的护栏](https://developer.adobe.com/data-collection-apis/docs/getting-started/guardrails/){target="_blank"}
   * [针对 [!DNL Real-Time Customer Profile] 数据和分段的护栏](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=zh-Hans){target="_blank"}
   * [数据 [!DNL Identity Service] 的护栏](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=zh-Hans){target="_blank"}
   * [&#x200B; [!DNL Query Service]的护栏](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=zh-Hans){target="_blank"}
   * [通过目标激活数据的护栏](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=zh-Hans){target="_blank"}
* 身份标识 {#identity}
   * [身份标识和身份标识命名空间](profile/identities-overview.md)
* 合并策略 {#merge-policies}
   * [合并策略概述](profile/merge-policies.md)
* 隐私和数据治理 {#privacy}
   * [隐私概述](privacy/privacy-overview.md)
   * [数据治理概述](privacy/data-governance-overview.md)
* 用户档案 {#profile}
   * [轮廓概述](profile/profile-overview.md)
   * [轮廓浏览](profile/profile-browse.md)
* Real-Time CDP B2B edition AI/ML服务 {#b2b-cdp-ai-ml}
   * [相关帐户](b2b-ai-ml-services/related-accounts.md)
   * [导致账户匹配](b2b-ai-ml-services/lead-to-account-matching.md)
   * 预测性商机和客户评分 {#predictive-lead-and-account-scoring-intro}
      * [预测性商机和客户评分概述](b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
      * [管理预测性商机和客户评分](b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md)
* 架构 {#schemas}
   * [架构概述](schemas/overview.md)
   * [Real-Time CDP B2B 版本中的架构](schemas/b2b.md)
* 源 {#sources}
   * [源概述](sources/sources-overview.md)
   * [Real-Time CDP B2B 版本中的源](sources/b2b.md)
* 用例 {#use-cases}
   * [示例用例概述](/help/rtcdp/use-case-guides/overview.md)
   * 客户获取 {#customer-acquisition}
      * [在不依赖第三方Cookie的情况下吸引和获取新客户](/help/rtcdp/partner-data/prospecting.md)
      * [使用合作伙伴辅助的访客识别功能，为未知访客提供个性化的现场体验](/help/rtcdp/partner-data/onsite-personalization.md)
      * [未经身份验证的用户异地重定向](./partner-data/offsite-retargeting.md)
      * [未经身份验证的服务器端重定位](./partner-data/unauthenticated-retargeting.md)
   * 轮廓扩充 {#profile-enrichment}
      * [用合作伙伴提供的属性补充第一方轮廓](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
   * 个性化洞察和参与 {#personalization-insights-engagement}
      * [将一次性客户价值提升至存留期价值](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md)
      * [以智能的方式重新吸引您的客户](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)
      * [智能地重新吸引客户：Luma示例](/help/rtcdp/use-case-guides/intelligent-re-engagement/use-cases-luma.md)
* [Experience Platform 发行说明](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/release-notes/latest)
* [Experience Platform 术语表](https://www.adobe.com/go/platform-glossary_cn)