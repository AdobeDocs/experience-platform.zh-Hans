---
keywords: Experience Platform；主页；热门主题；Adobe Campaign Managed Cloud Services；营销活动；营销活动托管服务
title: Adobe Campaign Managed Cloud Services
description: 了解如何使用用户界面将Campaign ManagedCloud Services连接到平台
exl-id: 8f18bf73-ebf1-4b4e-a12b-964faa0e24cc
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---

# Adobe Campaign Managed Cloud Services

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

Adobe Campaign Managed Cloud Services提供了用于设计跨渠道客户体验的Managed Services平台，并提供了可视活动编排、实时交互管理和跨渠道执行的环境。 访问 [Adobe Campaign v8文档](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=en) 以了解更多信息。

利用Adobe Campaign Managed Cloud Services源，可将Adobe Campaign v8投放日志和跟踪日志数据引入Adobe Experience Platform。

## 先决条件

在创建源连接以将Campaign v8Experience Platform之前，您必须先完成以下先决条件：

* [使用Adobe Campaign客户端控制台设置事件日志导入](#view-delivery-and-tracking-log-data)
* [创建XDM ExperienceEvent架构](#create-a-schema)
* [创建数据集](#create-a-dataset)

### 查看投放和跟踪日志数据 {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>您必须有权访问Adobe Campaign v8客户端控制台，才能在Campaign中查看日志数据。 访问 [Campaign v8文档](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html?lang=en) 有关如何下载和安装客户端控制台的信息。

通过客户端控制台登录到您的Campaign v8实例。 在 [!DNL Explorer] 选项卡，选择 [!DNL Administration] 然后选择 [!DNL Configuration]. 接下来，选择 [!DNL Data schemas] 然后应用 `broadLog` 筛选名称或标签。 在显示的列表中，选择名为的收件人投放日志源架构 `broadLogRcp`.

![在选择了Explorer选项卡的Adobe Campaign v8客户端控制台中，管理、配置和数据架构节点扩展并筛选集为“广泛”。](./images/campaign/explorer.png)

接下来，选择 **数据** 选项卡。

![选择了数据选项卡的Adobe Campaign v8客户端控制台。](./images/campaign/data.png)

在数据面板中右键单击/按键以打开上下文菜单。 从此处选择 **配置列表……**

![打开上下文菜单并选择配置列表选项的Adobe Campaign v8客户端控制台。](./images/campaign/configure.png)

此时将出现列表配置窗口，为您提供一个界面，您可以在其中向预先存在的列表添加任何所需的字段，以在数据面板中查看数据。

![可添加以供查看的收件人投放日志配置列表。](./images/campaign/list-configuration.png)

现在，您可以查看收件人的投放日志，包括上一步中添加的配置字段。

>[!TIP]
>
>您可以重复相同的步骤，但需要筛选 `tracking` 查看跟踪日志数据。

![收件人投放日志显示有关其上次修改名称、投放渠道、内部投放名称和标签的信息。](./images/campaign/recipient-delivery-logs.png)

### 创建架构 {#create-a-schema}

接下来，为投放日志和跟踪日志创建XDM ExperienceEvent架构。 您必须将“促销活动投放日志”字段组应用于您的投放日志架构，并将“促销活动跟踪日志”字段组应用于您的跟踪日志架构。 您还必须定义 `externalID` 字段作为架构的主标识。

>[!NOTE]
>
>您的XDM ExperienceEvent架构必须启用用户档案，才能将您的Campaign数据摄取到 [!DNL Real-Time Customer Profile].

有关如何创建模式的详细说明，请阅读 [在UI中创建XDM架构](../../../xdm/tutorials/create-schema-ui.md).

### 创建数据集 {#create-a-dataset}

最后，您必须为架构创建一个数据集。 有关如何创建数据集的详细说明，请阅读 [在UI中创建数据集](../../../catalog/datasets/user-guide.md).

## 使用Platform UI创建Adobe Campaign Managed Cloud Services源连接

现在，您已在Campaign客户端控制台中访问数据日志、创建架构和数据集，接下来可以继续创建源连接以将Campaign Managed Services数据导入平台。

有关如何将Campaign v8投放日志和跟踪日志数据引入Experience Platform的详细说明，请阅读 [在UI中创建Campaign Managed Services源连接](../../tutorials/ui/create/adobe-applications/campaign.md).
