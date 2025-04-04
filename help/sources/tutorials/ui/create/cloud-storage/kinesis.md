---
title: 在UI中创建Amazon Kinesis Source连接
description: 了解如何使用Adobe Experience Platform UI创建Amazon Kinesis源连接。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 2%

---

# 在用户界面中创建[!DNL Amazon Kinesis]源连接

>[!IMPORTANT]
>
>[!DNL Amazon Kinesis]源在源目录中可供已购买Real-Time Customer Data Platform Ultimate的用户使用。

Adobe Experience Platform中的Source连接器提供了按计划摄取外部来源数据的功能。 本教程提供了使用[!DNL Experience Platform]用户界面验证[!DNL Amazon Kinesis]（以下称为[!DNL "Kinesis"]）源连接器的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   - [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   - [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL Kinesis]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/streaming/cloud-storage-streaming.md)的教程。

### 收集所需的凭据

为了验证您的[!DNL Kinesis]源连接器，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | [!DNL Kinesis]帐户的访问密钥ID。 |
| `Secret access key` | [!DNL Kinesis]帐户的访问密钥。 |
| `region` | AWS服务器所在的地区。 |

有关这些值的详细信息，请参阅[此 [!DNL Kinesis] 文档](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)。

## 连接您的[!DNL Kinesis]帐户

收集所需的凭据后，您可以按照以下步骤将您的[!DNL Kinesis]帐户关联到[!DNL Experience Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;**[!UICONTROL Cloud Storage]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Amazon Kinesis]**。 如果这是您第一次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，请选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的[!DNL Kinesis]连接器。

![](../../../../images/tutorials/create/kinesis/catalog.png)

出现&#x200B;**[!UICONTROL 连接到Amazon Kinesis]**&#x200B;对话框。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入表单上，提供名称、可选描述和您的[!DNL Kinesis]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后留出一些时间来建立新连接。

![](../../../../images/tutorials/create/kinesis/new.png)

### 现有账户

若要连接现有帐户，请选择您要连接的[!DNL Kinesis]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![](../../../../images/tutorials/create/kinesis/existing.png)

## 后续步骤

按照本教程，您已将[!DNL Kinesis]帐户连接到[!DNL Experience Platform]。 您现在可以继续下一教程，并[配置数据流以将云存储中的数据引入 [!DNL Experience Platform]](../../dataflow/streaming/cloud-storage-streaming.md)。
