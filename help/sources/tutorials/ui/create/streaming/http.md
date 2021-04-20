---
keywords: Experience Platform；主页；热门主题；流连接；创建流连接；ui指南；教程；创建流连接；流摄取；
solution: Experience Platform
title: 使用UI创建流连接
topic: tutorial
type: Tutorial
description: 此UI指南将帮助您使用Adobe Experience Platform创建流连接。
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
translation-type: tm+mt
source-git-commit: 3b71f1399a770e097cf75827e626d6d4e289ab77
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---


# 使用UI创建流连接

本教程提供了使用[!UICONTROL Sources]工作区创建流源连接的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成的基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建基块，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

## 创建流连接

在平台UI中，从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 [!UICONTROL Catalog]屏幕显示了可创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在&#x200B;**[!UICONTROL Streaming]**&#x200B;类别下，选择&#x200B;**[!UICONTROL HTTP API]**，然后选择&#x200B;**[!UICONTROL Add data]**。

![目录](../../../../images/tutorials/create/http/catalog.png)

将显示&#x200B;**[!UICONTROL Connect HTTP API account]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择要用其创建新数据流的HTTP API帐户，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![existing-account](../../../../images/tutorials/create/http/existing.png)

### 新帐户

如果要创建新帐户，请选择&#x200B;**[!UICONTROL New account]**。 在显示的输入表单上，提供帐户名和可选说明。 您还可以选择提供以下配置属性：

- **[!UICONTROL Authentication]:** 此属性确定流连接是否需要身份验证。身份验证可确保从可信源收集数据。 如果您正在处理个人身份信息(PII)，应打开此属性。 默认情况下，此属性处于关闭状态。
- **[!UICONTROL XDM compatible]:** 此属性表示此流连接是否将发送与XDM模式兼容的事件。默认情况下，此属性处于关闭状态。

完成后，选择&#x200B;**[!UICONTROL Connect to source]**，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;继续。

![new-account](../../../../images/tutorials/create/http/new.png)

## 选择数据

创建HTTP API连接后，将显示&#x200B;**[!UICONTROL Select data]**&#x200B;步骤，为您提供一个用于上载和预览数据的接口。

选择&#x200B;**[!UICONTROL Upload files]**&#x200B;以上传您的数据。 或者，可以将数据拖放到接口的[!UICONTROL Drag and drop files]部分。

![add-data](../../../../images/tutorials/create/http/add-data.png)

上传数据后，您可以使用界面右侧的预览文件层次结构。 选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![预览-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## 将数据字段映射到XDM模式

将出现[!UICONTROL Mapping]步骤，提供一个接口将源数据映射到平台数据集。

Parke文件必须符合XDM标准，并且不要求您手动配置映射，而CSV文件要求您显式配置映射，但允许您选择要映射的源数据字段。 JSON文件（如果标记为XDM投诉）不需要手动配置。 但是，如果未标记为符合XDM规范，则需要显式配置映射。

为要摄取的入站数据选择数据集。 您可以使用现有数据集或创建新数据集。

### 创建新数据集

要创建新数据集，请选择&#x200B;**[!UICONTROL New dataset]**。 在显示的表单上，提供数据集的名称、可选说明以及目标模式。 如果选择[!DNL Profile]启用的模式，则可以选择数据集是否也应启用[!DNL Profile]。

![新数据集](../../../../images/tutorials/create/http/new-dataset.png)

### 使用现有数据集

要使用现有数据集，请选择&#x200B;**[!UICONTROL Existing dataset]**。 在显示的表单上，选择要使用的数据集。 选择数据集后，可以选择是否应启用该数据集[!DNL Profile]。

![existing-dataset](../../../../images/tutorials/create/http/existing-dataset.png)

### 映射标准字段

根据您的需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以导出计算值或计算值。 有关模式映射和映射器函数的详细信息，请参阅有关[将CSV数据映射到XDM字段](../../../../../ingestion/tutorials/map-a-csv-file.md)的教程。

要添加新源字段，请选择&#x200B;**[!UICONTROL Add new mapping]**。

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

将出现新的源字段和目标字段配对。 要添加新的源字段，请选择[!UICONTROL Select source field]输入栏旁的箭头图标。

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

[!UICONTROL Select attributes]面板允许您浏览文件层次结构并选择要映射到目标XDM字段的特定源字段。 选择要映射的源字段后，选择&#x200B;**[!UICONTROL Select]**&#x200B;继续。

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

选择源字段后，您现在可以标识要映射到的适当目标XDM字段。 在“模式”字段部分下选择目标图标。

![select-目标-field](../../../../images/tutorials/create/http/select-target-field.png)

将出现[!UICONTROL Map source field to target field]窗口，为您提供一个界面来浏览目标数据集的模式。 选择与源字段匹配的目标字段，然后选择&#x200B;**[!UICONTROL Select]**&#x200B;以继续。

![映射到目标字段](../../../../images/tutorials/create/http/map-to-target-field.png)

将源字段全部映射到相应的目标XDM字段后，请选择&#x200B;**[!UICONTROL Next]**

![数据准备完成](../../../../images/tutorials/create/http/data-prep-complete.png)

## 数据流详细信息

出现&#x200B;**[!UICONTROL Dataflow detail]**&#x200B;步骤。 在此页上，您可以通过提供名称和可选说明来提供创建的数据流的详细信息。

提供数据流的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

![数据流详细信息](../../../../images/tutorials/create/http/dataflow-detail.png)

## 审阅

将显示&#x200B;**[!UICONTROL Review]**&#x200B;步骤，允许您在创建数据流之前查看其详细信息。 详细信息按以下类别分组：

- **[!UICONTROL Connection]**:显示帐户名称、源平台和源名称。
- **[!UICONTROL Assign dataset and map fields]**:显示目标数据集和数据集附带的模式。

确认详细信息正确后，选择&#x200B;**[!UICONTROL Finish]**。

![审查](../../../../images/tutorials/create/http/review.png)

## 获取流端点URL

创建连接后，将显示源详细信息页。 本页显示您新创建的连接的详细信息，包括以前运行的数据流、ID和流端点URL。

![endipt](../../../../images/tutorials/create/http/endpoint.png)

## 后续步骤

通过本教程，您创建了流式HTTP连接，使您能够使用流式端点访问各种[!DNL Data Ingestion] API。 有关在API中创建流连接的说明，请阅读[创建流连接教程](../../../api/create/streaming/http.md)。

要了解如何将数据流化到平台，请阅读关于[流式时间系列数据](../../../../../ingestion/tutorials/streaming-time-series-data.md)的教程或关于[流式记录数据](../../../../../ingestion/tutorials/streaming-record-data.md)的教程。
