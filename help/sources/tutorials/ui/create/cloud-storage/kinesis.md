---
title: 在UI中创建Amazon Kinesis源连接
description: 了解如何使用Amazon UI创建Adobe Experience Platform Kinesis源连接。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# 创建 [!DNL Amazon Kinesis] UI中的源连接

>[!IMPORTANT]
>
>此 [!DNL Amazon Kinesis] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

Adobe Experience Platform中的源连接器提供了按计划摄取外部来源数据的功能。 本教程提供了对进行身份验证的步骤 [!DNL Amazon Kinesis] (以下简称： [!DNL "Kinesis"])源连接器使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   - [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   - [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL Kinesis] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/streaming/cloud-storage-streaming.md).

### 收集所需的凭据

为了验证您的 [!DNL Kinesis] 源连接器中，必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | 您的访问密钥ID [!DNL Kinesis] 帐户。 |
| `Secret access key` | 您的访问密钥 [!DNL Kinesis] 帐户。 |
| `region` | AWS服务器所在的地区。 |

有关这些值的更多信息，请参阅 [此 [!DNL Kinesis] 文档](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## 连接您的 [!DNL Kinesis] 帐户

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL Kinesis] 帐户至 [!DNL Platform].

登录 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航栏访问 **[!UICONTROL 源]** 工作区。 此 **[!UICONTROL 目录]** 屏幕显示了多种来源，您可以使用这些来源创建帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 **[!UICONTROL 云存储]** 类别，选择 **[!UICONTROL Amazon Kinesis]**. 如果这是您第一次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，选择 **[!UICONTROL 添加数据]** 以新建 [!DNL Kinesis] 连接器。

![](../../../../images/tutorials/create/kinesis/catalog.png)

此 **[!UICONTROL 连接到Amazon Kinesis]** 出现对话框。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您正在使用新凭据，请选择 **[!UICONTROL 新建帐户]**. 在出现的输入表单上，提供名称、可选描述以及 [!DNL Kinesis] 凭据。 完成后，选择 **[!UICONTROL 连接]** 然后等待一段时间以建立新连接。

![](../../../../images/tutorials/create/kinesis/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL Kinesis] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/kinesis/existing.png)

## 后续步骤

按照本教程，您已连接到 [!DNL Kinesis] 帐户至 [!DNL Platform]. 您现在可以继续下一教程和 [配置数据流以将云存储中的数据引入 [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
