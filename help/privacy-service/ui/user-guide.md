---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service用户指南
topic: UI guide
translation-type: tm+mt
source-git-commit: c8446f6040ac9ef1f4196d9057b531011e243258
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---


# [!DNL Privacy Service] 用户指南

此文档提供了使用用户界面创建和管理隐私请求 [!DNL Privacy Service] 的步骤。

## 浏览UI [!DNL Privacy Service] 仪表板

UI仪表板提 [!DNL Privacy Service] 供了两个构件，允许您视图隐私作业的状态： **[!UICONTROL 状态报告]** 和 **[!UICONTROL 作业请求]**。 仪表板还显示所显示作业的当前选定规则。

![UI仪表板](../images/user-guide/dashboard.png)

### 调整类型

[!DNL Privacy Service] 支持三种法规类型的工作请求：

* 欧洲合并 [!DNL General Data Protection Regulation] (GDPR)
* ( [!DNL California Consumer Privacy Act] CCPA)
* 泰国( [!DNL Personal Data Protection Act] PDPA_THA)

将单独跟踪每种法规类型的任务。 要在调整类型之间切换，请单 **[!UICONTROL 击“调整类型]** ”下拉菜单，并从列表中选择所需的调整。

![调整类型下拉列表](../images/user-guide/regulation.png)

当更改规则类型时，仪表板会更新以显示适用于所选规则的所有操作、过滤器、构件和工作创建对话框。

![更新的仪表板](../images/user-guide/dashboard-update.png)

### 状态报告

状态报告构件左侧的图形会跟踪已提交的作业与可能报告有错误的任何作业。 右侧的图形跟踪接近30天规范窗口末尾的作业。

单击图形上方的两个切换按钮之一以显示或隐藏各自的度量。

![](../images/user-guide/hide-errors.png)

通过将鼠标悬停在相关数据点上，可以视图与图形上任何数据点关联的确切作业数。

![鼠标悬停数据点](../images/user-guide/mouse-over.png)

要视图有关给定数据点的更多详细信息，请单击相关数据点以在“作业请求”构件中显示相关的作业。 记下在作业列表上方应用的筛选器。

![从构件中应用滤镜](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>将过滤器应用到“作业请求”构件后，可以通过单击筛选药片上的 **[!UICONTROL X]** 来删除过滤器。 然后，作业请求返回默认跟踪列表。

### 作业请求

作业请求构件列表您组织中所有可用的作业请求，包括请求类型、当前状态、到期日期和申请人电子邮件等详细信息。

>[!NOTE]
>
>之前创建的作业的数据仅在完成日期后30天内可访问。

您可以在“工作请求”标题下方的搜索栏中键入关键字来筛选列表。 列表会在您键入时自动过滤器，显示包含与搜索词匹配的值的请求。 您还可以使用“ **[!UICONTROL 请求时间]** ”下拉菜单来选择列出的作业的时间范围。

![作业请求搜索选项](../images/user-guide/job-search.png)

要视图特定作业请求的详细信息，请从列表中单击该请求的作业ID以打开“作业详 *[!UICONTROL 细信息]* ”页。

![GDPR UI作业详细信息](../images/user-guide/job-details.png)

此对话框包含有关每个解决方 [!DNL Experience Cloud] 案的状态信息，以及与整个作业相关的当前状态。 由于每个隐私作业都是异步的，因此该页面会显示每个解决方案的最新通信日期和时间(GMT)，因为有些解决方案需要的时间比其他解决方案多。

如果解决方案提供了任何其他数据，则可在此对话框中查看。 您可以通过单击各个产品行来视图此数据。

要以CSV文件形式下载完整的作业数据， **[!UICONTROL 请单击对话框右]** 上方的“导出到CSV”。

## 创建新的隐私作业请求

>[!NOTE]
>
>要创建隐私作业请求，您必须为要访问或删除其数据的特定客户提供身份信息。 请在继续本节之前 [查看隐私请求的身份](../identity-data.md) 文档。

UI [!DNL Privacy Service] 提供了两种创建新作业请求的方法：

* [使用Request Builder](#request-builder)
* [上传JSON文件](#json)

以下各节提供了使用这些方法的步骤。

### 使用Request Builder {#request-builder}

使用Request Builder，您可以在用户界面中手动创建新的隐私作业请求。 Request Builder最适合用于更简单、更小的请求集，因为Request Builder限制每个用户的请求只具有ID类型。 对于更复杂的请求，最好 [上传JSON文件](#json) 。

要使用Request Builder进行开始，请 **[!UICONTROL 单击屏幕右侧]** “状态报告”构件下的“创建请求”。

![单击“创建请求”](../images/user-guide/create-request.png)

此时 *[!UICONTROL 会打开]* “创建请求”对话框，显示提交当前选定法规类型的隐私作业请求的可用选项。

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

选择 **[!UICONTROL 请求的]** “作业类型”（“删除”或“访问”），并从列表中选择一个或多个可 **[!UICONTROL 用产]** 品。

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

在 *[!UICONTROL 命名空间类]*&#x200B;型下，为要发送到的客户ID选择适当的命名空间类型 [!DNL Privacy Service]。

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

使用标 _准命名空间_ 类型时，从下拉菜单（电子邮件、ECID或AAID）中选择命名空间，然后在右侧的文本框中键入ID值，为每个ID按 **\&lt;enter>** ，将其添加到列表。

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

使用自定 _义命名空间_ 类型时，您必须在提供以下ID值之前手动键入命名空间。

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

When finished, click **[!UICONTROL Create]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

该对话框将消失，新作业（或作业）将列在作业请求构件中及其当前处理状态。

### 上传JSON文件 {#json}

在创建更复杂的请求（如对每个正在处理的数据主体使用多个ID类型的请求）时，可以通过上传JSON文件来创建请求。

单击屏幕右侧 **[!UICONTROL 的状态报]**&#x200B;告构件下方的“创建请求”旁边的箭头。 从显示的选项列表中，选择“ **[!UICONTROL 上传JSON]**”。

![请求创建选项](../images/user-guide/create-options.png)

此 *[!UICONTROL 时将显示]* “上传JSON”对话框，其中提供了一个窗口，供您将JSON文件拖放到其中。

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

如果您没有要上传的JSON文件，请单 **[!UICONTROL 击“下载Adobe-GDPR-Request.json]** ”以下载模板，您可以根据从数据主体收集的值填充该模板。


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


在您的计算机上找到JSON文件，并将其拖入对话框窗口。 如果上载成功，则对话框中将显示文件名。 您可以根据需要将JSON文件拖放到对话框中，以继续添加更多文件。

When finished, click **[!UICONTROL Create]**. 该对话框将消失，新作业（或作业）将列在作业请 _求构件中_ ，并列出其当前处理状态。

### 后续步骤

通过阅读此文档，您学习了如何使用 [!DNL Privacy Service] UI创建隐私作业、视图作业的详细信息并监视其处理状态，以及在完成后下载结果。

有关如何使用API以编程方式执行这些操作 [!DNL Privacy Service] 的步骤，请参阅开发 [人员指南](../api/getting-started.md)。