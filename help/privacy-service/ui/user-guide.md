---
keywords: Experience Platform；主页；主题；导出；导出
solution: Experience Platform
title: 在Privacy ServiceUI中管理隐私作业
description: 了解如何使用Privacy Service用户界面协调和监控各种Experience Cloud应用程序中的隐私请求。
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: e539b1e165227d9a888bfe12d8205e285b3ce259
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---

# 在Privacy ServiceUI中管理隐私作业 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="描述"
>abstract=""

本文档提供了使用创建和管理隐私请求的步骤。 [!DNL Privacy Service] 用户界面。

## 浏览 [!DNL Privacy Service] UI仪表板

的仪表板 [!DNL Privacy Service] UI提供了两个允许您查看隐私作业状态的构件：“[!UICONTROL 状态报告]“ ”和“ ”[!UICONTROL 作业请求]“。 该仪表板还会显示所显示任务的当前选定法规。

![UI仪表板](../images/user-guide/dashboard.png)

### 法规类型

[!DNL Privacy Service] 支持多个隐私法规的作业请求。 下表列出了支持的法规及其在UI中表示的相应标签：

| UI标签 | 法规 |
| --- | --- |
| [!UICONTROL CCPA] | [!DNL California Consumer Privacy Act] |
| [!UICONTROL GDPR] | 欧盟的 [!DNL General Data Protection Regulation] |
| [!UICONTROL PDPA_THA] | 泰国的 [!DNL Personal Data Protection Act] |
| [!UICONTROL LGPD_BRA] | 巴西的 [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL NZPA_NZL] | 新西兰 [!DNL Privacy Act] |
| [!UICONTROL VCDPA_USA] | [!DNL Virginia Consumer Data Protection Act] |
| [!UICONTROL CPRA_USA] | [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL APA_AUS] | [!DNL Australia Privacy Act (Privacy Act)] |
| [!UICONTROL HIPAA_AUS] | [!DNL Health Insurance Portability and Accountability Act] |

{style="table-layout:auto"}

>[!NOTE]
>
>请参阅概述，位于 [支持的隐私法规](../regulations/overview.md) ，以了解有关每个法规的法律背景的更多信息。

每种法规类型的作业将单独进行跟踪。 要在法规类型之间切换，请选择 **[!UICONTROL 法规类型]** 下拉菜单，并从列表中选择所需的法规。

![“法规类型”下拉列表](../images/user-guide/regulation.png)

在更改法规类型后，仪表板会更新以显示适用于所选法规的所有操作、筛选器、小部件和作业创建对话框。

![已更新仪表板](../images/user-guide/dashboard-update.png)

### 状态报告

状态报表小组件左侧的图形可跟踪已提交的作业，以及可能已报告回但出现错误的任何作业。 右侧的图表跟踪接近30天合规性窗口结束的作业。

选择图表上方的两个切换按钮之一以显示或隐藏其各自的量度。

![](../images/user-guide/hide-errors.png)

通过将鼠标悬停在相关数据点上，可以查看与图表上任何数据点关联的作业的确切数量。

![将鼠标悬停在数据点上](../images/user-guide/mouse-over.png)

要查看有关给定数据点的更多详细信息，请选择相关数据点以在作业请求构件中显示关联的作业。 记下在作业列表上方应用的过滤器。

![从小组件应用了筛选器](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>将过滤器应用于作业请求构件后，您可以通过选择 **X** 在过滤药丸上。 然后，作业请求返回到默认跟踪列表。

### 作业请求

工作请求构件列出组织中所有可用的工作请求，包括请求类型、当前状态、截止日期和请求者电子邮件等详细信息。

>[!NOTE]
>
>以前创建的作业的数据只能在完成日期后的30天内访问。

您可以通过在“作业请求”标题下方的搜索栏中输入关键字来筛选列表。 列表会在您键入时自动筛选，显示包含与搜索词匹配值的请求。 您还可以使用 **[!UICONTROL 请求日期]** 下拉菜单，为列出的作业选择时间范围。

![作业请求搜索选项](../images/user-guide/job-search.png)

要查看特定作业请求的详细信息，请从列表中选择该请求的作业ID以打开 **[!UICONTROL 作业详细信息]** 页面。

![GDPR UI作业详细信息](../images/user-guide/job-details.png)

此对话框包含有关每个项目的状态信息 [!DNL Experience Cloud] 解决方案及其相对于整个作业的当前状态。 由于每个隐私作业都是异步执行的，因此页面会显示每个解决方案的最新通信日期和时间(GMT)，因为有些解决方案处理请求所需的时间比其他解决方案长。

如果某个解决方案提供了任何其他数据，则可以在该对话框中查看该数据。 您可以通过选择单个产品行来查看此数据。

要将完整的作业数据下载为CSV文件，请选择 **[!UICONTROL 导出到CSV]** 对话框的右上角。

## 创建新的隐私作业请求 {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="说明"
>abstract=""

>[!NOTE]
>
>要创建隐私作业请求，您必须提供其数据将被访问或删除的特定客户的身份信息。 请查看文档： [隐私请求的身份数据](../identity-data.md) 然后再继续本节。

此 [!DNL Privacy Service] UI提供了两种创建新作业请求的方法：

* [使用请求生成器](#request-builder)
* [上传JSON文件](#json)

以下各节提供了使用每种方法的步骤。

### 使用请求生成器 {#request-builder}

使用请求生成器，您可以在用户界面中手动创建新的隐私作业请求。 请求生成器最适合用于更简单、更小的请求集，因为请求生成器限制每个用户的请求只能具有ID类型。 对于更复杂的请求，最好是这样 [上传JSON文件](#json) 而是。

要开始使用请求生成器，请选择 **[!UICONTROL 创建请求]** 位于屏幕右侧的状态报表小部件下方。

![选择创建请求](../images/user-guide/create-request.png)

此 **[!UICONTROL 创建请求]** 这将打开一个对话框，其中显示了用于提交当前所选法规类型的隐私作业请求的可用选项。

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

选择 **[!UICONTROL 作业类型]** 请求（“删除”或“访问”）以及列表中的一个或多个可用产品。

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

下 **[!UICONTROL 命名空间类型]**，为要发送到的客户ID选择适当的命名空间类型 [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

使用标准命名空间类型时，请从下拉菜单（电子邮件、ECID或AAID）中选择命名空间，然后在右侧的文本框中键入ID值，然后按 **\&lt;enter>** ，以将其添加到列表。

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

使用自定义命名空间类型时，您必须手动键入命名空间，然后才能提供下面的ID值。

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

完成后，选择 **[!UICONTROL 创建]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

该对话框消失，新作业（或多个作业）及其当前处理状态将列在作业请求小部件中。

### 上传JSON文件 {#json}

在创建更复杂的请求（例如，为每个处理的数据主体使用多个ID类型的请求）时，您可以通过上传JSON文件来创建请求。

选择旁边的箭头 **[!UICONTROL 创建请求]**，位于屏幕右侧的状态报表小部件的下方。 从显示的选项列表中，选择 **[!UICONTROL 上传JSON]**.

![请求创建选项](../images/user-guide/create-options.png)

此 **[!UICONTROL 上传JSON]** 对话框，为您提供了一个用于将JSON文件拖放到中的窗口。

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

如果您没有要上传的JSON文件，请选择 **[!UICONTROL 下载Adobe-GDPR-Request.json]** 以下载可根据从数据主体收集的值填充的模板。


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


在计算机上找到JSON文件，并将其拖动到对话框窗口中。 如果上传成功，文件名将显示在对话框中。 您可以根据需要继续添加更多JSON文件，方法是将它们拖放到对话框中。

完成后，选择 **[!UICONTROL 创建]**. 该对话框消失，新作业（或多个作业）及其当前处理状态将列在作业请求小部件中。

### 后续步骤

通过阅读本文档，您已了解如何使用 [!DNL Privacy Service] UI，用于创建隐私作业、查看作业的详细信息并监控其处理状态，以及在作业完成后下载结果。

有关如何使用以编程方式执行这些操作的步骤 [!DNL Privacy Service] API，请参阅 [API指南](../api/overview.md).
