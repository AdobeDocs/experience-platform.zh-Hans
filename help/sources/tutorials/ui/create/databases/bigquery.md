---
keywords: Experience Platform;home;popular topics;Google Big Query;google big query;GBQ;gbq
solution: Experience Platform
title: 在UI中创建Google大查询源连接器
topic: overview
type: Tutorial
description: 本教程提供了使用平台用户界面创建Google大查询（以下称“GBQ”）源连接器的步骤。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# 在UI [!DNL Google Big Query] 中创建源连接器

>[!NOTE]
>
> 连接 [!DNL Google BigQuery] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用 [!DNL Google Big Query] 户界面创建（下称“GBQ”）源连接器 [!DNL Platform] 的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果已有有效的GBQ连接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

要在上访问您的GBQ帐 [!DNL Platform]户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `project` | 要查询的默认项目 [!DNL BigQuery] 的项目ID。 |
| `clientID` | 用于生成刷新令牌的ID值。 |
| `clientSecret` | 用于生成刷新令牌的机密值。 |
| `refreshToken` | 从中获取的用于 [!DNL Google] 授权访问的刷新令牌 [!DNL BigQuery]。 |

有关这些值的详细信息，请参 [阅此GBQ文档](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)。

## 连接您的GBQ帐户

收集所需凭据后，您可以按照以下步骤将GBQ帐户链接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 **[!UICONTROL 据库]** ”类别下， **[!UICONTROL 选择Google Big查询]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选 **[!UICONTROL 择“添加数据]** ”以创建新的GBQ连接器。

![](../../../../images/tutorials/create/google-big-query/catalog.png)

将显 **[!UICONTROL 示“连接到Google Big查询]** ”页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和GBQ凭据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![](../../../../images/tutorials/create/google-big-query/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的GBQ帐户，然后选择“下 **[!UICONTROL 一步]** ”以继续。

![](../../../../images/tutorials/create/google-big-query/existing.png)

## 后续步骤

按照本教程，您已建立了与GBQ帐户的连接。 您现在可以继续学习下一个教程， [并配置一个数据流以将数据引入 [!DNL Platform]](../../dataflow/databases.md)。