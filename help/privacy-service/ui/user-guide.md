---
keywords: Experience Platform；主页；热门主题；导出；导出
solution: Experience Platform
title: 在Privacy Service UI中管理隐私作业
topic-legacy: UI guide
description: 了解如何使用Privacy Service用户界面来协调和监控不同Experience Cloud应用程序的隐私请求。
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 0%

---

# 在Privacy Service UI中管理隐私作业

本文档提供了使用[!DNL Privacy Service]用户界面创建和管理隐私请求的步骤。

## 浏览[!DNL Privacy Service] UI仪表板

[!DNL Privacy Service] UI的仪表板提供了两个构件，允许您视图隐私作业的状态：&quot;[!UICONTROL Status Report]&quot;和&quot;[!UICONTROL Job Requests]&quot;。 仪表板还显示所显示作业的当前选定规则。

![UI仪表板](../images/user-guide/dashboard.png)

### 调节类型

[!DNL Privacy Service] 支持针对几个隐私法规的工作请求：

*  [!DNL California Consumer Privacy Act] ([!UICONTROL CCPA])
* 欧洲合并[!DNL General Data Protection Regulation]([!UICONTROL GDPR])
* 泰国的[!DNL Personal Data Protection Act]([!UICONTROL PDPA_THA])
* 巴西的[!DNL Lei Geral de Proteção de Dados]([!UICONTROL LGPD_BRA])
* 新西兰[!DNL Privacy Act]([!UICONTROL NZPA_NZL])

将单独跟踪每种调整类型的任务。 要在调节类型之间切换，请选择&#x200B;**[!UICONTROL Regulation Type]**&#x200B;下拉菜单，然后从列表中选择所需的调节。

![调整类型下拉列表](../images/user-guide/regulation.png)

当更改规则类型时，仪表板将更新以显示适用于所选规则的所有操作、过滤器、构件和作业创建对话框。

![更新的仪表板](../images/user-guide/dashboard-update.png)

### 状态报告

状态报告构件左侧的图表会跟踪针对可能报告有错误的任何作业提交的作业。 右侧的图表跟踪接近30天规范窗口末尾的作业。

选择图形上方的两个切换按钮之一以显示或隐藏各自的量度。

![](../images/user-guide/hide-errors.png)

通过将鼠标悬停在有关数据点上，可以视图与图形上任何数据点关联的作业的确切数量。

![鼠标悬停数据点](../images/user-guide/mouse-over.png)

要视图有关给定数据点的更多详细信息，请选择相关数据点以在“作业请求”构件中显示关联的作业。 请注意在作业列表上方应用的筛选器。

![从Widget应用的过滤器](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>将过滤器应用到作业请求构件后，可以通过选择过滤器丸上的&#x200B;**X**&#x200B;来删除过滤器。 然后，作业请求返回默认跟踪列表。

### 作业请求

作业请求构件会列表您组织中所有可用的作业请求，包括请求类型、当前状态、到期日期和申请人电子邮件等详细信息。

>[!NOTE]
>
>之前创建的作业的数据仅在完成日期后30天内可访问。

您可以在“作业请求”标题下方的搜索栏中键入关键字，以筛选列表。 列表会在您键入时自动过滤器，显示包含与搜索词匹配的值的请求。 您还可以使用&#x200B;**[!UICONTROL Requested on]**&#x200B;下拉菜单为列出的作业选择时间范围。

![作业请求搜索选项](../images/user-guide/job-search.png)

要视图特定作业请求的详细信息，请从列表中选择该请求的作业ID以打开&#x200B;**[!UICONTROL Job Details]**&#x200B;页。

![GDPR UI作业详细信息](../images/user-guide/job-details.png)

此对话框包含有关每个[!DNL Experience Cloud]解决方案的状态信息，以及它相对于整个作业的当前状态。 由于每个隐私作业都是异步的，因此该页面会显示每个解决方案的最新通信日期和时间(GMT)，因为有些解决方案在处理请求时所需的时间比其他解决方案要多。

如果解决方案提供了任何其他数据，则可在此对话框中查看。 您可以通过选择单个产品行来视图此数据。

要以CSV文件形式下载完整的作业数据，请选择对话框右上角的&#x200B;**[!UICONTROL Export to CSV]**。

## 创建新的隐私作业请求

>[!NOTE]
>
>要创建隐私作业请求，您必须为要访问或删除其数据的特定客户提供身份信息。 请查看有关隐私请求](../identity-data.md)的[标识数据的文档，然后继续本节。

[!DNL Privacy Service] UI提供了两种创建新作业请求的方法：

* [使用Request Builder](#request-builder)
* [上传JSON文件](#json)

以下各节提供了使用这些方法的步骤。

### 使用Request Builder {#request-builder}

使用Request Builder，您可以在用户界面中手动创建新的隐私作业请求。 请求生成器最适用于更简单、更小的请求集，因为请求生成器限制每个用户的请求只具有ID类型。 对于更复杂的请求，最好[上载JSON文件](#json)。

要使用Request Builder进行开始，请在屏幕右侧的状态报表构件下方选择&#x200B;**[!UICONTROL Create Request]**。

![选择创建请求](../images/user-guide/create-request.png)

将打开&#x200B;**[!UICONTROL Create Request]**&#x200B;对话框，其中显示用于提交当前所选法规类型的隐私作业请求的可用选项。

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

从列表中选择请求的&#x200B;**[!UICONTROL Job Type]**（“删除”或“访问”）以及一个或多个可用产品。

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

在&#x200B;**[!UICONTROL Namespace type]**&#x200B;下，为发送到[!DNL Privacy Service]的客户ID选择适当的命名空间类型。

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

使用标准命名空间类型时，从下拉菜单（电子邮件、ECID或AAID）中选择一个命名空间，然后在右侧文本框中键入ID值，按&#x200B;**\&lt;enter>**&#x200B;将每个ID添加到列表。

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

使用自定义命名空间类型时，必须在提供以下ID值之前手动键入命名空间。

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

完成后，选择&#x200B;**[!UICONTROL Create]**。

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

该对话框将消失，新作业（或作业）将列在作业请求构件中及其当前处理状态。

### 上传JSON文件{#json}

在创建更复杂的请求（例如对处理的每个数据主体使用多个ID类型的请求）时，可以通过上传JSON文件来创建请求。

选择屏幕右侧状态报表Widget下方的&#x200B;**[!UICONTROL Create Request]**&#x200B;旁边的箭头。 从显示的选项列表中，选择&#x200B;**[!UICONTROL Upload JSON]**。

![请求创建选项](../images/user-guide/create-options.png)

将显示&#x200B;**[!UICONTROL Upload JSON]**&#x200B;对话框，其中提供了一个窗口，供您将JSON文件拖放到其中。

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

如果您没有要上传的JSON文件，请选择&#x200B;**[!UICONTROL Download Adobe-GDPR-Request.json]**&#x200B;以下载模板，您可以根据从数据主体收集的值填充该模板。


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


在您的计算机上找到JSON文件，并将其拖入对话框窗口。 如果上载成功，则该文件名将显示在对话框中。 您可以根据需要继续添加更多JSON文件，方法是将这些文件拖放到对话框中。

完成后，选择&#x200B;**[!UICONTROL Create]**。 该对话框将消失，新作业（或作业）将列在作业请求构件中及其当前处理状态。

### 后续步骤

通过阅读此文档，您学习了如何使用[!DNL Privacy Service] UI创建隐私作业、视图作业的详细信息并监控其处理状态，以及在完成后下载结果。

有关如何使用[!DNL Privacy Service] API以编程方式执行这些操作的步骤，请参阅[开发人员指南](../api/getting-started.md)。
