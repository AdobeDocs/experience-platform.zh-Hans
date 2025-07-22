---
title: 创建新的目标连接
type: Tutorial
description: 了解如何在Adobe Experience Platform中连接到目标、启用警报以及为连接的目标设置营销操作。
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 59ff77ff9f4a6fe147b5d8231fd3caa2550ae20e
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 0%

---

# 创建新的目标连接

>[!IMPORTANT]
> 
>* 若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要连接到支持数据集导出的目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理和激活数据集目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

## 概述 {#overview}

在将受众数据发送到目标之前，必须设置与目标平台的连接。 本文介绍如何设置新的目标连接，然后可以使用Adobe Experience Platform用户界面激活受众或导出数据集。

## 在目录中找到所需的目标 {#setup}

1. 转到&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**，然后选择&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡。

   ![Experience Platform UI屏幕截图，显示目标目录页面。](../assets/ui/connect-destinations/catalog.png)

2. 目录中的目标卡片可能具有不同的操作控件，具体取决于您是否具有到目标的现有连接，以及目标是否支持激活受众、导出数据集，或同时支持两者。 您可能会看到目标信息卡的以下任意控件：

   * **[!UICONTROL 设置]**。 在激活受众或导出数据集之前，需要先设置与此目标的连接。
   * **[!UICONTROL 激活]**。 已为此目标设置了连接。 此目标支持受众激活和数据集导出。
   * **[!UICONTROL 激活受众]**。 已为此目标设置了连接。 此目标仅支持受众激活。

   有关这些控件之间差异的更多信息，您还可以参阅目标工作区文档的[目录](../ui/destinations-workspace.md#catalog)部分。

   根据您可用的控件，选择&#x200B;**[!UICONTROL 设置]**、**[!UICONTROL 激活]**&#x200B;或&#x200B;**[!UICONTROL 激活受众]**。

   ![Experience Platform UI屏幕截图，其中显示了突出显示“设置”控件的目标目录页面。](../assets/ui/connect-destinations/set-up.png)

   ![Experience Platform UI屏幕截图，显示突出显示了“激活受众”控件的目标目录页面。](../assets/ui/connect-destinations/activate-segments.png)

3. 如果您选择了&#x200B;**[!UICONTROL 设置]**，请跳到下一步，以对目标[进行身份验证](#authenticate)。

   如果您选择了&#x200B;**[!UICONTROL 激活]**、**[!UICONTROL 激活受众]**&#x200B;或&#x200B;**[!UICONTROL 导出数据集]**，您现在可以看到现有目标连接的列表。

   选择&#x200B;**[!UICONTROL 配置新目标]**&#x200B;以建立与该目标的新连接。

   ![Experience Platform UI屏幕截图，显示可用目标的列表，并突出显示了“配置新目标”控件。](../assets/ui/connect-destinations/configure-new-destination.png)

## 验证目标 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_account_name"
>title="帐户名称"
>abstract="输入一个名称，以帮助您将来轻松识别此目标帐户。 如果您有多个到同一目标类型的连接，这会特别有用。"

连接到目标的第一步是向目标平台进行身份验证。

根据您连接到的目标，系统可能会将您带到目标合作伙伴的页面进行身份验证，或者可能会要求您直接在Experience Platform工作流中输入身份验证凭据。 以下是验证[!DNL Amazon S3]目标所需的输入示例。 每个目标文档页面中都提供了有关所需输入的详细说明（例如，请参阅[[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate)和[[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate)的身份验证部分）。

**[!DNL Amazon S3]必需的和可选的身份验证参数**

![在对目标Amazon S3进行身份验证时显示必需输入参数和可选输入参数的图像。](../assets/ui/connect-destinations/authenticate-amazon-s3-example.png)

## 设置连接参数 {#set-up-connection-parameters}

如果您已经设置了目标身份验证，则可以使用现有帐户继续操作，也可以设置新帐户。

根据您连接到的目标，可能会要求您输入不同类型的连接参数。 例如，在连接到[!DNL Amazon S3]目标时，将要求您提供有关[!DNL Amazon S3]存储段名称和将存储文件的文件夹路径的详细信息。 以下是[!DNL Amazon S3]目标和[!DNL Trade Desk]目标所需输入的两个示例。 有关所需输入的详细说明，请参见每个目标文档页面。

>[!IMPORTANT]
>
>以下图像仅用于说明目的。 目标连接详细信息因目标而异。 有关目标的连接详细信息，请阅读每个&#x200B;**目标目录**&#x200B;页面中的[连接到目标](../catalog/overview.md)部分（例如，[[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect)、[[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect)或[[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)）。

**[!DNL Amazon S3]必需和可选输入参数**

![该图像显示了连接到Amazon S3目标时必需的和可选的输入参数。](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

**[!DNL The Trade Desk]必需和可选输入参数**

![显示连接到交易台目标时必需和可选输入参数的图像。](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### 为导出的文件设置文件格式选项 {#file-formatting-and-compression-options}

对于基于文件的目标，您可以配置与导出文件的格式化和压缩方式相关的各种设置。 有关所有可用格式设置和压缩选项的更多信息，请阅读[基于文件的目标的配置文件格式设置选项教程](/help/destinations/ui/batch-destinations-file-formatting-options.md)。

![显示CSV文件的文件类型选择和各选项图像。](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### 设置目标连接，用于受众激活、帐户激活、潜在客户激活或数据集导出 {#segment-activation-or-dataset-exports}

某些基于文件的目标支持向已知客户、帐户客户或潜在客户激活受众，并支持数据集导出。 对于这些目标，您可以选择是否创建连接，以便能够[激活受众](/help/destinations/ui/activate-batch-profile-destinations.md)、[帐户](/help/destinations/ui/activate-account-audiences.md)、[潜在客户](/help/destinations/ui/activate-prospect-audiences.md)或[导出数据集](/help/destinations/ui/export-datasets.md)。

>[!WARNING]
>
>在导出数据集时，请注意，仅在压缩模式下支持导出到JSON文件。 在压缩和未压缩模式下支持导出到[!DNL Parquet]文件。

![显示数据类型选择控件的图像，该控件允许用户在受众激活和数据集导出之间进行选择。](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### 启用目标警报 {#enable-alerts}

1. （可选）选择要订阅的目标数据流警报。 在创建数据流以接收有关流运行的状态、成功或失败的警报消息时，您可以订阅警报。 可用的警报因您连接到的目标类型（基于文件的或流式传输）而异。 有关目标数据流警报的详细信息，请阅读[订阅上下文中的目标警报](alerts.md)。

   ![突出显示了“配置新目标”对话框的内容中目标警报订阅选项。](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. 选择&#x200B;**[!UICONTROL 下一步]**。

   ![突出显示了“配置新目标”对话框，其中显示了“下一步”控件，允许用户继续工作流中的下一步。](../assets/ui/connect-destinations/next.png)

## 选择营销操作 {#select-marketing-actions}

1. 选择适用于要导出到目标的数据的营销操作。 营销操作指示将数据导出到目标的意图。 您可以从Adobe定义的营销操作中进行选择，也可以创建自己的营销操作。 有关营销操作的更多信息，请参阅[数据使用策略概述](../../data-governance/policies/overview.md)页面。

   ![突出显示可用营销操作的“配置新目标”对话框。 用于完成“连接到目标”工作流的可用控件也突出显示。](../assets/ui/connect-destinations/governance.png)

2. 选择&#x200B;**[!UICONTROL 保存并退出]**&#x200B;以保存目标配置，或选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续执行受众数据[激活流程](activation-overview.md)。

## 后续步骤 {#next-steps}

通过阅读本文档，您已了解如何使用Experience Platform UI建立与目标的连接。 提醒一下，可用和所需的连接参数因目标而异。 您还应该查阅[目标目录](/help/destinations/catalog/overview.md)中的目标文档页面，了解有关每个目标类型的所需输入和可用选项的特定信息。

接下来，您可以继续[激活受众](/help/destinations/ui/activation-overview.md)或[将数据集](/help/destinations/ui/export-datasets.md)导出到您的目标。