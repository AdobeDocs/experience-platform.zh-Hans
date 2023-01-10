---
keywords: RTCDP;CDP;Real-time Customer Data Platform；实时客户数据平台；实时CDP;RTCDP
title: Real-time Customer Data Platform B2B Edition的示例用例
description: 此样板场景提供一个示例，其中配置您实施的 Adobe Real-Time Customer Data Platform B2B 版本。
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 2%

---

# Real-time Customer Data Platform B2B Edition的示例用例

Real-time Customer Data Platform B2B Edition扩展了现有的Real-Time CDP和Adobe Experience Platform产品，以支持B2B数据和工作流。 本文档提供了一个示例用例，用于演示B2B Edition提供的其他优势。 其中包括：

- 将来自不同孤立数据源的人员和帐户数据组合在一起，以生成一个全面的视图，从而更好地了解客户并更准确地细分客户。 请参阅 [创建XDM模式关系](./schemas/b2b.md) 用于不同的B2B源，以获取更多信息。
- 根据相关实体的属性对受众进行分段。 这包括“帐户”、“机会”、“营销活动”和“营销列表”。 区段不再仅限于人员属性和体验事件。 请参阅 [B2B分段文档](./segmentation/b2b.md) 有关创建特定于B2B的受众的更多示例。
- 本地支持一个人与多个帐户相关的用例。

## 用例

科技公司Bodea有一款新产品，希望同时通过电子邮件和LinkedIn广告活动来定位客户。 为了最大限度地提高其营销活动的效率，Bodea还希望定位与该现有帐户相关的人员，这些人员以前在其产品上花费了超过100万美元，并且AND在上个月访问了新产品页面。

然而，Bodea有两个不同的业务领域。 Bodea的第一线业务“第一线”为汽车行业创建软件。 其第二线业务“2号线”销售制造汽车部件的3D打印机。 由于Bodea的两项业务，从Bodea的客户帐户中产生的收入数据在单一视图中并不统一。

每个业务部门都有自己的销售系统：“CRM 1”和“CRM 2”。 这两个CRM销售系统均与各自的营销自动化平台“Marketo 1”和“Marketo 2”相连。 来自CRM 1的数据将仅同步到Marketo 1，而来自CRM2的数据将仅同步到Marketo 2。 最终，他们的数据将在不同的公司信息孤岛中维护。

## 当前数据情况

由于Bodea的两项业务向汤森公司销售，汤森业务数据将记录为每个销售系统中两个单独的帐户。

在Marketo 1中，Townsend被记录为帐户1。 它有两名相关人员(p1@townsend.com和p2@townsend.com)，在CRM 1中有一个价值20万美元（“机会1”）的闭门销售机会。 该数据会从CRM 1同步到Marketo 1。

在Marketo 2中，Townsend被记录为帐户2。 客户2还有两名相关人员(p2@townsend.com和p3@townsend.com)，以及CRM 2中一个价值90万美元（“机会2”）的闭门销售机会。 该数据会从CRM 2同步到Marketo 2。

为了进行集成和进行其他公司控制，Bodea还拥有主控数据管理(MDM)系统，其中保留了记录，表明Marketo 1中的帐户1（和CRM 1）和Marketo 2中的帐户2（和CRM 2）是同一公司。

上个月， `p2@townsend.com` 访问了新产品页面，Marketo 1记录了网站访问。

![帐户信息图](./assets/account-info.png)

## 问题

第一线刚刚发布了一款新的软件产品，并希望将其向上销售给Bodea现有的顶级客户群。 Bodea会在启动营销活动时考虑特定目标受众。

由于相关汤森信息被记录为Marketo 1的帐户1和Marketo 2的帐户2，因此Bodea的营销团队无法有效地利用孤立的信息。

这禁止Bodea的营销团队利用这一新机会高效地定位这些公司的特定业务联系人。

迄今为止，汤森公司在其所有账户中累计花费了超过100万美元购买Bodea产品。 但是，使用旧系统创建的区段将不包括来自汤森的任何人，除非在单个销售系统中花费的总金额超过100万美元。 这是因为收入数据位于不同销售系统下的帐户中。

由于汤森的支出分为不同的销售系统，且个人总数不超过100万，因此该部门找不到任何符合Marketo 1或Marketo 2的资格。

### Real-Time CDP B2B Edition如何解决此问题

借助Real-Time CDP B2B Edition，Bodea的营销团队可以：

- 将来自所有不同来源(多个Marketo和CRM实例，以及主控数据管理)的数据合并到Real-Time CDP B2B Edition中。

借助RT-CDP B2B Edition，Bodea可以使用Marketo Engage源连接器将Marketo 1和Marketo 2中的B2B数据引入Experience Platform，并使用与平台连接的应用程序保持此数据的最新状态。 请参阅 [Marketo源连接器](../sources/connectors/adobe-applications/marketo/marketo.md) 文档以了解更多信息。

CRM1中的B2B数据（人员、帐户、机会和活动）会同步到Marketo 1。 同样，来自CRM 2的所有B2B数据也会同步到Marketo 2。 它们通过Marketo源连接器同步到Adobe Experience Platform。 但是，如果Bodea希望将CRM中的其他数据导入Experience Platform，则他们可以使用现有的CRM连接器。

为了简单起见和此示例的目的，人们正在通过电子邮件进行识别。 此示例的组合帐户数据如下所示：

| 人员 |
|---|
| p1@townsend.com |
| p2@townsend.com（上个月谁访问了新产品页面） |
| p3@townsend.com |

| 机会（闭门） |
|---|
| 机会1, 20万美元 |
| 机会2,90万美元 |

- 使用此汇总数据创建独特区段，以用于各种营销计划。 在此示例中，区段会查找以下所有人员：

   - （跨所有帐户）的相关机会价值超过100万美元
   - AND
   - 在上个月访问过产品页面

- 创建受众，使其成为Bodea新营销活动的最高效收件人。 在此示例中，RT-CDP B2B Edition将帮助营销人员识别 `p2@townsend.com` 作为此营销活动的正确目标。

通过使用Marketo Engage和LinkedIn目标，Bodea为其营销团队提供了端到端客户体验管理(CXM)解决方案。 在Experience Platform中创建的受众会推送到Marketo目标，该目标将显示为静态列表。 然后，此受众会自动添加到Marketo营销活动中。 同时，受众也可以通过RT-CDP B2B Edition发送到LinkedIn营销活动。

## 后续步骤

通过阅读本文档，您现在已介绍了使用Real-Time CDP B2B Edition可解决的目标和问题的类型。

为了提高您对B2B特定功能的了解，建议使用以下文档：

- [Real-time Customer Data Platform B2B Edition端到端教程](./b2b-tutorial.md)
- [Real-time Customer Data Platform B2B版中的源](./sources/b2b.md)
- [Real-time Customer Data Platform B2B版中的模式](./schemas/b2b.md)
- [B2B分段示例](./segmentation/b2b.md)
- [帐户配置文件概述](./accounts/account-profile-overview.md)
- [Real-time Customer Data Platform B2B版中的目标](./destinations/b2b.md)
- [配置LinkedIn匹配的受众目标](../destinations/catalog/social/linkedin.md)
