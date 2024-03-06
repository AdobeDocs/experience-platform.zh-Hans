---
title: 钎焊电流源概述
description: 了解如何将数据从钎焊电流流式传输到Experience Platform。
badge: Beta 版
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 2%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>此 [!DNL Braze Currents] 源为测试版。 请阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记源代码的更多信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从流式应用程序引入数据。 对流式提供商的支持包括 [!DNL Braze Currents].

[!DNL Braze] 支持消费者和品牌之间以客户为中心的实时互动。 [!DNL Braze Currents] 是来自Braze平台的参与事件的实时数据流，是最强大但最精细的导出 [!DNL Braze] 平台。

## 先决条件

要完成本指南中的步骤，您将需要：

* 登录至 [Adobe Experience Platform](https://platform.adobe.com) 和创建新的流源连接的权限。
* 登录您的 [[!DNL Braze] 仪表板](https://dashboard.braze.com/sign_in)，未使用 [电流连接器许可证](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)、和创建连接器的权限。 欲知更多信息，请参阅 [设置要求 [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### 收集所需的凭据

要成功提交 [!DNL Braze Currents] 要Experience PlatformExperience Platform的数据，您需要在 [!DNL Braze] UI仪表板。

| 字段 | 描述 |
| --- | --- |
| 客户端ID | 与您的Experience Platform源关联的客户端ID。 |
| 客户端密码 | 与您的Experience Platform源关联的客户端密钥。 |
| 租户ID | 与您的Experience Platform源关联的租户ID。 |
| 沙盒名称 | 与您的Experience Platform源关联的沙盒。 |
| 数据流ID | 与您的Experience Platform源关联的数据流ID。 |
| 流端点 | 与您的Experience Platform源关联的流端点。 **注意**： [!DNL Braze] 自动将其转换为批处理流端点。 |

有关如何检索这些值的信息，请阅读上的指南 [Platform API快速入门](../../../landing/api-authentication.md). 有关使用 [!DNL Braze] 仪表板，阅读 [!DNL Braze] 操作方法指南 [导航到电流](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## 后续步骤

通过阅读本文档，您已完成流传输数据所需的先决条件设置 [!DNL Braze Currents] 帐户到Experience Platform。 您现在可以继续阅读以下指南： [连接 [!DNL Braze Currents] 使用用户界面Experience Platform](../../tutorials/ui/create/marketing-automation/braze.md).