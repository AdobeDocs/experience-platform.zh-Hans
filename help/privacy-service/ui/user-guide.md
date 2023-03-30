---
keywords: Experience Platform；主页；热门主题；导出；导出
solution: Experience Platform
title: 在Privacy ServiceUI中管理隐私作业
description: 了解如何使用Privacy Service用户界面跨各种Experience Cloud应用程序协调和监控隐私请求。
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 1%

---

# 在Privacy ServiceUI中管理隐私作业 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="执行数据主体隐私请求"
>abstract="<h2>描述</h2><p>Adobe Experience Platform Privacy Service允许您代表那些希望根据法律隐私法规访问或删除其个人数据的客户创建和管理隐私请求。</p>"

本文档提供了使用创建和管理隐私请求的步骤 [!DNL Privacy Service] 用户界面。

>[!IMPORTANT]
>
>Privacy Service仅适用于数据主体和消费者权限请求。 不支持或允许将Privacy Service用于数据清理或维护的任何其他用途。 Adobe有法律义务及时履行这些义务。 因此，不允许对Privacy Service进行负载测试，因为它是仅生产环境，并且会造成有效隐私请求的不必要积压。
>
>现已设置硬性的每日上载限制，以帮助防止滥用服务。 发现滥用系统的用户将禁用其对服务的访问权限。 随后将与他们举行会议，讨论他们的行动并讨论可接受的Privacy Service用途。

## 浏览 [!DNL Privacy Service] UI功能板

功能板 [!DNL Privacy Service] UI提供了两个小组件，用于查看隐私作业的状态：&quot;[!UICONTROL 状态报表]&quot;和&quot;[!UICONTROL 作业请求]&quot; 仪表板还显示所显示作业的当前选定法规。

![UI功能板](../images/user-guide/dashboard.png)

### 调节类型

[!DNL Privacy Service] 支持多项隐私法规的作业请求。 下表列出了受支持的法规及其相应标签，如UI中所示：

| UI标签 | 监管 |
| --- | --- |
| [!UICONTROL CCPA] | [!DNL California Consumer Privacy Act] |
| [!UICONTROL GDPR] | 欧盟 [!DNL General Data Protection Regulation] |
| [!UICONTROL PDPA_THA] | 泰国 [!DNL Personal Data Protection Act] |
| [!UICONTROL LGPD_BRA] | 巴西 [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL NZPA_NZL] | 新西兰 [!DNL Privacy Act] |
| [!UICONTROL VCDPA_USA] | [!DNL Virginia Consumer Data Protection Act] |
| [!UICONTROL CPRA_USA] | [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL APA_AUS] | [!DNL Australia Privacy Act (Privacy Act)] |
| [!UICONTROL HIPAA_AUS] | [!DNL Health Insurance Portability and Accountability Act] |

{style="table-layout:auto"}

>[!NOTE]
>
>请参阅 [受支持的隐私法规](../regulations/overview.md) 以详细了解每项条例的法律背景。

将单独跟踪每种法规类型的作业。 要在调节类型之间切换，请选择 **[!UICONTROL 调节类型]** 下拉菜单，并从列表中选择所需的规则。

![规则类型下拉列表](../images/user-guide/regulation.png)

当更改法规类型时，功能板会进行更新，以显示适用于所选法规的所有操作、过滤器、小部件和职务创建对话框。

![更新了功能板](../images/user-guide/dashboard-update.png)

### 状态报表

状态报表小组件左侧的图表会跟踪已提交的作业，以及可能已报告有错误的任何作业。 右侧的图表跟踪接近30天合规性窗口结束的作业。

选择图表上方的两个切换按钮之一，以显示或隐藏其各自的量度。

![](../images/user-guide/hide-errors.png)

通过将鼠标悬停在相关数据点上，可以查看与图形上的任何数据点关联的确切作业数。

![将鼠标悬停在数据点上](../images/user-guide/mouse-over.png)

要查看有关给定数据点的更多详细信息，请选择相关数据点，以在“作业请求”小组件中显示相关的作业。 请注意应用于作业列表上方的过滤器。

![从小组件中应用的过滤器](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>将过滤器应用到“作业请求”小组件后，您可以通过选择 **X** 在药丸上。 然后，作业请求返回到默认跟踪列表。

### 作业请求

作业请求小组件列出了您组织中所有可用的作业请求，包括请求类型、当前状态、到期日期和请求者电子邮件等详细信息。

>[!NOTE]
>
>之前创建的作业的数据仅在完成日期后30天内可访问。

您可以在“作业请求”标题下方的搜索栏中键入关键字以过滤列表。 该列表会根据您的键入自动进行过滤，并显示包含与您的搜索词匹配值的请求。 您还可以使用 **[!UICONTROL 请求日期]** 用于为列出的作业选择时间范围的下拉菜单。

![作业请求搜索选项](../images/user-guide/job-search.png)

要查看特定作业请求的详细信息，请从列表中选择该请求的作业ID以打开 **[!UICONTROL 作业详细信息]** 页面。

![GDPR UI作业详细信息](../images/user-guide/job-details.png)

此对话框包含有关每个 [!DNL Experience Cloud] 解决方案及其当前状态与整体工作的关系。 由于每个隐私作业都是异步的，因此页面会显示每个解决方案的最新通信日期和时间(GMT)，因为有些解决方案在处理请求时需要的时间比其他解决方案多。

如果解决方案提供了任何其他数据，则可在此对话框中查看该数据。 您可以通过选择单个产品行来查看此数据。

要将完整的作业数据下载为CSV文件，请选择 **[!UICONTROL 导出到CSV]** 对话框的右上方。

## 创建新的隐私作业请求 {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="说明"
>abstract="<ul><li>选择 <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html#logging-in-from-experience-platform">请求</a> 在左侧导航中打开隐私Ul，然后选择 <b>创建请求</b>.</li><li>从此处，您可以使用请求生成器或上传数据主体的JSON文件。</li><li>如果使用请求生成器，请选择作业类型（访问和/或删除），然后选择您提供的身份类型（电子邮件、ECID或AAID），或输入自定义身份命名空间。 为客户输入相应的标识值，然后选择 <b>创建</b> 完成。</li><li>如果上传JSON文件，请选择创建请求旁边的箭头。 从选项列表中，选择 <b>上传JSON</b> 并上传您的文件。 如果您没有要上传的JSON文件，请选择 <b>下载Adobe-GDPR-Request.json</b> 下载可填充的模板。 上传JSON并选择 <b>创建</b> 完成。</li><li>有关此功能的更多帮助，请参阅 <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=zh-Hans">Privacy Service用户指南</a> Experience League。</li></ul>"

>[!NOTE]
>
>要创建隐私作业请求，您必须为要访问或删除其数据的特定客户提供身份信息。 请查阅 [隐私请求的身份数据](../identity-data.md) ，然后再继续使用此部分。

的 [!DNL Privacy Service] UI提供了两种创建新作业请求的方法：

* [使用请求生成器](#request-builder)
* [上传JSON文件](#json)

以下各节提供了使用上述每种方法的步骤。

### 使用请求生成器 {#request-builder}

使用请求生成器，您可以在用户界面中手动创建新的隐私作业请求。 请求生成器最适合于更简单和更小的请求集，因为请求生成器将请求限制为每个用户只具有ID类型。 对于更复杂的请求，最好是 [上传JSON文件](#json) 中。

要开始使用请求生成器，请选择 **[!UICONTROL 创建请求]** 位于屏幕右侧的状态报表小组件下方。

![选择创建请求](../images/user-guide/create-request.png)

的 **[!UICONTROL 创建请求]** 对话框打开，显示用于提交当前选定法规类型的隐私作业请求的可用选项。

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

选择 **[!UICONTROL 作业类型]** 请求（“删除”或“访问”）以及列表中一个或多个可用产品。

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

在 **[!UICONTROL 命名空间类型]**，为要发送到的客户ID选择相应的命名空间类型 [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

使用标准命名空间类型时，从下拉菜单（电子邮件、ECID或AAID）中选择命名空间，然后在右侧的文本框中键入ID值，然后按 **\&lt;enter>** ，以将其添加到列表中。

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

使用自定义命名空间类型时，必须先手动键入命名空间，然后再提供下面的ID值。

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

完成后，选择 **[!UICONTROL 创建]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

该对话框会消失，新作业（或作业）连同其当前处理状态一起列在作业请求小组件中。

### 上传JSON文件 {#json}

在创建更复杂的请求（例如对处理的每个数据主体使用多个ID类型的请求）时，您可以通过上传JSON文件来创建请求。

选择旁边的箭头 **[!UICONTROL 创建请求]**，位于屏幕右侧状态报表小组件下方。 从显示的选项列表中，选择 **[!UICONTROL 上传JSON]**.

![请求创建选项](../images/user-guide/create-options.png)

的 **[!UICONTROL 上传JSON]** 对话框中，提供了一个窗口供您将JSON文件拖放到中。

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

如果您没有要上传的JSON文件，请选择 **[!UICONTROL 下载Adobe-GDPR-Request.json]** 下载模板，以根据从数据主体收集的值进行填充。


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


在计算机上找到JSON文件，并将其拖到对话框窗口中。 如果上传成功，则会在对话框中显示文件名。 您可以根据需要，继续添加更多JSON文件，方法是将它们拖放到对话框中。

完成后，选择 **[!UICONTROL 创建]**. 该对话框会消失，新作业（或作业）连同其当前处理状态一起列在作业请求小组件中。

### 后续步骤

通过阅读本文档，您已学会了如何使用 [!DNL Privacy Service] 用于创建隐私作业、查看作业的详细信息并监视其处理状态的UI，并在作业完成后下载结果。

有关如何使用 [!DNL Privacy Service] API，请参阅 [API指南](../api/overview.md).
