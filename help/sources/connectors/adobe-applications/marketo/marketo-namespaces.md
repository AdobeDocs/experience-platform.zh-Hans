---
title: B2B命名空间和架构
description: 本文档概述了创建B2B源连接器时所需的自定义命名空间。
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 4%

---

# B2B命名空间和架构

>[!NOTE]
>
>您可以使用Adobe Experience Platform UI中的模板来加快B2B和B2C数据的资源创建。 有关详细信息，请阅读以下指南： [在Platform UI中使用模板](../../../tutorials/ui/templates.md).

本文档提供了有关为要与B2B源一起使用的命名空间和架构进行的基础设置的信息。 本文档还提供了有关设置生成B2B命名空间和架构所需的Postman自动化实用程序的详细信息。

>[!IMPORTANT]
>
>您必须有权访问 [Adobe Real-time Customer Data Platform B2B版本](../../../../rtcdp/b2b-overview.md) 以便B2B架构参与 [Real-time Customer Profile](../../../../profile/home.md).

## 设置B2B命名空间和模式自动生成实用程序

使用B2B命名空间和模式自动生成实用程序的第一步是设置平台开发人员控制台和 [!DNL Postman] 环境。

- 您可以从此处下载命名空间和架构自动生成实用程序集合和环境 [GitHub存储库](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- 有关使用Platform API的信息，包括有关如何收集所需标头的值和读取示例API调用的详细信息，请参阅以下指南中的 [Platform API快速入门](../../../../landing/api-guide.md).
- 有关如何为Platform API生成凭据的信息，请参阅关于的教程 [身份验证和访问Experience PlatformAPI](../../../../landing/api-authentication.md).
- 有关如何设置的信息 [!DNL Postman] 有关平台API的信息，请参阅关于的教程 [设置开发人员控制台和 [!DNL Postman]](../../../../landing/postman.md).

通过Platform开发人员控制台和 [!DNL Postman] 设置，您现在可以开始将适当的环境值应用于 [!DNL Postman] 环境。

下表包含示例值以及有关填充 [!DNL Postman] 环境：

| Variable | 描述 | 示例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用于生成 `{ACCESS_TOKEN}`. 请参阅上的教程 [身份验证和访问Experience PlatformAPI](../../../../landing/api-authentication.md) 以获取有关如何检索 `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web令牌(JWT)是用于生成{ACCESS_TOKEN}的身份验证凭据。 请参阅上的教程 [身份验证和访问Experience PlatformAPI](../../../../landing/api-authentication.md) 了解有关如何生成 `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | 用于验证Experience PlatformAPI调用的唯一标识符。 请参阅上的教程 [身份验证和访问Experience PlatformAPI](../../../../landing/api-authentication.md) 以获取有关如何检索 `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成Experience PlatformAPI调用所需的授权令牌。 请参阅上的教程 [身份验证和访问Experience PlatformAPI](../../../../landing/api-authentication.md) 以获取有关如何检索 `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 关于 [!DNL Marketo]，此值是固定的，并且始终设置为： `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | 此 `global` container包含所有标准Adobe和Experience Platform合作伙伴提供的类、架构字段组、数据类型和架构。 关于 [!DNL Marketo]，此值是固定的，并且始终设置为 `global`. | `global` |
| `PRIVATE_KEY` | 用于验证您的帐户的凭据 [!DNL Postman] Experience PlatformAPI的实例。 请参阅有关设置开发人员控制台的教程，并且 [设置开发人员控制台和 [!DNL Postman]](../../../../landing/postman.md) 以获取有关如何检索{PRIVATE_KEY}的说明。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用于集成到Adobe I/O的凭据。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS)提供了对Adobe服务进行身份验证的框架。 关于 [!DNL Marketo]，此值是固定的，并且始终设置为： `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 企业实体，可以拥有或许可产品和服务，并允许其成员访问。 请参阅上的教程 [设置开发人员控制台和 [!DNL Postman]](../../../../landing/postman.md) 以获取有关如何检索 `{ORG_ID}` 信息。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您正在使用的虚拟沙盒分区的名称。 | `prod` |
| `TENANT_ID` | 一个ID，用于确保您创建的资源被正确命名并包含在您的组织内。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 您对其进行API调用的URL端点。 此值是固定的，并且始终设置为： `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### 运行脚本

通过您的 [!DNL Postman] 收集和环境设置完成后，您现在可以通过 [!DNL Postman] 界面。

在 [!DNL Postman] 界面，选择自动生成器实用程序的根文件夹，然后选择 **[!DNL Run]** 从顶部标题中。

![root-folder](../images/marketo/root-folder.png)

此 [!DNL Runner] 界面。 从此处确保选中了所有复选框，然后选择 **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![游程生成器](../images/marketo/run-generator.png)

成功的请求将创建B2B所需的命名空间和架构。

## B2B命名空间

身份命名空间是的组件 [[!DNL Identity Service]](../../../../identity-service/home.md) 用于区分身份的上下文或类型。 完全限定的身份包括ID值和命名空间。 请参阅 [命名空间概述](../../../../identity-service/namespaces.md) 了解更多信息。

B2B命名空间用于实体的主标识。

下表包含有关B2B命名空间的基础设置的信息。

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

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

{style="table-layout:auto"}

## B2B架构

Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。通过在整个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。

在将数据摄取到Platform中之前，必须构建一个架构来描述数据的结构，并为每个字段中可以包含的数据类型提供约束。 架构由一个基类以及零个或多个架构字段组组成。

有关架构组合模型的更多信息，包括设计原则和最佳实践，请参阅 [模式组合基础](../../../../xdm/schema/composition.md).

下表包含有关B2B架构的基础设置的信息。

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 架构名称 | 基类 | 字段组 | [!DNL Profile] 在架构中 | 主要标识 | 主要身份命名空间 | 辅助标识 | 辅助身份命名空间 | 关系 | 注释 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B帐户 | [XDM商业帐户](../../../../xdm/classes/b2b/business-account.md) | XDM业务帐户详细信息 | 已启用 | `accountKey.sourceKey` 在基类中 | B2B帐户 | `extSourceSystemAudit.externalKey.sourceKey` 在基类中 | B2B帐户 | <ul><li>`accountParentKey.sourceKey` 在XDM业务帐户详细信息字段组中</li><li>目标属性： `/accountKey/sourceKey`</li><li>类型：一对一</li><li>引用架构：B2B帐户</li><li>命名空间： B2B帐户</li></ul> |
| B2B人员 | [XDM 个人资料](../../../../xdm/classes/individual-profile.md) | <ul><li>XDM业务人员详细信息</li><li>XDM业务人员组件</li><li>Identitymap</li><li>同意和偏好设置详细信息</li></ul> | 已启用 | `b2b.personKey.sourceKey` 在XDM业务人员详细信息字段组中 | B2B人员 | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` XDM业务人员详细信息字段组的</li><li>`workEmail.address` XDM业务人员详细信息字段组的</ol></li> | <ol><li>B2B人员</li><li>电子邮件</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` “XDM业务人员组成部分”字段组的</li><li>类型：多对一</li><li>引用架构：B2B帐户</li><li>命名空间： B2B帐户</li><li>目标属性： accountKey.sourceKey</li><li>来自当前架构的关系名称：帐户</li><li>引用架构中的关系名称：人员</li></ul> |
| B2B机会 | [XDM商业机会](../../../../xdm/classes/b2b/business-opportunity.md) | XDM业务机会详细信息 | 已启用 | `opportunityKey.sourceKey` 在基类中 | B2B机会 | `extSourceSystemAudit.externalKey.sourceKey` 在基类中 | B2B机会 | <ul><li>`accountKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B帐户</li><li>命名空间： B2B帐户</li><li>目标属性： `accountKey.sourceKey`</li><li>来自当前架构的关系名称：帐户</li><li>引用架构中的关系名称：商机</li></ul> |
| B2B机会人员关系 | [XDM业务机会人员关系](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | None | 已启用 | `opportunityPersonKey.sourceKey` 在基类中 | B2B机会人员关系 | `extSourceSystemAudit.externalKey.sourceKey` 在基类中 | B2B机会人员关系 | **第一关系**<ul><li>`personKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B人员</li><li>命名空间： B2B人员</li><li>目标属性： b2b.personKey.sourceKey</li><li>来自当前架构的关系名称：人员</li><li>引用架构中的关系名称：商机</li></ul>**第二关系**<ul><li>`opportunityKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B机会 </li><li>命名空间： B2B机会 </li><li>目标属性： `opportunityKey.sourceKey`</li><li>来自当前架构的关系名称：机会</li><li>引用架构中的关系名称：人员</li></ul> |
| B2B营销活动 | [XDM商业营销活动](../../../../xdm/classes/b2b/business-campaign.md) | XDM商业营销活动详细信息 | 已启用 | `campaignKey.sourceKey` 在基类中 | B2B营销活动 | `extSourceSystemAudit.externalKey.sourceKey` 在基类中 | B2B营销活动 |
| B2B营销活动成员 | [XDM商业营销活动成员](../../../../xdm/classes/b2b/business-campaign-members.md) | XDM商业营销活动成员详细信息 | 已启用 | `ccampaignMemberKey.sourceKey` 在基类中 | B2B营销活动成员 | `extSourceSystemAudit.externalKey.sourceKey` 在基类中 | B2B营销活动成员 | **第一关系**<ul><li>`personKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B人员</li><li>命名空间： B2B人员</li><li>目标属性： `b2b.personKey.sourceKey`</li><li>来自当前架构的关系名称：人员</li><li>引用架构中的关系名称：营销活动</li></ul>**第二关系**<ul><li>`campaignKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B营销活动</li><li>命名空间： B2B营销活动</li><li>目标属性： `campaignKey.sourceKey`</li><li>来自当前架构的关系名称：营销活动</li><li>引用架构中的关系名称：人员</li></ul> |
| B2B营销列表 | [XDM业务营销列表](../../../../xdm/classes/b2b/business-marketing-list.md) | None | 已启用 | `marketingListKey.sourceKey` 在基类中 | B2B营销列表 | None | None | None | 静态列表未从同步 [!DNL Salesforce] 因此没有辅助标识。 |
| B2B营销列表成员 | [XDM商业营销列表成员](../../../../xdm/classes/b2b/business-marketing-list-members.md) | None | 已启用 | `marketingListMemberKey.sourceKey` 在基类中 | B2B营销列表成员 | None | None | **第一关系**<ul><li>`PersonKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B人员</li><li>命名空间： B2B人员</li><li>目标属性： `b2b.personKey.sourceKey`</li><li>来自当前架构的关系名称：人员</li><li>引用架构中的关系名称：营销列表</li></ul>**第二关系**<ul><li>`marketingListKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B营销列表</li><li>命名空间： B2B营销列表</li><li>目标属性： `marketingListKey.sourceKey`</li><li>来自当前架构的关系名称：营销列表</li><li>引用架构中的关系名称：人员</li></ul> | 静态列表成员未从同步 [!DNL Salesforce] 因此没有辅助标识。 |
| B2B活动 | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>访问网页</li><li>新建潜在客户</li><li>转换潜在客户</li><li>添加到列表</li><li>从列表中删除</li><li>添加到机会</li><li>从机会中移除</li><li>表单已填写</li><li>链接点击次数</li><li>电子邮件已送达</li><li>电子邮件已打开</li><li>已单击电子邮件</li><li>电子邮件已退回</li><li>电子邮件软退回</li><li>电子邮件已取消订阅</li><li>分数已更改</li><li>机会已更新</li><li>促销活动进展中的状态已更改</li><li>人员标识符</li><li>Marketo Web URL</li><li>有趣的时刻</li><li>调用Webhook</li><li>更改营销活动节奏</li><li>收入阶段已更改</li><li>合并潜在客户</li><li>已发送电子邮件</li><li>更改营销活动流</li><li>添加到营销活动</li></ul> | 已启用 | `personKey.sourceKey` “人员标识符”字段组 | B2B人员 | None | None | **第一关系**<ul><li>`listOperations.listKey.sourceKey` 字段</li><li>类型：一对一</li><li>引用架构：B2B营销列表</li><li>命名空间： B2B营销列表</li></ul>**第二关系**<ul><li>`opportunityEvent.opportunityKey.sourceKey` 字段</li><li>类型：一对一</li><li>引用架构：B2B机会</li><li>命名空间： B2B机会</li></ul>**第三关系**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` 字段</li><li>类型：一对一</li><li>引用架构：B2B营销活动</li><li>命名空间： B2B营销活动</li></ul> | `ExperienceEvent` 不同于实体。 体验事件的身份是执行活动的人员。 |
| B2B帐户人员关系 | [XDM业务帐户人员关系](../../../../xdm/classes/b2b/business-account-person-relation.md) | 标识映射 | 已启用 | `accountPersonKey.sourceKey` 在基类中 | B2B帐户人员关系 | None | None | **第一关系**<ul><li>`personKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B人员</li><li>命名空间： B2B人员</li><li>目标属性： `b2b.personKey.SourceKey`</li><li>来自当前架构的关系名称：人员</li><li>引用架构中的关系名称：帐户</li></ul>**第二关系**<ul><li>`accountKey.sourceKey` 在基类中</li><li>类型：多对一</li><li>引用架构：B2B帐户</li><li>命名空间： B2B帐户</li><li>目标属性： `accountKey.sourceKey`</li><li>来自当前架构的关系名称：帐户</li><li>引用架构中的关系名称：人员</li></ul> |

{style="table-layout:auto"}

## 后续步骤

要了解如何连接 [!DNL Marketo] 将数据导入Platform，请参阅 [在UI中创建Marketo源连接器](../../../tutorials/ui/create/adobe-applications/marketo.md).
