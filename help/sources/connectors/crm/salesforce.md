---
keywords: Experience Platform；主页；热门主题；CRM架构；CRM；CRM；Salesforce；Salesforce
solution: Experience Platform
title: Salesforce源连接器概述
description: 了解如何使用API或用户界面将Salesforce连接到Adobe Experience Platform。
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# [!DNL Salesforce] 连接器

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从第三方CRM系统中摄取数据。 CRM提供商的支持包括 [!DNL Salesforce].

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于地区的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面，以了解更多信息。

## 字段映射自 [!DNL Salesforce] 到XDM

建立源连接： [!DNL Salesforce] 和平台 [!DNL Salesforce] 在将源数据字段引入到Platform中之前，必须将其映射到相应的目标XDM字段。

有关以下字段之间的映射规则的详细信息，请参阅以下内容 [!DNL Salesforce] 数据集和平台：

- [联系人](../adobe-applications/mapping/salesforce.md#contact)
- [潜在客户](../adobe-applications/mapping/salesforce.md#lead)
- [帐户](../adobe-applications/mapping/salesforce.md#account)
- [机会](../adobe-applications/mapping/salesforce.md#opportunity)
- [机会联系人角色](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [营销活动](../adobe-applications/mapping/salesforce.md#campaign)
- [营销活动成员](../adobe-applications/mapping/salesforce.md#campaign-member)
- [帐户联系人关系](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## 设置 [!DNL Salesforce] 命名空间和模式自动生成实用程序

要使用 [!DNL Salesforce] 源作为的一部分 [!DNL B2B-CDP]，您必须首先设置 [!DNL Postman] 自动生成 [!DNL Salesforce] 命名空间和架构。 以下文档提供了有关设置的其他信息 [!DNL Postman] 实用工具：

- 您可以从此处下载命名空间和架构自动生成实用程序集合和环境 [GitHub存储库](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- 有关使用Platform API的信息，包括有关如何收集所需标头的值和读取示例API调用的详细信息，请参阅以下指南中的 [Platform API快速入门](../../../landing/api-guide.md).
- 有关如何为Platform API生成凭据的信息，请参阅关于的教程 [身份验证和访问Experience PlatformAPI](../../../landing/api-authentication.md).
- 有关如何设置的信息 [!DNL Postman] 有关平台API的信息，请参阅关于的教程 [设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md).

通过Platform开发人员控制台和 [!DNL Postman] 设置，您现在可以开始将适当的环境值应用于 [!DNL Postman] 环境。

下表包含示例值以及有关填充 [!DNL Postman] 环境：

| Variable | 描述 | 示例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用于生成 `{ACCESS_TOKEN}`. 请参阅上的教程 [身份验证和访问Experience PlatformAPI](../../../landing/api-authentication.md) 以获取有关如何检索 `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web令牌(JWT)是用于生成{ACCESS_TOKEN}的身份验证凭据。 请参阅上的教程 [身份验证和访问Experience PlatformAPI](../../../landing/api-authentication.md) 了解有关如何生成 `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | 用于验证Experience PlatformAPI调用的唯一标识符。 请参阅上的教程 [身份验证和访问Experience PlatformAPI](../../../landing/api-authentication.md) 以获取有关如何检索 `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成Experience PlatformAPI调用所需的授权令牌。 请参阅上的教程 [身份验证和访问Experience PlatformAPI](../../../landing/api-authentication.md) 以获取有关如何检索 `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 关于 [!DNL Marketo]，此值是固定的，并且始终设置为： `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | 此 `global` container包含所有标准Adobe和Experience Platform合作伙伴提供的类、架构字段组、数据类型和架构。 关于 [!DNL Marketo]，此值是固定的，并且始终设置为 `global`. | `global` |
| `PRIVATE_KEY` | 用于验证您的帐户的凭据 [!DNL Postman] Experience PlatformAPI的实例。 请参阅有关设置开发人员控制台的教程，并且 [设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md) 以获取有关如何检索{PRIVATE_KEY}的说明。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用于集成到Adobe I/O的凭据。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS)提供了对Adobe服务进行身份验证的框架。 关于 [!DNL Marketo]，此值是固定的，并且始终设置为： `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 企业实体，可以拥有或许可产品和服务，并允许其成员访问。 请参阅上的教程 [设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md) 以获取有关如何检索 `{ORG_ID}` 信息。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您正在使用的虚拟沙盒分区的名称。 | `prod` |
| `TENANT_ID` | 一个ID，用于确保您创建的资源被正确命名并包含在您的组织内。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 您对其进行API调用的URL端点。 此值是固定的，并且始终设置为： `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | 您的唯一ID [!DNL Marketo] 帐户。 请参阅上的教程 [验证您的 [!DNL Marketo] 实例](../adobe-applications/marketo/marketo-auth.md) 以获取有关如何检索 `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | 您的组织ID [!DNL Salesforce] 帐户。 请参阅以下内容 [[!DNL Salesforce] 指南](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) ，以了解有关获取您的 [!DNL Salesforce] 组织ID。 | `00D4W000000FgYJUA0` |
| `has_abm` | 指示您是否订阅的布尔值 [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | 指示您是否订阅的布尔值 [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

### 运行脚本

通过您的 [!DNL Postman] 收集和环境设置完成后，您现在可以通过 [!DNL Postman] 界面。

在 [!DNL Postman] 界面，选择自动生成器实用程序的根文件夹，然后选择 **[!DNL Run]** 从顶部标题中。

![root-folder](../../images/tutorials/create/salesforce/root-folder.png)

此 [!DNL Runner] 界面。 从此处确保选中了所有复选框，然后选择 **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![游程生成器](../../images/tutorials/create/salesforce/run-generator.png)

成功的请求将根据测试版规范创建B2B命名空间和架构。

## Connect [!DNL Salesforce] 到使用API的平台

以下文档提供了有关如何连接的信息 [!DNL Salesforce] 至使用API或用户界面的Platform：

- [使用流服务API创建Salesforce基本连接](../../tutorials/api/create/crm/salesforce.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为CRM源创建数据流](../../tutorials/api/collect/crm.md)

## Connect [!DNL Salesforce] 使用UI到Platform

- [在UI中创建Salesforce源连接](../../tutorials/ui/create/crm/salesforce.md)
- [在UI中为CRM连接创建数据流](../../tutorials/ui/dataflow/crm.md)
