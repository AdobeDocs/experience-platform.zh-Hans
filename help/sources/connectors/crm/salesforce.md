---
keywords: Experience Platform；主页；热门主题；CRM架构；CRM;Salesforce;Salesforce
solution: Experience Platform
title: Salesforce源连接器概述
topic-legacy: overview
description: 了解如何使用API或用户界面将Salesforce连接到Adobe Experience Platform。
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: fa861e9740e05b4fcc4e8039bb288301d42b8357
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 0%

---

# [!DNL Salesforce] 连接器

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

Experience Platform支持从第三方CRM系统摄取数据。 对CRM提供商的支持包括 [!DNL Salesforce].

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 无法将特定于区域的IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面以了解更多信息。

## 字段映射来源 [!DNL Salesforce] 到XDM

在 [!DNL Salesforce] 平台， [!DNL Salesforce] 在将源数据字段摄取到Platform之前，必须将其映射到相应的目标XDM字段。

请参阅以下内容，以详细了解 [!DNL Salesforce] 数据集和平台：

- [联系人](../adobe-applications/mapping/salesforce.md#contact)
- [潜在客户](../adobe-applications/mapping/salesforce.md#lead)
- [帐户](../adobe-applications/mapping/salesforce.md#account)
- [机会](../adobe-applications/mapping/salesforce.md#opportunity)
- [机会联系角色](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [营销活动](../adobe-applications/mapping/salesforce.md#campaign)
- [营销活动成员](../adobe-applications/mapping/salesforce.md#campaign-member)

## 设置 [!DNL Salesforce] 命名空间和模式自动生成实用程序

使用 [!DNL Salesforce] 作为 [!DNL B2B-CDP]，则必须先设置 [!DNL Postman] 用于自动生成 [!DNL Salesforce] 命名空间和模式。 以下文档提供了有关设置 [!DNL Postman] 实用程序：

- 您可以从此处下载命名空间和模式自动生成实用程序集合和环境 [GitHub存储库](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- 有关使用Platform API的信息，包括有关如何收集所需标头值和读取示例API调用的详细信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).
- 有关如何为Platform API生成凭据的信息，请参阅 [验证和访问Experience PlatformAPI](../../../landing/api-authentication.md).
- 有关如何设置 [!DNL Postman] 对于Platform API，请参阅 [设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md).

使用平台开发人员控制台和 [!DNL Postman] 设置后，您现在可以开始将相应的环境值应用到 [!DNL Postman] 环境。

下表包含示例值以及有关填充您的 [!DNL Postman] 环境：

| Variable | 描述 | 示例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用于生成 `{ACCESS_TOKEN}`. 请参阅 [验证和访问Experience PlatformAPI](../../../landing/api-authentication.md) 有关如何检索 `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web令牌(JWT)是用于生成{ACCESS_TOKEN}的身份验证凭据。 请参阅 [验证和访问Experience PlatformAPI](../../../landing/api-authentication.md) 以了解有关如何生成 `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | 用于验证对Experience PlatformAPI的调用的唯一标识符。 请参阅 [验证和访问Experience PlatformAPI](../../../landing/api-authentication.md) 有关如何检索 `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成对Experience PlatformAPI的调用所需的授权令牌。 请参阅 [验证和访问Experience PlatformAPI](../../../landing/api-authentication.md) 有关如何检索 `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 关于 [!DNL Marketo]，此值已修复，并且始终设置为： `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | 的 `global` 容器包含所有标准Adobe和Experience Platform合作伙伴提供的类、架构字段组、数据类型和架构。 关于 [!DNL Marketo]，此值是固定的，且始终设置为 `global`. | `global` |
| `PRIVATE_KEY` | 用于验证您的 [!DNL Postman] 实例Experience PlatformAPI。 请参阅有关设置开发人员控制台的教程和 [设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md) 有关如何检索{PRIVATE_KEY}的说明。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用于集成以Adobe I/O的凭据。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management系统(IMS)为Adobe服务提供了身份验证框架。 关于 [!DNL Marketo]，此值已修复，且始终设置为： `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 拥有或许可产品和服务并允许其成员访问的公司实体。 请参阅 [设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md) 有关如何检索 `{IMS_ORG}` 信息。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您使用的虚拟沙盒分区的名称。 | `prod` |
| `TENANT_ID` | 用于确保您创建的资源命名正确且包含在IMS组织中的ID。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 您对进行API调用的URL端点。 此值是固定的，始终设置为： `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | 您的 [!DNL Marketo] 帐户。 请参阅 [验证 [!DNL Marketo] 实例](../adobe-applications/marketo/marketo-auth.md) 有关如何检索 `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | 您的组织ID [!DNL Salesforce] 帐户。 请参阅以下内容 [[!DNL Salesforce] 指南](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) 有关获取 [!DNL Salesforce] 组织ID。 | `00D4W000000FgYJUA0` |
| `has_abm` | 一个布尔值，指示您是否订阅了 [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | 一个布尔值，指示您是否被划分为 [!DNL Marketo Sales Insight]. | `false` |

{style=&quot;table-layout:auto&quot;}

### 运行脚本

使用 [!DNL Postman] 收集和环境设置之后，您现在可以通过 [!DNL Postman] 界面。

在 [!DNL Postman] 界面中，选择自动生成器实用程序的根文件夹，然后选择 **[!DNL Run]** 中。

![根文件夹](../../images/tutorials/create/salesforce/root-folder.png)

的 [!DNL Runner] 界面。 从此处，确保选中所有复选框，然后选择 **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![运行发生器](../../images/tutorials/create/salesforce/run-generator.png)

成功的请求根据测试版规范创建B2B命名空间和架构。

## 连接 [!DNL Salesforce] 到使用API的平台

以下文档提供了有关如何连接的信息 [!DNL Salesforce] 要使用API或用户界面实现平台，请执行以下操作：

- [使用流服务API创建Salesforce基连接](../../tutorials/api/create/crm/salesforce.md)
- [使用流量服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为CRM源创建数据流](../../tutorials/api/collect/crm.md)

## 连接 [!DNL Salesforce] 到使用UI的平台

- [在UI中创建Salesforce源连接](../../tutorials/ui/create/crm/salesforce.md)
- [在UI中为CRM连接创建数据流](../../tutorials/ui/dataflow/crm.md)
