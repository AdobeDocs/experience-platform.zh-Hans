---
title: 在UI中创建Google Big Query Source连接
description: 了解如何使用Google UI创建Adobe Experience Platform Big Query源连接。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 55aaaa39659566de81bb161d704b6f8212e29a8b
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# 在用户界面中创建[!DNL Google BigQuery]源连接

>[!IMPORTANT]
>
>[!DNL Google BigQuery]源在源目录中可供已购买Real-time Customer Data Platform Ultimate的用户使用。

阅读本教程，了解如何使用用户界面将您的[!DNL Google BigQuery]帐户连接到Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL Google BigQuery]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需的凭据

有关收集所需凭据的详细步骤，请阅读[[!DNL Google BigQuery] 身份验证指南](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)。

## 连接您的Google BigQuery帐户

在Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。 您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在[!UICONTROL 数据库]类别下，选择&#x200B;**[!UICONTROL Google BigQuery]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

>[!TIP]
>
>当给定的源尚未具有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL 设置]**&#x200B;选项。 一旦存在经过身份验证的帐户，此选项将更改为&#x200B;**[!UICONTROL 添加数据]**。

![已选择Google BigQuery的源目录。](../../../../images/tutorials/create/google-big-query/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到Google Big Query]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有账户

若要连接现有帐户，请选择您要连接的[!DNL Google BigQuery]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![显示现有帐户列表的现有帐户页面。](../../../../images/tutorials/create/google-big-query/existing.png)

### 新帐户

如果要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后为您的新[!DNL Google BigQuery]帐户提供名称和可选描述。

![源工作流中的新帐户接口。](../../../../images/tutorials/create/google-big-query/new.png)

>[!BEGINTABS]

>[!TAB 使用基本身份验证]

要使用基本身份验证，请选择&#x200B;**[!UICONTROL 基本身份验证]**，并提供[项目、客户端ID、客户端密钥、刷新令牌和（可选）大型结果数据集ID](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)的值。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，等待一段时间以建立连接。

![选择基本身份验证的新帐户接口。](../../../../images/tutorials/create/google-big-query/basic_auth.png)

>[!TAB 使用服务身份验证]

要使用服务身份验证，请选择&#x200B;**[!UICONTROL 服务身份验证]**，并提供[项目ID、密钥文件内容和（可选）大型结果数据集ID](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)的值。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，等待一段时间以建立连接。

![选择服务身份验证的新帐户接口。](../../../../images/tutorials/create/google-big-query/service_auth.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与[!DNL Google BigQuery]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入Platform](../../dataflow/databases.md)。
