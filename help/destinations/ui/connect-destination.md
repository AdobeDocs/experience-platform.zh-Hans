---
keywords: 连接目标；目标连接；如何连接目标
title: 创建新目标连接
type: Tutorial
description: 了解如何在Adobe Experience Platform中连接到目标、启用警报，以及为连接的目标设置营销操作。
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 434b9ed4f64320b5fd73b752716cb34a8e48aec9
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---

# 创建新目标连接

>[!IMPORTANT]
> 
>* 要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。
>* 要连接到支持数据集导出的目标，您需要 **[!UICONTROL 管理和激活数据集目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。


## 概述 {#overview}

在将受众数据发送到目标之前，您必须设置与目标平台的连接。 本文将向您展示如何设置新的目标连接，随后您可以使用Adobe Experience Platform用户界面激活该连接或导出数据集。

## 在目录中查找所需的目标 {#setup}

1. 转到 **[!UICONTROL 连接]** > **[!UICONTROL 目标]**，然后选择 **[!UICONTROL 目录]** 选项卡。

   ![Experience PlatformUI的屏幕截图，其中显示了目标目录页面。](../assets/ui/connect-destinations/catalog.png)

2. 目录中的目标卡片可能具有不同的操作控件，具体取决于您是否拥有与目标的现有连接，以及目标是否支持激活区段、导出数据集，还是两者都支持。 您可能会看到目标卡片的以下任意控件：

   * **[!UICONTROL 设置]**. 在激活区段或导出数据集之前，需要先设置到此目标的连接。
   * **[!UICONTROL 激活]**. 已设置到此目标的连接。 此目标支持区段激活和数据集导出。
   * **[!UICONTROL 激活区段]**. 已设置到此目标的连接。 此目标仅支持区段激活。

   有关这些控件之间差异的更多信息，您还可以参阅 [目录](../ui/destinations-workspace.md#catalog) 目标工作区文档的部分。

   选择 **[!UICONTROL 设置]**, **[!UICONTROL 激活]**&#x200B;或 **[!UICONTROL 激活区段]**，具体取决于您可以使用的控件。

   ![Experience PlatformUI的屏幕截图，其中显示了目标目录页面，并突出显示了设置控件。](../assets/ui/connect-destinations/set-up.png)

   ![Experience PlatformUI的屏幕截图，其中显示了目标目录页面，并突出显示了激活区段控件。](../assets/ui/connect-destinations/activate-segments.png)

3. 如果已选择 **[!UICONTROL 设置]**，跳到下一步，到 [身份验证](#authenticate) 到目的地。

   如果已选择 **[!UICONTROL 激活]**, **[!UICONTROL 激活区段]**&#x200B;或 **[!UICONTROL 导出数据集]**，您现在可以看到现有目标连接的列表。

   选择 **[!UICONTROL 配置新目标]** 建立与目标的新连接。

   ![Experience PlatformUI的屏幕截图，其中显示了可用目标列表，并突出显示了配置新目标控件。](../assets/ui/connect-destinations/configure-new-destination.png)

## 对目标进行身份验证 {#authenticate}

连接到目标的第一步是验证到目标平台。

根据您连接到的目标，您可能会转到目标合作伙伴的页面进行身份验证，或者可能会要求您直接在平台工作流中输入身份验证凭据。 以下是验证到的所需输入示例 [!DNL Amazon S3] 目标。 每个目标文档页面中提供了有关所需输入的详细说明(例如，请参阅 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) 对于 [[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate))。

**[!DNL Amazon S3]必需和可选的身份验证参数**

![该图像显示了在对Amazon S3目标进行身份验证时所需的和可选的输入参数。](../assets/ui/connect-destinations/authenticate-amazon-s3-example.png)

## 设置连接参数 {#set-up-connection-parameters}

如果您已经设置目标的身份验证，则可以继续使用现有帐户，也可以设置新帐户。

根据您连接的目标，可能会要求您输入不同类型的连接参数。 例如，在连接到 [!DNL Amazon S3] 目标，您需要提供有关 [!DNL Amazon S3] 存储段名称和文件存放位置的文件夹路径。 以下是 [!DNL Amazon S3] 目标和 [!DNL Trade Desk] 目标。 每个目标文档页面中提供了有关所需输入的详细说明。

>[!IMPORTANT]
>
>下面的图像仅用于插图。 目标连接详细信息因目标而异。 有关目标的连接详细信息，请阅读 **连接到目标** 每个 [目标目录](../catalog/overview.md) 页面(例如， [[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect), [[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect)或 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details))。

**[!DNL Amazon S3]必需和可选的输入参数**

![该图像显示了连接到Amazon S3目标时所需的和可选的输入参数。](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

**[!DNL The Trade Desk]必需和可选的输入参数**

![该图像显示了在连接到交易台目标时所需的和可选的输入参数。](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### 为导出的文件设置文件格式选项 {#file-formatting-and-compression-options}

对于基于文件的目标，您可以配置与导出文件的格式和压缩方式相关的各种设置。 有关所有可用格式和压缩选项的更多信息，请阅读 [为基于文件的目标配置文件格式选项教程](/help/destinations/ui/batch-destinations-file-formatting-options.md).

![显示CSV文件文件类型选择和各种选项的图像。](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### 为区段激活或数据集导出设置目标连接 {#segment-activation-or-dataset-exports}

某些基于文件的目标支持区段激活以及数据集导出。 对于这些目标，您可以选择是创建连接以激活区段还是导出数据集。

![显示数据类型选择控件的图像，该控件允许用户在区段激活和数据集导出之间进行选择。](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### 启用目标警报 {#enable-alerts}

1. （可选）选择要订阅的目标数据流警报。 创建数据流时，您可以订阅警报，以接收有关流运行状态、成功或失败的警报消息。 可用的警报因您连接的目标类型（基于文件或流）而异。 读取 [订阅上下文关联目标警报](alerts.md) 有关目标数据流警报的详细信息。

   ![配置新目标对话框中突出显示了上下文目标警报订阅选项。](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. 选择&#x200B;**[!UICONTROL 下一步]**。

   ![选中“配置新目标”对话框，且“下一步”控件处于高亮状态，允许用户继续执行工作流中的下一步。](../assets/ui/connect-destinations/next.png)

## 选择营销操作 {#select-marketing-actions}

1. 选择适用于要导出到目标的数据的营销操作。 营销操作指示将数据导出到目标的意图。 您可以从Adobe定义的营销操作中进行选择，也可以创建自己的营销操作。 有关营销操作的更多信息，请参阅 [数据使用策略概述](../../data-governance/policies/overview.md) 页面。

   ![配置新目标对话框中突出显示了可用的营销操作。 用于完成连接到目标工作流的可用控件也会突出显示。](../assets/ui/connect-destinations/governance.png)

2. 选择 **[!UICONTROL 保存并退出]** 要保存目标配置，或选择 **[!UICONTROL 下一个]** 继续访问受众数据 [激活流程](activation-overview.md).

## 后续步骤 {#next-steps}

通过阅读本文档，您了解了如何使用Experience PlatformUI建立与目标的连接。 请注意，可用的连接参数和必需的连接参数因目标而异。 您还应查阅 [目标目录](/help/destinations/catalog/overview.md) 有关每个目标类型所需输入和可用选项的特定信息。

接下来，您可以继续 [激活区段](/help/destinations/ui/activation-overview.md) 或 [导出数据集](/help/destinations/ui/export-datasets.md) 到目的地。