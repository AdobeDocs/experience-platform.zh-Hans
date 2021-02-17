---
keywords: Experience Platform；主页；热门主题；流连接；创建流连接；ui指南；教程；创建流连接；流摄取；
solution: Experience Platform
title: 使用UI创建流连接
topic: tutorial
type: Tutorial
description: 此UI指南将帮助您使用Adobe Experience Platform创建流连接。
translation-type: tm+mt
source-git-commit: a4019227abaddd9dbe143899d273580ebf21849e
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---


# 使用UI创建流连接

此UI指南将帮助您使用Adobe Experience Platform创建流连接。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成的基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建基块，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

## 创建流连接

登录到[!DNL Experience Platform] UI后，从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL 目录]**&#x200B;屏幕显示了可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在&#x200B;**[!UICONTROL 流]**&#x200B;类别下，选择&#x200B;**[!UICONTROL HTTP API]**。 如果这是您首次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的HTTP流连接器。

![](../../../../images/tutorials/create/http/catalog.png)

将显示&#x200B;**[!UICONTROL 连接HTTP API帐户]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择&#x200B;**[!UICONTROL 新建帐户]**。 在显示的输入表单上，提供帐户名和可选说明。 您还可以选择提供以下配置属性：

- **[!UICONTROL 身份验证]:** 此属性确定流连接是否需要身份验证。身份验证可确保从可信源收集数据。 如果您正在处理个人身份信息(PII)，应打开此属性。 默认情况下，此属性处于关闭状态。
- **[!UICONTROL XDM模式兼容性]:** 此属性表示此流连接是否将发送与XDM模式兼容的事件。默认情况下，此属性处于打开状态。

完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![](../../../../images/tutorials/create/http/new-account.png)

### 现有帐户

要使用现有凭据进行连接，请选择要使用的HTTP API连接，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![](../../../../images/tutorials/create/http/existing-account.png)

## 选择数据

创建HTTP API连接后，将显示&#x200B;**[!UICONTROL 选择数据]**&#x200B;步骤，提供一个界面以选择要连接的数据集。 您可以选择创建新数据集或连接到现有数据集。

### 创建新数据集

要创建新数据集，请选择&#x200B;**[!UICONTROL 新建数据集]**。 在显示的表单上，提供数据集的名称、可选说明以及目标模式。 如果选择启用用户档案的模式，则可以选择是否应也启用用户档案集。

![](../../../../images/tutorials/create/http/new-dataset.png)

### 使用现有数据集

要使用现有数据集，请选择&#x200B;**[!UICONTROL 现有数据集]**。 在显示的表单上，选择要使用的数据集。 选择数据集后，可以选择是否应启用用户档案集。

![](../../../../images/tutorials/create/http/existing-dataset.png)

## 数据流详细信息

出现&#x200B;**[!UICONTROL 数据流详细信息]**&#x200B;步骤。 在此页上，您可以通过提供名称和可选说明来提供创建的数据流的详细信息。

提供数据流的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

![](../../../../images/tutorials/create/http/dataflow-detail.png)

## 审阅

将显示&#x200B;**[!UICONTROL 查看]**&#x200B;步骤，允许您在创建数据流之前查看其详细信息。 详细信息按以下类别分组：

- **[!UICONTROL 连接]**:显示帐户名称、源平台和源名称。
- **[!UICONTROL 分配数据集和映射字段]**:显示目标数据集和数据集附带的模式。

确认详细信息正确后，选择&#x200B;**[!UICONTROL 完成]**。

![](../../../../images/tutorials/create/http/review.png)

## 获取流端点URL

创建连接后，将显示源详细信息页。 本页显示您新创建的连接的详细信息，包括以前运行的数据流、ID和流端点URL。

![](../../../../images/tutorials/create/http/get-streaming-url.png)

## 后续步骤

通过本教程，您创建了流式HTTP连接，使您能够使用流式端点访问各种[!DNL Data Ingestion] API。 有关在API中创建流连接的说明，请阅读[创建流连接教程](../../../api/create/streaming/http.md)。

要了解如何将数据流化到平台，请阅读关于[流式时间系列数据](../../../../../ingestion/tutorials/streaming-time-series-data.md)的教程或关于[流式记录数据](../../../../../ingestion/tutorials/streaming-record-data.md)的教程。
