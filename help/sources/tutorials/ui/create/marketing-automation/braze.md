---
title: 在UI中为Braze数据创建数据流
description: 了解如何使用Adobe Experience Platform UI为您的Braze帐户创建数据流。
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta 版
exl-id: 6e94414a-176c-4810-80ff-02cf9e797756
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 2%

---

# 在用户界面中创建[!DNL Braze Currents]源连接

>[!NOTE]
>
>[!DNL Braze Currents]源为测试版。 有关使用测试版标记源的更多信息，请阅读[源概述](../../../../home.md#terms-and-conditions)。

[!DNL Braze]支持消费者和品牌之间以客户为中心的实时互动。 [!DNL Braze Currents]是来自Braze平台的参与事件的实时数据流，它是[!DNL Braze]平台中最可靠但最精细的导出。

阅读以下教程，了解如何在UI中将[!DNL Braze]帐户中的参与事件数据引入Adobe Experience Platform。

## 先决条件

要完成本指南中的步骤，您将需要：

* 登录到[Adobe Experience Platform](https://platform.adobe.com)并拥有创建新的流源连接的权限。
* 登录您的[[!DNL Braze] 仪表板](https://dashboard.braze.com/sign_in)、未使用的[Currences Connector许可证](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)以及创建连接器的权限。 有关详细信息，请阅读设置 [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements)的[要求。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

本教程还需要对[[!DNL Braze] 电流](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)有实际了解。

如果您已经有[!DNL Braze]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/marketing-automation.md)的教程。

## 将你的[!DNL Braze]帐户连接到Experience Platform

在Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;*营销自动化*&#x200B;类别下，选择&#x200B;**[!UICONTROL 铜流电流]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![Experience PlatformUI上选定了钎焊电流源的源目录。](../../../../images/tutorials/create/braze/catalog.png)

接下来，上载提供的[铜线电流示例文件](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json)。 此文件包含Braze可能作为事件的一部分发送的所有可能字段。

![“添加数据”屏幕。](../../../../images/tutorials/create/braze/select-data.png)

上传文件后，必须提供数据流详细信息，包括有关数据集和要映射到的架构的信息。
![突出显示“数据集详细信息”的“数据流详细信息”屏幕。](../../../../images/tutorials/create/braze/dataflow-detail.png)

然后，使用映射界面配置数据的映射。

![“映射”屏幕。](../../../../images/tutorials/create/braze/mapping.png)

>[!IMPORTANT]
>
>钎焊时间戳不是以毫秒为单位表示，而是以秒为单位表示。 为了准确反映Experience Platform中的时间戳，您需要创建以毫秒为单位的计算字段。 “time * 1000”的计算将正确地转换为毫秒，适合映射到Experience Platform内的时间戳字段。
>
>![为时间戳](../../../../images/tutorials/create/braze/create-calculated-field.png)创建计算字段

### 收集所需的凭据

创建连接后，必须收集以下凭据值，随后将在钎焊仪表板中提供这些凭据值，以将数据发送到Experience Platform。 有关详细信息，请阅读有关导航到Currences](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents)的[!DNL Braze] [指南。

| 字段 | 描述 |
| --- | --- |
| 客户端 ID | 与您的Experience Platform源关联的客户端ID。 |
| 客户端密码 | 与您的Experience Platform源关联的客户端密钥。 |
| 租户ID | 与您的Experience Platform源关联的租户ID。 |
| 沙盒名称 | 与您的Experience Platform源关联的沙盒。 |
| 数据流 ID | 与您的Experience Platform源关联的数据流ID。 |
| 流端点 | 与您的Experience Platform源关联的流端点。 **注意**： [!DNL Braze]自动将其转换为批处理流终结点。 |

### 配置[!DNL Braze Currents]将数据流式传输到数据源

在[!DNL Braze Dashboard]中，导航到合作伙伴集成&#x200B;**->**&#x200B;数据导出，然后选择&#x200B;**[!DNL Create New Current]**。 系统将提示您提供连接器的名称、有关连接器的通知的联系信息以及上面列出的凭据。 选择要接收的事件，或者配置任何所需的字段排除/转换，然后选择&#x200B;**[!DNL Launch Current]**。

## 后续步骤

通过学习本教程，您已建立与[!DNL Braze]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将营销自动化系统数据引入 [!DNL Platform]](../../dataflow/marketing-automation.md)。
