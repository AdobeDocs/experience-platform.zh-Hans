---
keywords: Experience Platform；主页；热门主题；导出；导出
solution: Experience Platform
title: 在Privacy Service UI中管理隐私作业
description: 了解如何使用Privacy Service用户界面跨各种Experience Cloud应用程序协调和监视隐私请求。
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: b960e67789acaeb27a0a39db933a2bbb7d84f4d5
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 12%

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

[!DNL Privacy Service] UI的仪表板提供两个小组件，允许您查看隐私作业的状态：“[!UICONTROL Status Report]”和“[!UICONTROL Job Requests]”。 该仪表板还会显示所显示任务的当前选定法规。

![UI仪表板](../images/user-guide/dashboard.png)

### 法规类型

[!DNL Privacy Service]支持多个隐私法规的作业请求。 下表列出了支持的法规及其在UI中表示的相应标签。

请参阅[隐私法规概述](../regulations/overview.md)，了解有关消费者权利和强制商业义务的各项法规的说明。

>[!TIP]
>
>为方便起见，已包含API法规类型。

| UI标签 | API `regulation_type` | 法规 |
|-------------------------------------------|-----------------------|----------------|
| [!UICONTROL APA_AUS (Australia)] | `apa_aus` | [!DNL Australia Privacy Act] |
| [!UICONTROL CCCA (California)] | `ccpa` | [!DNL California Consumer Privacy Act] (CCPA) |
| [!UICONTROL CPA_CO_USA (Colorado)] | `cpa_co_usa` | [!DNL Colorado Privacy Act] |
| [!UICONTROL CPRA_CA_USA (California)] | `cpra_ca_usa` | [!DNL California Privacy Rights Act] (CPRA) |
| [!UICONTROL CTDPA_CT_USA (Connecticut)] | `ctdpa_ct_usa` | [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL DPDPA_DE_USA (Delaware)] | `dpdpa_de_usa` | [!DNL Delaware Personal Data Privacy Act] |
| [!UICONTROL FDBR_FL_USA (Florida)] | `fdbr_fl_usa` | [!DNL Florida Digital Bill of Rights] |
| [!UICONTROL GDPR (European Union)] | `gdpr` | 欧盟的[!DNL General Data Protection Regulation] |
| [!UICONTROL HIPAA_USA (United States)] | `hipaa_usa` | [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL ICDPALIA_USA (Iowa)] | `icdpa_ia_usa` | [!DNL Iowa Consumer Data Protection Act] |
| [!UICONTROL LGPD_BRA (Brazil)] | `lgpd_bra` | 巴西的“[!DNL General Data Protection Law]”[!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL MCDPA_MN_USA (Minnesota)] | `mcdpa_mn_usa` | [!DNL Minnesota Consumer Data Privacy Act] |
| [!UICONTROL MCDPA_MT_USA (Montana)] | `mcdpa_mt_usa` | [!DNL Montana Consumer Data Privacy Act] |
| [!UICONTROL MHMDA_WA_USA (Washington)] | `mhmda_wa_usa` | [!DNL Washington My Health My Data Act] |
| [!UICONTROL MODPA_MD_USA (Maryland)] | `modpa_md_usa` | [!DNL Maryland Online Data Privacy Act] |
| [!UICONTROL NDPA_NE_USA (Nebraska)] | `ndpa_ne_usa` | [!DNL Nebraska Data Protection Act] |
| [!UICONTROL NHPA_NH_USA (New Hampshire)] | `nhpa_nh_usa` | [!DNL New Hampshire Privacy Act] |
| [!UICONTROL NJDPA_NJ_USA (New Jersey)] | `njdpa_nj_usa` | [!DNL New Jersey Data Protection Act] |
| [!UICONTROL NZPA_NZL (New Zealand)] | `nzpa_nzl` | 新西兰的[!DNL Privacy Act] (PA) |
| [!UICONTROL OCPA_OR_USA (Oregon)] | `ocpa_or_usa` | [!DNL Oregon Consumer Privacy Act] |
| [!UICONTROL PDPA_THA (Thailand)] | `pdpa_tha` | 泰国的[!DNL Personal Data Protection Act] (PDPA) |
| [!UICONTROL PIPA_KOR (South Korea)] | `pipa_kor` | 韩国的[!DNL Personal Information Privacy Act] (PIPA) |
| [!UICONTROL QL25_QC_CAN (Quebec)] | `ql25_qc_can` | [!DNL Quebec Law 25] |
| [!UICONTROL TDPSA_TX_USA (Texas)] | `tdpsa_tx_usa` | [!DNL Texas Data Privacy and Security Act] |
| [!UICONTROL TIPA_TN_USA (Tennessee)] | `tipa_tn_usa` | [!DNL Tennessee Information Protection Act] |
| [!UICONTROL UCPA_UT_USA (Utah)] | `ucpa_ut_usa` | [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_VA_USA (Virginia)] | `vcdpa_va_usa` | [!DNL Virginia Consumer Data Protection Act] (VCDPA) |

{style="table-layout:auto"}

<!-- | [!UICONTROL ICDPA_IN_USA (Indiana)]       | `icdpa_in_usa` | [!DNL Indiana Consumer Data Protection Act]| NOT SUPP YET JAN 1st ### ... -->
<!-- | [!UICONTROL KCDPA_KY_USA (Kentucky)]      | `kcdpa_ky_usa`| [!DNL Kentucky Consumer Data Protection Act]|  NOT SUPP YET JAN 1st ### ... -->
<!-- | [!UICONTROL RIDTPPA_RI_USA (Rhode Island)]| `ridtppa_ri_usa` | [!DNL Rhode Island Data Transparency and Privacy Protection Act]|  NOT SUPP YET JAN 1st ### ... -->

>[!NOTE]
>
>有关每种法规的法律背景的更多信息，请参阅[支持的隐私法规](../regulations/overview.md)概述。

每种法规类型的作业将单独进行跟踪。 要在法规类型之间切换，请选择&#x200B;**[!UICONTROL Regulation Type]**&#x200B;下拉菜单，然后从列表中选择所需的法规。

![具有Regulation Type下拉列表的Privacy Service控制台。](../images/user-guide/regulation.png)

更改法规类型后，仪表板将更新以显示适用于所选法规的所有操作、筛选器、小部件和作业创建对话框。

![已更新仪表板](../images/user-guide/dashboard-update.png)

### 状态报表

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

[!UICONTROL Job Requests]工作区列出了有关组织中最近作业请求的详细信息。 详细信息包括请求类型、当前状态、截止日期、请求者电子邮件等。 一次加载100条记录集。 默认情况下，当向下滚动浏览时，最近创建的作业将显示在顶部，并加载更多记录集。

>[!NOTE]
>
>以前创建的作业的数据只能在完成日期后的30天内访问。

您可以通过在[!UICONTROL Job Requests]标题下方的搜索栏中输入关键字来筛选列表。 列表会在您键入时自动进行筛选，并显示包含与您的搜索词匹配的值的请求。 搜索字段执行“快速”搜索，将隐私作业ID与UI中当前渲染/加载的作业相匹配。 它并非全面搜索您提交的所有作业。 而是应用于加载结果的过滤器。 使用Privacy Service API可[根据特定法规、日期范围或单个作业](../api/privacy-jobs.md#list)返回作业。

>[!TIP]
>
>要将过去30天的记录加载到UI中，必须向下滚动表并加载更多记录批次。

![突出显示搜索字段的“隐私控制台作业请求”部分。](../images/user-guide/job-search.png)

或者，使用搜索按钮执行跨特定日期范围的隐私作业查询。 此操作返回贵组织在给定时间范围内提交的所有隐私作业。 选择&#x200B;**[!UICONTROL Requested on]**&#x200B;下拉菜单以选择查询的开始日期和完成日期。 可用选项包括[!UICONTROL Today]、[!UICONTROL Last 7 Days]、[!UICONTROL Last 2 Weeks]、[!UICONTROL Last 30 Days]或[!UICONTROL Custom]。 与[!UICONTROL Requested on]选项一起使用时，搜索功能仅显示所选日期范围之间提交的作业请求。

![包含搜索字段的“作业请求”部分，“已请求”位于下拉菜单，且“搜索”按钮突出显示。](../images/user-guide/requested-on-dropdown-menu.png)

要查看特定作业请求的详细信息，请从列表中选择该请求的作业ID以打开&#x200B;**[!UICONTROL Job Details]**&#x200B;页。

![GDPR UI作业详细信息](../images/user-guide/job-details.png)

此对话框包含有关每个[!DNL Experience Cloud]解决方案的状态信息及其相对于整个作业的当前状态。 由于每个隐私作业都是异步的，因此页面会显示每个解决方案的最新通信日期和时间(GMT)，因为有些解决方案处理请求所需的时间比其他解决方案多。

如果解决方案提供了任何其他数据，则可在该对话框中查看。 您可以通过选择单个产品行来查看此数据。

要将完整的作业数据下载为CSV文件，请选择对话框右上角的&#x200B;**[!UICONTROL Export to CSV]**。

## 创建新的隐私作业请求 {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="说明"
>abstract="<ul><li>在左侧导航中选择<a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html#logging-in-from-experience-platform">请求</a>以打开 Privacy Ul，然后选择<b>创建请求</b>。</li><li>从这里可使用请求生成器或上传数据主体的 JSON 文件。</li><li>如果使用请求生成器，则选择作业类型（访问和/或删除），然后选择您提供的身份标识类型（电子邮件、ECID 或 AAID）或输入自定义身份标识命名空间。输入适合客户的身份标识值，并在完成后选择<b>创建</b>。</li><li>如果上传 JSON 文件，则选择“创建请求”旁边的箭头。从选项列表中，选择<b>上传 JSON</b> 并上传您的文件。如果您没有要上传的 JSON 文件，则选择<b>下载 Adobe-GDPR-Request.json</b> 以下载可填写的模板。上传 JSON，并在完成后选择<b>创建</b>。</li><li>有关此功能的更多帮助，请参阅 Experience League 上的 <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=zh-Hans">Privacy Service 用户指南</a>。</li></ul>"

>[!NOTE]
>
>要创建隐私作业请求，您必须提供其数据将被访问或删除的特定客户的身份信息。 在继续此部分之前，请查看隐私请求[的](../identity-data.md)身份数据的文档。

[!DNL Privacy Service] UI提供了两种创建新作业请求的方法：

* [使用请求生成器](#request-builder)
* [上传JSON文件](#json)

以下各节提供了使用每种方法的步骤。

### 使用请求生成器 {#request-builder}

使用请求生成器，您可以在用户界面中手动创建新的隐私作业请求。 请求生成器最适合用于更简单、更小的请求集，因为请求生成器限制每个用户的请求只能具有ID类型。 对于更复杂的请求，最好[上传JSON文件](#json)。

要开始使用请求生成器，请在屏幕右侧的状态报表小部件下方选择&#x200B;**[!UICONTROL Create Request]**。

![选择创建请求](../images/user-guide/create-request.png)

将打开&#x200B;**[!UICONTROL Create Request]**&#x200B;对话框，其中显示用于提交当前所选法规类型的隐私作业请求的可用选项。

![](../images/user-guide/request-builder.png){width=500}

从列表中选择请求的&#x200B;**[!UICONTROL Job Type]**（“删除”或“访问”）以及一个或多个可用产品。

Privacy Service支持两种针对个人数据的作业请求：[!UICONTROL Access] （读取）和/或[!UICONTROL Delete]。 您可以提交请求，以接收产品中保存的与查询主题相关的所有信息，也可以请求删除与查询主题相关的所有信息。

![](../images/user-guide/type-and-products.png){width=500}

在&#x200B;**[!UICONTROL Namespace type]**&#x200B;下，为发送到[!DNL Privacy Service]的客户ID选择适当的命名空间类型。

![](../images/user-guide/namespace-type.png){width=500}

使用标准命名空间类型时，请从下拉菜单（电子邮件、ECID或AAID）中选择命名空间，然后在右侧的文本框中键入ID值，为每个ID按&#x200B;**\&lt;enter>**&#x200B;以将其添加到列表中。

![](../images/user-guide/standard-namespace.png){width=500}

使用自定义命名空间类型时，必须先手动键入命名空间，然后才能提供以下ID值。

![](../images/user-guide/custom-namespace.png){width=500}

完成后，选择&#x200B;**[!UICONTROL Create]**。

![](../images/user-guide/request-builder-create.png){width=500}

该对话框消失，新作业（或多个作业）及其当前处理状态将列在作业请求小部件中。

### 上传JSON文件 {#json}

创建更复杂的请求时（例如为每个处理的数据主体使用多个ID类型的请求），您可以通过上传JSON文件创建请求。

选择屏幕右侧“状态报告”小部件下方&#x200B;**[!UICONTROL Create Request]**&#x200B;旁边的箭头。 从显示的选项列表中，选择&#x200B;**[!UICONTROL Upload JSON]**。

![请求创建选项](../images/user-guide/create-options.png)

此时将显示&#x200B;**[!UICONTROL Upload JSON]**&#x200B;对话框，为您提供了一个将JSON文件拖放到中的窗口。

![](../images/user-guide/upload-json.png){width=500}

如果您没有要上传的JSON文件，请选择&#x200B;**[!UICONTROL Download Adobe-GDPR-Request.json]**&#x200B;以下载可以根据您从数据主体收集的值填充的模板。


![](../images/user-guide/privacy-template.png){width=500}


在计算机上找到JSON文件，并将其拖到对话框窗口中。 如果上传成功，则文件名将显示在对话框中。 您可以通过将更多JSON文件拖放到对话框中，继续根据需要添加这些文件。

完成后，选择&#x200B;**[!UICONTROL Create]**。 该对话框消失，新作业（或多个作业）及其当前处理状态将列在作业请求小部件中。

### 后续步骤

通过阅读本文档，您已了解如何使用[!DNL Privacy Service] UI创建隐私作业、查看作业的详细信息并监视其处理状态，以及在作业完成后下载结果。

有关如何使用[!DNL Privacy Service] API以编程方式执行这些操作的步骤，请参阅[API指南](../api/overview.md)。
