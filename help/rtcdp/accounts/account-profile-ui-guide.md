---
keywords: rtcdp配置文件；配置文件rtcdp;rtcdp身份；rtcdp合并策略；实时客户配置文件
title: 帐户配置文件UI指南
description: 通过使用帐户配置文件，Real-time Customer Data Platform B2B Edition使您能够统一来自多个来源的帐户信息。 本指南提供了有关在Adobe Experience Platform用户界面中与帐户配置文件进行交互的详细信息。
source-git-commit: 5301cf870052f537a34913beb0b814212bdaadaa
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 0%

---


# 帐户配置文件UI指南

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition目前为测试版。 文档和功能可能会发生更改。

>[!NOTE]
>
>帐户配置文件仅适用于Real-time Customer Data Platform B2B Edition客户。 要进一步了解Real-time CDP ，包括每种许可证类型可用的特性和功能，请首先阅读[Real-time CDP overview](../overview.md)。

帐户配置文件允许您统一来自多个来源的帐户信息。 此帐户统一视图将来自多个营销渠道的数据以及贵组织当前用于存储客户帐户信息的各种系统的数据汇集在一起。 本文档提供了使用Adobe Experience Platform用户界面(UI)中提供的Real-time CDP、B2B Edition功能与帐户配置文件交互的指南。

## 浏览帐户配置文件

要浏览帐户配置文件，请首先在左侧导航的“帐户”下选择&#x200B;**[!UICONTROL Profiles]**。

![](images/b2b-account-browse.png)

在&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡上，您可以使用连接的企业源中的帐户id或直接输入源详细信息来浏览帐户配置文件。

![](images/b2b-account-browse-by.png)

### 按[!UICONTROL 连接的企业源]浏览

要按连接的企业源浏览帐户配置文件，必须首先使用&#x200B;**[!UICONTROL Source]**&#x200B;字段旁边的选择器按钮选择连接的源。

![](images/b2b-account-browse.png)

此时将打开&#x200B;**[!UICONTROL 选择源]**&#x200B;对话框，您可以在其中根据贵组织已建立的连接选择源。

>[!NOTE]
>
>您的组织可能为同一服务提供商配置了多个源(例如，Marketo)，因此务必要检查连接名称、源系统和源系统实例，以确保按正确的源实例进行搜索。

要了解有关连接企业源的更多信息，请参阅[源概述](../sources/sources-overview.md)。

![](images/b2b-account-select-source.png)

您可以通过选择连接名称旁边的单选按钮来选择源，然后使用&#x200B;**[!UICONTROL Select]**&#x200B;返回到[!UICONTROL Browse]选项卡。

选择源后，您现在必须输入与源相关的&#x200B;**[!UICONTROL 帐户id]**。 例如，选择Salesforce来源将要求您从Salesforce实例中输入帐户ID，以查看与该ID绑定的帐户配置文件。

>[!NOTE]
>
>对于Marketo帐户ID，可以引用两个可能的帐户表，因此您必须使用特定语法以确保查看正确的帐户。
>
>最常见的标准语法是由`.mkto_org`附加的Marketo帐户ID（例如，`1234567.mkto_org`）。 Marketo基于帐户的营销客户可能具有其他值，这些值可使用`.mkto_account`附加的Marketo帐户ID找到。 如果您不确定要使用哪种语法，请咨询您的Marketo管理员。

![](images/b2b-account-browse-id.png)

### 按[!UICONTROL 其他]浏览

Real-time CDP， B2B Edition支持执行直接查找的功能，它允许您为要查看的帐户输入&#x200B;**[!UICONTROL 源名称]**、**[!UICONTROL 源实例]**&#x200B;和&#x200B;**[!UICONTROL 帐户ID]**。 通过直接输入源名称和实例，您可以提供Experience Platform搜索和显示正确的帐户配置文件数据所需的上下文。

在无法直接与数据建立源连接的情况下，执行直接查找的功能非常有用。 例如，如果贵组织已制定数据管理策略，阻止直接连接到CRM，则可以将该数据导出到云存储系统，然后将其引入Experience Platform。

另一个示例可能是，您正在从离开系统并进入平台之间对数据执行转换。 您可以使用直接查找功能为数据提供上下文(例如，指定它是Marketo数据，尽管它来自Amazon S3存储段)，以便系统知道要查找的位置以及如何正确渲染数据。

![](images/b2b-account-browse-adhoc.png)

## 查看帐户配置文件详细信息

使用&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡查找帐户配置文件后，选择&#x200B;**[!UICONTROL 配置文件ID]**&#x200B;会打开帐户配置文件的&#x200B;**[!UICONTROL Detail]**&#x200B;选项卡。 **[!UICONTROL Detail]**&#x200B;选项卡中显示的配置文件信息已从多个配置文件片段合并到一起，以形成单个帐户的单个视图。 这包括基本属性和社交媒体数据等帐户详细信息。

显示的默认字段也可以在组织级别更改，以显示首选帐户配置文件属性。

>[!NOTE]
>
>客户配置文件也提供类似功能，并且已创建分步指南，其中包含有关添加和删除属性、调整面板大小等的说明。 请阅读[配置文件详细信息自定义指南](../../profile/ui/profile-customization.md)以了解更多信息。

![](images/b2b-account-details.png)

您可以通过选择其他可用选项卡来查看与帐户相关的其他详细信息。 这些选项卡包括属性、人员和机会选项卡，这些选项卡显示与整个企业系统中的帐户相关的打开和关闭的机会。 有关每个选项卡的更多信息，请参阅以下部分。

## “属性”选项卡

**[!UICONTROL 属性]**&#x200B;选项卡列出了与帐户相关的所有记录信息。 这包括来自多个来源的属性数据，这些来源已合并在一起以构成帐户的单个视图。

除了能够在列表中查看数据外，您还可以使用搜索栏搜索特定属性或以JSON形式查看记录数据。

![](images/b2b-account-attributes.png)

## “人员”选项卡

**[!UICONTROL People]**&#x200B;选项卡提供了与帐户关联的个人人员列表。 这些人员可能是来自不同企业系统的联系人和潜在客户，这些企业系统由您组织内的不同团队管理，但在Real-time CDP和B2B Edition中，他们以单个列表一起呈现，使您能够更全面地了解您的客户联系人。

>[!NOTE]
>
>[!UICONTROL People]选项卡显示与帐户关联的最多25人的列表。 对于拥有25名以上关联人员的帐户，系统会显示25条记录的随机抽样。

除了向您显示联系人的信息快照外，列出的每个人员还包含一个&#x200B;**[!UICONTROL 配置文件ID]**，这是一个可单击的链接，通过该链接，您可以浏览该个人的实时客户资料。 要了解有关查看与您的帐户相关的单个客户配置文件的更多信息，请访问[在Real-time CDP， B2B Edition中浏览配置文件的指南](../profile/profile-browse.md)。

![](images/b2b-account-people.png)

## “机会”选项卡

**[!UICONTROL Opportunity]**&#x200B;选项卡提供与帐户相关的未结和已结业务机会的信息。 这些机会可能会从多个来源摄取到Experience Platform中，但实时CDP B2B Edition使营销人员能够轻松地在一个位置看到所有这些机会。

>[!NOTE]
>
>[!UICONTROL Opportunity]选项卡显示与帐户关联的最多25个机会的列表。 对于拥有25个以上关联机会的帐户，系统显示25条记录的随机抽样。

每个机会都包括诸如机会名称、其数量、阶段，以及该机会是否是打开、关闭、赢得还是丢失的信息。

![](images/b2b-account-opportunities.png)
