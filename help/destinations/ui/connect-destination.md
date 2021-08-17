---
keywords: 连接目标；目标连接；如何连接目标
title: 创建新目标连接
type: Tutorial
description: 本教程列出了连接到Adobe Experience Platform中目标的步骤
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# 创建新目标连接

## 概述 {#overview}

在将受众数据发送到目标之前，您必须设置与目标平台的连接。 本文将向您展示如何使用Adobe Experience Platform用户界面设置新目标。

## 创建新目标连接 {#setup}

### 选择目标 {#select-destination}

1. 转到&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**，然后选择&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡。

   ![目录页面](../assets/ui/connect-destinations/catalog.png)

1. 根据您是否具有与目标的现有连接，您可以在目标卡上看到&#x200B;**[!UICONTROL Configure]**&#x200B;或&#x200B;**[!UICONTROL Activate]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的更多信息，请参阅目标工作区文档的[Catalog](../ui/destinations-workspace.md#catalog)部分。 选择&#x200B;**[!UICONTROL 配置]**&#x200B;或&#x200B;**[!UICONTROL 激活]**，具体取决于您可以使用的按钮。

   ![目录页面](../assets/ui/connect-destinations/set-up.png)

   ![激活区段](../assets/ui/connect-destinations/activate-segments.png)

<!-- 1. If you selected **[!UICONTROL Set up]**, skip this step. If you selected **[!UICONTROL Activate segments]**, you can now see a list of the existing destination connections. Select **[!UICONTROL Configure new destination]**.

   ![Configure new destination](../assets/ui/connect-destinations/configure-new-destination.png) -->

### 帐户步骤 {#account}

选择&#x200B;**[!UICONTROL 新建帐户]**&#x200B;以设置到目标的新连接。 或者，如果您之前已设置到目标的连接，请选择&#x200B;**[!UICONTROL 现有帐户]**&#x200B;并选择现有连接。

您在帐户步骤中输入的凭据因目标和身份验证类型而异。

* 对于云存储目标，您需要提供Experience Platform凭据才能连接到存储位置。

   ![为云存储目标选择帐户类型](../assets/ui/connect-destinations/new-account-cloud-storage.png)

* 对于Facebook和其他几个社交和广告目标，请选择&#x200B;**[!UICONTROL 新建帐户]** ，然后选择&#x200B;**[!UICONTROL 连接到目标]**。 这会将您转到目标登录页面，以便将Experience Platform连接到目标。

   ![为社交目标选择帐户类型](../assets/ui/connect-destinations/new-account.png)

>[!IMPORTANT]
>
>有关此步骤中所需参数的详细信息（例如， [Azure Blob](../catalog/cloud-storage/azure-blob.md#parameters)需要连接字符串），请参阅每个目标目录页面中的&#x200B;**[!UICONTROL 连接参数]**&#x200B;部分。

### 身份验证步骤 {#authentication}

输入目标平台连接详细信息，然后选择&#x200B;**[!UICONTROL 创建目标]**。

1. 选择适用于要导出到目标的数据的营销操作。 营销操作指示将数据导出到目标的意图。 您可以从Adobe定义的营销操作中进行选择，也可以创建自己的营销操作。 有关营销操作的更多信息，请参阅[数据使用策略概述](../../data-governance/policies/overview.md)页面。

   >[!IMPORTANT]
   >
   >下图仅用于插图。 目标连接详细信息因目标而异。 有关目标的连接详细信息，请参阅每个[目标目录](../catalog/overview.md)页面中的&#x200B;**[!UICONTROL 连接参数]**&#x200B;部分（例如，[Google客户匹配](../catalog/advertising/google-customer-match.md#parameters)）。

   ![连接到目标](../assets/ui/connect-destinations/connect-destination.png)

1. 选择&#x200B;**[!UICONTROL 保存并退出]**&#x200B;以保存目标配置，或选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续访问受众数据[激活流程](activation-overview.md)。