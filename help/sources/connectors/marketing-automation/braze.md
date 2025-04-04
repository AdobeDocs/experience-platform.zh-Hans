---
title: 钎焊电流Source概述
description: 了解如何将数据从钎焊电流流式传输到Experience Platform。
badge: Beta 版
exl-id: dd304e10-26e5-4586-ab39-8fe3294b19c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 4%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>[!DNL Braze Currents]源为测试版。 有关使用测试版标记源的更多信息，请阅读[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从流应用程序中摄取数据。 对流式提供程序的支持包括[!DNL Braze Currents]。

[!DNL Braze]支持消费者和品牌之间以客户为中心的实时互动。 [!DNL Braze Currents]是来自Braze平台的参与事件的实时数据流，它是[!DNL Braze]平台中最可靠但最精细的导出。

## 先决条件

要完成本指南中的步骤，您将需要：

* 登录到[Adobe Experience Platform](https://platform.adobe.com)并拥有创建新的流源连接的权限。
* 登录您的[[!DNL Braze] 仪表板](https://dashboard.braze.com/sign_in)、未使用的[Currences Connector许可证](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)以及创建连接器的权限。 有关详细信息，请阅读设置 [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements)的[要求。

### 收集所需的凭据

要成功地将您的[!DNL Braze Currents]数据提交到Experience Platform，您需要在[!DNL Braze] UI仪表板中输入以下Experience Platform凭据。

| 字段 | 描述 |
| --- | --- |
| 客户端 ID | 与您的Experience Platform源关联的客户端ID。 |
| 客户端密码 | 与您的Experience Platform源关联的客户端密钥。 |
| 租户 ID | 与您的Experience Platform源关联的租户ID。 |
| 沙盒名称 | 与您的Experience Platform源关联的沙盒。 |
| 数据流 ID | 与您的Experience Platform源关联的数据流ID。 |
| 流端点 | 与您的Experience Platform源关联的流端点。 **注意**： [!DNL Braze]自动将其转换为批处理流终结点。 |

有关如何检索这些值的信息，请阅读[Experience Platform API快速入门](../../../landing/api-authentication.md)指南。 有关使用[!DNL Braze]仪表板的信息，请阅读有关如何[导航到“电流”](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents)的[!DNL Braze]指南。

## 后续步骤

通过阅读本文档，您已完成从[!DNL Braze Currents]帐户向Experience Platform流式传输数据所需的先决条件设置。 现在，您可以使用用户界面](../../tutorials/ui/create/marketing-automation/braze.md)在[连接 [!DNL Braze Currents] 到Experience Platform时继续阅读指南。
