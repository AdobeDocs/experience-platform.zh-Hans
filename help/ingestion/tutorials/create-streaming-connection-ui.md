---
keywords: Experience Platform；主页；热门主题；流连接；创建流连接；ui指南；教程；创建流连接；流摄取；
solution: Experience Platform
title: 使用UI创建流连接
topic: tutorial
type: Tutorial
description: 此UI指南将帮助您使用Adobe Experience Platform创建流连接。
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# 使用UI创建流连接

此UI指南将帮助您使用Adobe Experience Platform创建流连接。

## 入门指南

要将流数据开始到[!DNL Experience Platform]，必须先创建流HTTP连接。 创建流连接时，您需要提供关键详细信息，如流数据源，以及您是否打算从受信任（已验证）或不受信任的（未验证）源发送数据。

注册流连接后，您将有一个唯一的URL，它可用于将数据流化到[!DNL Platform]。

请注意，要完成本指南，您需要访问Adobe Experience Platform。 如果您无权访问[!DNL Platform]，请在继续操作前与系统管理员联系。

## 创建流连接

登录[!DNL Experience Platform] UI后，单击&#x200B;**[!UICONTROL 源]**&#x200B;以打开&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡。 此页将可用的源类型显示为单个卡，每个卡都包含一个气泡，该气泡显示从与数据集的流连接创建的数据流数。

![](../images/streaming-ingestion/ui/click-sources.png)

在&#x200B;**[!UICONTROL 源]**&#x200B;页面上，单击&#x200B;**[!UICONTROL HTTP API]**，然后单击&#x200B;**[!UICONTROL 连接源]**。

![](../images/streaming-ingestion/ui/click-connect-source.png)

出现&#x200B;**[!UICONTROL 连接到HTTP]**&#x200B;屏幕。 在&#x200B;**[!UICONTROL 服务详细信息]**&#x200B;下，为新流连接提供名称和说明。

在&#x200B;**[!UICONTROL 帐户身份验证]**&#x200B;下，为流连接选择以下配置属性：

- **[!UICONTROL 身份验证]:** 流连接是否需要身份验证。身份验证确保从可信源收集数据。 建议在处理个人身份信息(PII)时启用此选项。
- **[!UICONTROL XDM模式兼容]:** 此流连接是否将发送与XDM模式兼容的事件。默认情况下，此属性在&#x200B;**处于开启状态。**

选择完配置属性后，单击&#x200B;**[!UICONTROL Connect]**。 您的流式HTTP连接现已创建，现在可以在&#x200B;**[!UICONTROL Sources]**&#x200B;工作区的&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡下查看。

![](../images/streaming-ingestion/ui/http-sources-details.png)

从&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中，可以单击新创建的流式HTTP连接并视图该连接的详细信息。

![](../images/streaming-ingestion/ui/browse-sources.png)

通过单击连接名称的超链接，您可以通过单击&#x200B;**[!UICONTROL 选择数据]**&#x200B;来配置要连接的数据集，从而选择要显示的数据。

![](../images/streaming-ingestion/ui/select-data.png)

您可以[创建新数据集](#create-a-new-dataset)或[使用现有数据集](#use-an-existing-dataset)。

### 创建新数据集

要创建新数据集，请提供数据集的名称、描述以及目标模式。

![](../images/streaming-ingestion/ui/create-new-dataset.png)

插入所有详细信息并单击&#x200B;**[!UICONTROL Next]**&#x200B;后，您可以查看提供的详细信息，然后单击&#x200B;**[!UICONTROL Finish]**&#x200B;将数据集连接到流式HTTP连接。

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### 使用现有数据集

要使用现有数据集，请选择&#x200B;**[!UICONTROL 输出数据集名称]**。

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

单击&#x200B;**[!UICONTROL Next]**&#x200B;后，可查看详细信息，然后单击&#x200B;**[!UICONTROL Finish]**&#x200B;将所选数据集连接到流式HTTP连接。

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## 后续步骤

通过本教程，您已创建了流式HTTP连接，使您可以使用流式端点访问各种[!DNL Data Ingestion] API。 有关在API中创建流连接的说明，请阅读创建流连接教程](../tutorials/create-streaming-connection.md)。[
