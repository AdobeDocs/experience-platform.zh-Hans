---
keywords: Experience Platform；主页；热门主题；导出；导出
solution: Experience Platform
title: 在Privacy Service UI中管理隐私作业
description: 了解如何使用Privacy Service用户界面跨各种Experience Cloud应用程序协调和监视隐私请求。
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '1770'
ht-degree: 11%

---

# 在 Privacy Service UI 中管理隐私作业 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="遵守数据主体隐私请求"
>abstract="<h2>描述</h2><p>通过 Adobe Experience Platform Privacy Service，可代表要根据隐私法规访问或删除其个人数据的客户创建和管理隐私请求。</p>"

本文档提供了使用[!DNL Privacy Service]用户界面创建和管理隐私请求的步骤。

>[!IMPORTANT]
>
>Privacy Service仅适用于数据主体和消费者权利请求。 不支持或允许将Privacy Service用于数据清理或维护的任何其他用途。 Adobe有及时履行这些义务的法律义务。 因此，不允许在Privacy Service上进行负载测试，因为它是一个仅用于生产的环境，并会创建有效隐私请求的不必要积压。
>
>现已设定每日硬性上传限制，以防止滥用服务。 发现滥用系统的用户将禁用其对该服务的访问权限。 随后将与他们举行一次会议，讨论他们的行动并讨论Privacy Service的可接受用途。

## 浏览[!DNL Privacy Service]用户界面仪表板

[!DNL Privacy Service] UI的仪表板提供两个允许您查看隐私作业状态的小组件：“[!UICONTROL 状态报告]”和“[!UICONTROL 作业请求]”。 该仪表板还会显示所显示任务的当前选定法规。

![UI仪表板](../images/user-guide/dashboard.png)

### 法规类型

[!DNL Privacy Service]支持多个隐私法规的作业请求。 下表列出了支持的法规及其在UI中表示的相应标签：

| UI标签 | 法规 |
|-------------------------------------|------------------------|
| [!UICONTROL APA_AUS （澳大利亚）] | [!DNL Australia Privacy Act] |
| [!UICONTROL CCPA （加利福尼亚）] | [!DNL California Consumer Privacy Act] |
| [!UICONTROL CPA_USA （科罗拉多）] | [!DNL Colorado Privacy Act] |
| [!UICONTROL CPRA_USA（加利福尼亚）] | [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL CTDPA_USA （康涅狄格州）] | [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL DPDPA_USA（特拉华州）] | [!DNL Delaware Personal Data Privacy Act] |
| [!UICONTROL FDBR_USA（佛罗里达州）] | [!DNL Florida Digital Bill of Rights] |
| [!UICONTROL GDPR （欧盟）] | 欧盟的[!DNL General Data Protection Regulation] |
| [!UICONTROL HIPPA_USA（美国）] | [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL ICDPA_USA] （爱荷华州） | [!DNL Iowa Consumer Data Protection Act] |
| [!UICONTROL LGPD_BRA（巴西）] | 巴西的“[!DNL General Data Protection Law]”[!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL MHMDA_USA（华盛顿）] | [!DNL Washington My Health My Data Act] |
| [!UICONTROL MCDPA_USA （蒙大拿州）] | [!DNL Montana Consumer Data Privacy Act] |
| [!UICONTROL NDPA_USA （内布拉斯加州）] | [!DNL Nebraska Data Protection Act] |
| [!UICONTROL NZPA_NZL（新西兰）] | 新西兰的[!DNL Privacy Act] |
| [!UICONTROL NHPA_USA（新罕布什尔州）] | [!DNL New Hampshire Privacy Act] |
| [!UICONTROL NJDPA_USA（新泽西）] | [!DNL New Jersey Data Protection Act] |
| [!UICONTROL OCPA USA （俄勒冈）] | [!DNL Oregon Consumer Privacy Act] |
| [!UICONTROL PDPA_THA（泰国）] | 泰国的[!DNL Personal Data Protection Act] |
| [!UICONTROL QL25_CAN （魁北克）] | [!DNL Quebec Law 25] |
| [!UICONTROL TDPSA美国（得克萨斯州）] | [!DNL Texas Data Privacy and Security Act] |
| [!UICONTROL UCPA_USA （犹他州）] | [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_USA（弗吉尼亚）] | [!DNL Virginia Consumer Data Protection Act] |

{style="table-layout:auto"}

<!-- 
Waiting:
| **[!UICONTROL PIPA_KOR]**  ?        | South Korea [!DNL Personal Information Privacy Act] |
 -->

>[!NOTE]
>
>有关每种法规的法律背景的更多信息，请参阅[支持的隐私法规](../regulations/overview.md)概述。

每种法规类型的作业将单独进行跟踪。 要在法规类型之间切换，请选择&#x200B;**[!UICONTROL 法规类型]**&#x200B;下拉菜单，然后从列表中选择所需的法规。

![具有Regulation Type下拉列表的Privacy Service控制台。](../images/user-guide/regulation.png)

更改法规类型后，仪表板将更新以显示适用于所选法规的所有操作、筛选器、小部件和作业创建对话框。

![已更新仪表板](../images/user-guide/dashboard-update.png)

### 状态报告

状态报表小组件左侧的图形可跟踪已提交作业，以及任何可能已报告并出现错误的作业。 右侧的图表将跟踪接近30天合规性窗口末尾的作业。

选择图形上方的两个切换按钮之一，可显示或隐藏其各自的量度。

![](../images/user-guide/hide-errors.png)

通过将鼠标悬停在相关数据点上，可以查看与图形上任何数据点关联的准确作业数。

![鼠标悬停在数据点上](../images/user-guide/mouse-over.png)

要查看有关给定数据点的更多详细信息，请选择相关数据点以在作业请求小组件中显示关联的作业。 记下在作业列表上方应用的过滤器。

![从小部件应用了筛选器](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>将过滤器应用于“作业请求”小部件后，您可以通过选择过滤器面板上的&#x200B;**X**&#x200B;来删除该过滤器。 然后，作业请求返回到默认跟踪列表。

### 作业请求 {#job-requests}

[!UICONTROL 作业请求]工作区列出了有关组织中最近作业请求的详细信息。 详细信息包括请求类型、当前状态、截止日期、请求者电子邮件等。 一次加载100条记录集。 默认情况下，当向下滚动浏览时，最近创建的作业将显示在顶部，并加载更多记录集。

>[!NOTE]
>
>以前创建的作业的数据只能在完成日期后的30天内访问。

您可以通过在[!UICONTROL 作业请求]标题下面的搜索栏中输入关键字来筛选列表。 列表会在您键入时自动进行筛选，并显示包含与您的搜索词匹配的值的请求。 搜索字段执行“快速”搜索，将隐私作业ID与UI中当前渲染/加载的作业相匹配。 它并非全面搜索您提交的所有作业。 而是应用于加载结果的过滤器。 使用Privacy Service API可[根据特定法规、日期范围或单个作业](../api/privacy-jobs.md#list)返回作业。

>[!TIP]
>
>要将过去30天的记录加载到UI中，必须向下滚动表并加载更多记录批次。

![突出显示搜索字段的“隐私控制台作业请求”部分。](../images/user-guide/job-search.png)

或者，使用搜索按钮执行跨特定日期范围的隐私作业查询。 此操作返回贵组织在给定时间范围内提交的所有隐私作业。 选择&#x200B;**[!UICONTROL 请求日期]**&#x200B;下拉菜单以选择查询的开始日期和完成日期。 可用选项包括[!UICONTROL 今天]、[!UICONTROL 最近7天]、[!UICONTROL 最近2周]、[!UICONTROL 最近30天]或[!UICONTROL 自定义]。 与[!UICONTROL 请求日期]选项一起使用时，搜索功能仅显示所选日期范围之间提交的作业请求。

![包含搜索字段的“作业请求”部分，“已请求”位于下拉菜单，且“搜索”按钮突出显示。](../images/user-guide/requested-on-dropdown-menu.png)

要查看特定作业请求的详细信息，请从列表中选择该请求的作业ID以打开&#x200B;**[!UICONTROL 作业详细信息]**&#x200B;页。

![GDPR UI作业详细信息](../images/user-guide/job-details.png)

此对话框包含有关每个[!DNL Experience Cloud]解决方案的状态信息及其相对于整个作业的当前状态。 由于每个隐私作业都是异步的，因此页面会显示每个解决方案的最新通信日期和时间(GMT)，因为有些解决方案处理请求所需的时间比其他解决方案多。

如果解决方案提供了任何其他数据，则可在该对话框中查看。 您可以通过选择单个产品行来查看此数据。

要将完整的作业数据下载为CSV文件，请选择对话框右上角的&#x200B;**[!UICONTROL 导出到CSV]**。

## 创建新的隐私作业请求 {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="说明"
>abstract="<ul><li>在左侧导航中选择<a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=zh-Hans#logging-in-from-experience-platform">请求</a>以打开 Privacy Ul，然后选择<b>创建请求</b>。</li><li>从这里可使用请求生成器或上传数据主体的 JSON 文件。</li><li>如果使用请求生成器，则选择作业类型（访问和/或删除），然后选择您提供的身份标识类型（电子邮件、ECID 或 AAID）或输入自定义身份标识命名空间。输入适合客户的身份标识值，并在完成后选择<b>创建</b>。</li><li>如果上传 JSON 文件，则选择“创建请求”旁边的箭头。从选项列表中，选择<b>上传 JSON</b> 并上传您的文件。如果您没有要上传的 JSON 文件，则选择<b>下载 Adobe-GDPR-Request.json</b> 以下载可填写的模板。上传 JSON，并在完成后选择<b>创建</b>。</li><li>有关此功能的更多帮助，请参阅 Experience League 上的 <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=zh-Hans">Privacy Service 用户指南</a>。</li></ul>"

>[!NOTE]
>
>要创建隐私作业请求，您必须提供其数据将被访问或删除的特定客户的身份信息。 在继续此部分之前，请查看隐私请求[&#128279;](../identity-data.md)的身份数据的文档。

[!DNL Privacy Service] UI提供了两种创建新作业请求的方法：

* [使用请求生成器](#request-builder)
* [上传JSON文件](#json)

以下各节提供了使用每种方法的步骤。

### 使用请求生成器 {#request-builder}

使用请求生成器，您可以在用户界面中手动创建新的隐私作业请求。 请求生成器最适合用于更简单、更小的请求集，因为请求生成器限制每个用户的请求只能具有ID类型。 对于更复杂的请求，最好[上传JSON文件](#json)。

要开始使用请求生成器，请选择屏幕右侧“状态报告”小组件下方的&#x200B;**[!UICONTROL 创建请求]**。

![选择创建请求](../images/user-guide/create-request.png)

将打开&#x200B;**[!UICONTROL 创建请求]**&#x200B;对话框，其中显示了用于提交当前所选法规类型的隐私作业请求的可用选项。

![](../images/user-guide/request-builder.png){width=500}

从列表中选择请求的&#x200B;**[!UICONTROL 作业类型]**（“删除”或“访问”）以及一个或多个可用产品。

Privacy Service支持两种针对个人数据的作业请求：[!UICONTROL 访问] （读取）和/或[!UICONTROL 删除]。 您可以提交请求，以接收产品中保存的与查询主题相关的所有信息，也可以请求删除与查询主题相关的所有信息。

![](../images/user-guide/type-and-products.png){width=500}

在&#x200B;**[!UICONTROL 命名空间类型]**&#x200B;下，为要发送到[!DNL Privacy Service]的客户ID选择适当的命名空间类型。

![](../images/user-guide/namespace-type.png){width=500}

使用标准命名空间类型时，请从下拉菜单（电子邮件、ECID或AAID）中选择命名空间，然后在右侧的文本框中键入ID值，为每个ID按&#x200B;**\&lt;enter>**&#x200B;以将其添加到列表中。

![](../images/user-guide/standard-namespace.png){width=500}

使用自定义命名空间类型时，必须先手动键入命名空间，然后才能提供以下ID值。

![](../images/user-guide/custom-namespace.png){width=500}

完成后，选择&#x200B;**[!UICONTROL 创建]**。

![](../images/user-guide/request-builder-create.png){width=500}

该对话框消失，新作业（或多个作业）及其当前处理状态将列在作业请求小部件中。

### 上传JSON文件 {#json}

创建更复杂的请求时（例如为每个处理的数据主体使用多个ID类型的请求），您可以通过上传JSON文件创建请求。

选择屏幕右侧“状态报告”小组件下&#x200B;**[!UICONTROL 创建请求]**&#x200B;旁边的箭头。 从显示的选项列表中，选择&#x200B;**[!UICONTROL 上传JSON]**。

![请求创建选项](../images/user-guide/create-options.png)

此时将显示&#x200B;**[!UICONTROL 上传JSON]**&#x200B;对话框，为您提供了一个将JSON文件拖放到中的窗口。

![](../images/user-guide/upload-json.png){width=500}

如果您没有要上传的JSON文件，请选择&#x200B;**[!UICONTROL 下载Adobe-GDPR-Request.json]**&#x200B;以下载一个模板，您可以根据从数据主体那里收集的值填充该模板。


![](../images/user-guide/privacy-template.png){width=500}


在计算机上找到JSON文件，并将其拖到对话框窗口中。 如果上传成功，则文件名将显示在对话框中。 您可以通过将更多JSON文件拖放到对话框中，继续根据需要添加这些文件。

完成后，选择&#x200B;**[!UICONTROL 创建]**。 该对话框消失，新作业（或多个作业）及其当前处理状态将列在作业请求小部件中。

### 后续步骤

通过阅读本文档，您已了解如何使用[!DNL Privacy Service] UI创建隐私作业、查看作业的详细信息并监视其处理状态，以及在作业完成后下载结果。

有关如何使用[!DNL Privacy Service] API以编程方式执行这些操作的步骤，请参阅[API指南](../api/overview.md)。
