---
keywords: Experience Platform；主页；热门主题；流连接；创建流连接；UI指南；教程；创建流连接；流摄取；
solution: Experience Platform
title: 使用UI创建流连接
topic-legacy: tutorial
type: Tutorial
description: 本UI指南将帮助您使用Adobe Experience Platform创建流连接。
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: df6ddf52f5cab7e5faae591594f060d641977783
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 0%

---


# 使用UI创建流连接

本教程提供了使用[!UICONTROL Sources]工作区创建流源连接的步骤。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):用于组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

## 创建流连接

在平台UI中，从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 [!UICONTROL Catalog]屏幕显示了您可以使用创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在&#x200B;**[!UICONTROL 流]**&#x200B;类别下，选择&#x200B;**[!UICONTROL HTTP API]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![目录](../../../../images/tutorials/create/http/catalog.png)

出现&#x200B;**[!UICONTROL 连接HTTP API帐户]**&#x200B;页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择要使用创建新数据流的HTTP API帐户，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![现有帐户](../../../../images/tutorials/create/http/existing.png)

### 新帐户

如果要创建新帐户，请选择&#x200B;**[!UICONTROL 新建帐户]**。 在显示的输入窗体上，提供帐户名称和可选描述。 您还可以选择提供以下配置属性：

- **[!UICONTROL 身份验证]:** 此属性确定流连接是否需要身份验证。身份验证可确保从可信来源收集数据。 如果您要处理个人身份信息(PII)，则应该打开此资产。 默认情况下，此属性处于关闭状态。
- **[!UICONTROL XDM兼容]:** 此属性指示此流连接是否将发送与XDM架构兼容的事件。默认情况下，此属性处于关闭状态。

完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![新帐户](../../../../images/tutorials/create/http/new.png)

## 选择数据

创建HTTP API连接后，将显示&#x200B;**[!UICONTROL 选择数据]**&#x200B;步骤，为您提供一个用于上传和预览数据的接口。

选择&#x200B;**[!UICONTROL 上传文件]**&#x200B;以上传数据。 或者，也可以将数据拖放到界面的[!UICONTROL 拖放文件]部分。

![添加数据](../../../../images/tutorials/create/http/add-data.png)

上传数据后，您可以使用界面的右侧预览文件层次结构。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## 将数据字段映射到XDM架构

将显示[!UICONTROL 映射]步骤，提供一个接口，用于将源数据映射到Platform数据集。

Parquet文件必须符合XDM标准，并且不需要您手动配置映射，而CSV文件要求您明确配置映射，但允许您选择要映射的源数据字段。 如果JSON文件标记为XDM投诉，则无需手动配置。 但是，如果它未标记为符合XDM，则需要您明确配置映射。

为要摄取到的入站数据选择数据集。 您可以使用现有数据集，也可以创建新数据集。

### 创建新数据集

要创建新数据集，请选择&#x200B;**[!UICONTROL New dataset]**。 在显示的表单中，提供名称、可选描述以及数据集的目标架构。 如果选择启用了[!DNL Profile]的架构，则可以选择数据集是否也应启用[!DNL Profile]。

![新数据集](../../../../images/tutorials/create/http/new-dataset.png)

### 使用现有数据集

要使用现有数据集，请选择&#x200B;**[!UICONTROL 现有数据集]**。 在显示的表单中，选择要使用的数据集。 选择数据集后，您可以选择是否应启用该数据集[!DNL Profile]。

![现有数据集](../../../../images/tutorials/create/http/existing-dataset.png)

### 映射标准字段

根据您的需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以导出计算值或计算值。 有关映射器函数和计算字段的详细信息，请参阅[数据准备函数指南](../../../../../data-prep/functions.md)或[计算字段指南](../../../../../data-prep/calculated-fields.md)。

要添加新源字段，请选择&#x200B;**[!UICONTROL 添加新映射]**。

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

出现新的源字段和目标字段配对。 要添加新的源字段，请选择[!UICONTROL 选择源字段]输入栏旁边的箭头图标。

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

通过[!UICONTROL 选择属性]面板，您可以浏览文件层次结构并选择要映射到目标XDM字段的特定源字段。 选择要映射的源字段后，选择&#x200B;**[!UICONTROL 选择]**&#x200B;以继续。

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

现在，选择源字段后，您可以识别要映射到的相应目标XDM字段。 选择目标字段部分下的架构图标。

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

此时会出现[!UICONTROL 将源字段映射到目标字段]窗口，为您提供一个界面来浏览目标数据集的架构。 选择与源字段匹配的目标字段，然后选择&#x200B;**[!UICONTROL 选择]**&#x200B;以继续。

![映射到目标字段](../../../../images/tutorials/create/http/map-to-target-field.png)

在所有源字段都映射到相应的目标XDM字段后，选择&#x200B;**[!UICONTROL Next]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## 数据流详细信息

出现&#x200B;**[!UICONTROL 数据流详细信息]**&#x200B;步骤。 在本页中，您可以通过提供名称和可选描述来提供已创建数据流的详细信息。

在提供数据流的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

![数据流详细信息](../../../../images/tutorials/create/http/dataflow-detail.png)

## 审阅

此时将显示&#x200B;**[!UICONTROL 查看]**&#x200B;步骤，允许您在创建数据流之前查看数据流的详细信息。 详细信息属于以下类别：

- **[!UICONTROL 连接]**:显示帐户名称、源平台和源名称。
- **[!UICONTROL 分配数据集和映射字段]**:显示目标数据集以及数据集所遵循的架构。

确认详细信息正确后，选择&#x200B;**[!UICONTROL 完成]**。

![审查](../../../../images/tutorials/create/http/review.png)

## 获取流端点URL

创建连接后，将显示源详细信息页面。 本页显示新创建连接的详细信息，包括以前运行的数据流、ID和流端点URL。

![端点](../../../../images/tutorials/create/http/endpoint.png)

## 后续步骤

在本教程后，您创建了一个流HTTP连接，使您能够使用流端点访问各种[!DNL Data Ingestion] API。 有关在API中创建流连接的说明，请阅读[创建流连接教程](../../../api/create/streaming/http.md)。

要了解如何将数据流式传输到Platform，请阅读[流时间系列数据](../../../../../ingestion/tutorials/streaming-time-series-data.md)的教程或[流记录数据](../../../../../ingestion/tutorials/streaming-record-data.md)的教程。
