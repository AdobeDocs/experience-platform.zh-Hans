---
keywords: Experience Platform；主页；热门主题；Marketo源连接器；命名空间；架构；b2b;B2B
solution: Experience Platform
title: B2B命名空间和架构
topic-legacy: overview
description: 本文档概述创建B2B源连接器时所需的自定义命名空间。
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1707'
ht-degree: 4%

---

# B2B命名空间和架构

本文档提供了有关命名空间和架构的基础设置信息，这些命名空间和架构将与B2B源一起使用。 本文档还提供了有关设置生成B2B命名空间和模式所需的Postman自动化实用程序的详细信息。

>[!IMPORTANT]
>
>您必须具有 [Adobe Real-time Customer Data Platform B2B版](../../../../rtcdp/b2b-overview.md) 以便B2B模式参与 [实时客户资料](../../../../profile/home.md).

## 设置B2B命名空间和模式自动生成实用程序

使用B2B命名空间和模式自动生成实用程序的第一步是设置您的平台开发人员控制台和 [!DNL Postman] 环境。

- 您可以从此处下载命名空间和模式自动生成实用程序集合和环境 [GitHub存储库](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- 有关使用Platform API的信息，包括有关如何收集所需标头值和读取示例API调用的详细信息，请参阅 [Platform API快速入门](../../../../landing/api-guide.md).
- 有关如何为Platform API生成凭据的信息，请参阅 [验证和访问Experience PlatformAPI](../../../../landing/api-authentication.md).
- 有关如何设置 [!DNL Postman] 对于Platform API，请参阅 [设置开发人员控制台和 [!DNL Postman]](../../../../landing/postman.md).

使用平台开发人员控制台和 [!DNL Postman] 设置后，您现在可以开始将相应的环境值应用到 [!DNL Postman] 环境。

下表包含示例值以及有关填充您的 [!DNL Postman] 环境：

| Variable | 描述 | 示例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用于生成 `{ACCESS_TOKEN}`. 请参阅 [验证和访问Experience PlatformAPI](../../../../landing/api-authentication.md) 有关如何检索 `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web令牌(JWT)是用于生成{ACCESS_TOKEN}的身份验证凭据。 请参阅 [验证和访问Experience PlatformAPI](../../../../landing/api-authentication.md) 以了解有关如何生成 `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | 用于验证对Experience PlatformAPI的调用的唯一标识符。 请参阅 [验证和访问Experience PlatformAPI](../../../../landing/api-authentication.md) 有关如何检索 `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成对Experience PlatformAPI的调用所需的授权令牌。 请参阅 [验证和访问Experience PlatformAPI](../../../../landing/api-authentication.md) 有关如何检索 `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 关于 [!DNL Marketo]，此值已修复，并且始终设置为： `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | 的 `global` 容器包含所有标准Adobe和Experience Platform合作伙伴提供的类、架构字段组、数据类型和架构。 关于 [!DNL Marketo]，此值是固定的，且始终设置为 `global`. | `global` |
| `PRIVATE_KEY` | 用于验证您的 [!DNL Postman] 实例Experience PlatformAPI。 请参阅有关设置开发人员控制台的教程和 [设置开发人员控制台和 [!DNL Postman]](../../../../landing/postman.md) 有关如何检索{PRIVATE_KEY}的说明。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用于集成以Adobe I/O的凭据。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management系统(IMS)为Adobe服务提供了身份验证框架。 关于 [!DNL Marketo]，此值已修复，且始终设置为： `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 拥有或许可产品和服务并允许其成员访问的公司实体。 请参阅 [设置开发人员控制台和 [!DNL Postman]](../../../../landing/postman.md) 有关如何检索 `{ORG_ID}` 信息。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您使用的虚拟沙盒分区的名称。 | `prod` |
| `TENANT_ID` | 用于确保您创建的资源命名正确且包含在IMS组织中的ID。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 您对进行API调用的URL端点。 此值是固定的，始终设置为： `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style=&quot;table-layout:auto&quot;}

### 运行脚本

使用 [!DNL Postman] 收集和环境设置之后，您现在可以通过 [!DNL Postman] 界面。

在 [!DNL Postman] 界面中，选择自动生成器实用程序的根文件夹，然后选择 **[!DNL Run]** 中。

![根文件夹](../images/marketo/root-folder.png)

的 [!DNL Runner] 界面。 从此处，确保选中所有复选框，然后选择 **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![运行发生器](../images/marketo/run-generator.png)

成功的请求会创建B2B所需的命名空间和架构。

## B2B命名空间

身份命名空间是 [[!DNL Identity Service]](../../../../identity-service/home.md) 用于区分身份的上下文或类型。 完全限定的标识包括ID值和命名空间。 请参阅 [命名空间概述](../../../../identity-service/namespaces.md) 以了解更多信息。

B2B命名空间用于实体的主标识。

下表包含有关为B2B命名空间设置的基础信息。

>[!NOTE]
>
>请向左/向右滚动以查看表的完整内容。

| 显示名称 | 身份符号 | 身份类型 |
| --- | --- | --- |
| B2B人员 | `b2b_person` | `CROSS_DEVICE` |
| B2B帐户 | `b2b_account` | `B2B_ACCOUNT` |
| B2B机会 | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| B2B机会人员关系 | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| B2B营销活动 | `b2b_campaign` | `B2B_CAMPAIGN` |
| B2B营销活动成员 | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| B2B营销列表 | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| B2B营销列表成员 | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| B2B帐户人员关系 | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style=&quot;table-layout:auto&quot;}

## B2B模式

Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。通过在整个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。

在将数据摄取到平台中之前，必须构建一个架构来描述数据的结构，并对每个字段中可包含的数据类型提供约束。 架构由基类和零个或多个架构字段组组成。

有关架构组合模型（包括设计原则和最佳实践）的更多信息，请参阅 [架构组合基础知识](../../../../xdm/schema/composition.md).

下表包含有关B2B架构的基础设置的信息。

>[!NOTE]
>
>请向左/向右滚动以查看表的完整内容。

| 架构名称 | 基类 | 字段组 | [!DNL Profile] 在模式中 | 主标识 | 主标识命名空间 | 次标识 | 次标识命名空间 | 关系 | 注释 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B帐户 | [XDM业务帐户](../../../../xdm/classes/b2b/business-account.md) | XDM业务帐户详细信息 | 已启用 | `accountKey.sourceKey` 在基类中 | B2B帐户 | `extSourceSystemAudit.externalKey.sourceKey` 在基类中 | B2B帐户 | <ul><li>`accountParentKey.sourceKey` “ XDM业务帐户详细信息”字段组中</li><li>目标属性： `/accountKey/sourceKey`</li><li>类型：一对一</li><li>引用架构：B2B帐户</li><li>命名空间：B2B帐户</li></ul> |
| B2B人员 | [XDM个人配置文件](../../../../xdm/classes/individual-profile.md) | <ul><li>XDM业务人员详细信息</li><li>XDM业务人员组件</li><li>IdentityMap</li><li>同意和首选项详细信息</li></ul> | 已启用 | `b2b.personKey.sourceKey` “ XDM业务人员详细信息”字段组中的 | B2B人员 | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` “XDM业务人员详细信息”字段组</li><li>`workEmail.address` “XDM业务人员详细信息”字段组</ol></li> | <ol><li>B2B人员</li><li>电子邮件</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` XDM业务人员组件字段组的</li><li>类型：多对一</li><li>引用架构：B2B帐户</li><li>命名空间：B2B帐户</li><li>目标属性：accountKey.sourceKey</li><li>当前架构中的关系名称：帐户</li><li>引用架构中的关系名称：人员</li></ul> |
| B2B机会 | [XDM业务机会](../../../../xdm/classes/b2b/business-opportunity.md) | XDM业务机会详细信息 | 已启用 | `opportunityKey.sourceKey` 在基类中 | B2B机会 | `extSourceSystemAudit.externalKey.sourceKey` 在基类中 | B2B机会 | <ul><li>`accountKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B帐户</li><li>命名空间：B2B帐户</li><li>目标属性： `accountKey.sourceKey`</li><li>当前架构中的关系名称：帐户</li><li>引用架构中的关系名称：机会</li></ul> |
| B2B机会人员关系 | [XDM业务机会人员关系](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | None | 已启用 | `opportunityPersonKey.sourceKey` 在基类中 | B2B机会人员关系 | `extSourceSystemAudit.externalKey.sourceKey` 在基类中 | B2B机会人员关系 | **第一关系**<ul><li>`personKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B人员</li><li>命名空间：B2B人员</li><li>目标属性：b2b.personKey.sourceKey</li><li>当前架构中的关系名称：人员</li><li>引用架构中的关系名称：机会</li></ul>**第二关系**<ul><li>`opportunityKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B机会 </li><li>命名空间：B2B机会 </li><li>目标属性： `opportunityKey.sourceKey`</li><li>当前架构中的关系名称：机会</li><li>引用架构中的关系名称：人员</li></ul> |
| B2B营销活动 | [XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign.md) | XDM Business Campaign详细信息 | 已启用 | `campaignKey.sourceKey` 在基类中 | B2B营销活动 | `extSourceSystemAudit.externalKey.sourceKey` 在基类中 | B2B营销活动 |
| B2B营销活动成员 | [XDM Business Campaign成员](../../../../xdm/classes/b2b/business-campaign-members.md) | XDM Business Campaign成员详细信息 | 已启用 | `ccampaignMemberKey.sourceKey` 在基类中 | B2B营销活动成员 | `extSourceSystemAudit.externalKey.sourceKey` 在基类中 | B2B营销活动成员 | **第一关系**<ul><li>`personKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B人员</li><li>命名空间：B2B人员</li><li>目标属性： `b2b.personKey.sourceKey`</li><li>当前架构中的关系名称：人员</li><li>引用架构中的关系名称：促销活动</li></ul>**第二关系**<ul><li>`campaignKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B营销活动</li><li>命名空间：B2B营销活动</li><li>目标属性： `campaignKey.sourceKey`</li><li>当前架构中的关系名称：Campaign</li><li>引用架构中的关系名称：人员</li></ul> |
| B2B营销列表 | [XDM业务营销列表](../../../../xdm/classes/b2b/business-marketing-list.md) | 无 | 已启用 | `marketingListKey.sourceKey` 在基类中 | B2B营销列表 | 无 | 无 | 无 | 静态列表未从同步 [!DNL Salesforce] 因此，没有辅助身份。 |
| B2B营销列表成员 | [XDM业务营销列表成员](../../../../xdm/classes/b2b/business-marketing-list-members.md) | 无 | 已启用 | `marketingListMemberKey.sourceKey` 在基类中 | B2B营销列表成员 | 无 | 无 | **第一关系**<ul><li>`PersonKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B人员</li><li>命名空间：B2B人员</li><li>目标属性： `b2b.personKey.sourceKey`</li><li>当前架构中的关系名称：人员</li><li>引用架构中的关系名称：营销列表</li></ul>**第二关系**<ul><li>`marketingListKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B营销列表</li><li>命名空间：B2B营销列表</li><li>目标属性： `marketingListKey.sourceKey`</li><li>当前架构中的关系名称：营销列表</li><li>引用架构中的关系名称：人员</li></ul> | 静态列表成员未从同步 [!DNL Salesforce] 因此，没有辅助身份。 |
| B2B活动 | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>访问网页</li><li>新潜在客户</li><li>转化潜在客户</li><li>添加到列表</li><li>从列表中删除</li><li>Add To Opportunity</li><li>从机会中删除</li><li>已填写的表单</li><li>链接点击量</li><li>电子邮件发送</li><li>已打开电子邮件</li><li>已点击电子邮件</li><li>电子邮件退回</li><li>Email Robjected Soft</li><li>取消订阅的电子邮件</li><li>分数已更改</li><li>Opportunity Updated</li><li>促销活动进度中的状态已更改</li><li>人员标识符</li><li>Marketo Web URL</li><li>有趣的时刻</li><li>调用Webhook</li><li>更改促销活动频度</li><li>收入阶段已更改</li><li>合并潜在客户</li><li>已发送电子邮件</li><li>更改促销活动流</li><li>添加到Campaign</li></ul> | 已启用 | `personKey.sourceKey` 人员标识符字段组 | B2B人员 | 无 | 无 | **第一关系**<ul><li>`listOperations.listKey.sourceKey` 字段</li><li>类型：一对一</li><li>引用架构：B2B营销列表</li><li>命名空间：B2B营销列表</li></ul>**第二关系**<ul><li>`opportunityEvent.opportunityKey.sourceKey` 字段</li><li>类型：一对一</li><li>引用架构：B2B机会</li><li>命名空间：B2B机会</li></ul>**第三种关系**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` 字段</li><li>类型：一对一</li><li>引用架构：B2B营销活动</li><li>命名空间：B2B营销活动</li></ul> | `ExperienceEvent` 与实体不同。 体验事件的标识是执行活动的人员。 |
| B2B帐户人员关系 | [XDM业务帐户人员关系](../../../../xdm/classes/b2b/business-account-person-relation.md) | 标识映射 | 已启用 | `accountPersonKey.sourceKey` 在基类中 | B2B帐户人员关系 | 无 | 无 | **第一关系**<ul><li>`personKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B人员</li><li>命名空间：B2B人员</li><li>目标属性： `b2b.personKey.SourceKey`</li><li>当前架构中的关系名称：人员</li><li>引用架构中的关系名称：帐户</li></ul>**第二关系**<ul><li>`accountKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B帐户</li><li>命名空间：B2B帐户</li><li>目标属性： `accountKey.sourceKey`</li><li>当前架构中的关系名称：帐户</li><li>引用架构中的关系名称：人员</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 后续步骤

了解如何连接 [!DNL Marketo] 数据到平台，请参阅 [在UI中创建Marketo源连接器](../../../tutorials/ui/create/adobe-applications/marketo.md).
