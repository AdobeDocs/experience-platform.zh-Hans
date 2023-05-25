---
keywords: Experience Platform；主页；热门主题；流连接；创建流连接；ui指南；教程；创建流连接；流摄取；摄取；
solution: Experience Platform
title: 使用UI创建HTTP API流连接
type: Tutorial
description: 本UI指南将帮助您使用Adobe Experience Platform创建流连接。
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 0%

---


# 创建 [!DNL HTTP API] 使用UI的流连接

本教程提供了使用创建流源连接的步骤。 [!UICONTROL 源] 工作区。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   - [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   - [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

## 创建流连接

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 **[!UICONTROL 流]** 类别，选择 **[!UICONTROL HTTP API]** 然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/http/catalog.png)

此 **[!UICONTROL 连接HTTP API帐户]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择要通过创建新数据流的HTTP API帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![existing-account](../../../../images/tutorials/create/http/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**. 在显示的输入表单上，提供帐户名称和可选描述。 您还可以选择提供以下配置属性：

- **[!UICONTROL 身份验证]：** 此属性确定流连接是否需要身份验证。 身份验证确保从可信来源收集数据。 如果您处理的是个人身份信息(PII)，则应该启用此属性。 默认情况下，此属性处于关闭状态。
- **[!UICONTROL 与XDM兼容]：** 此属性表示此流连接是否将发送与XDM架构兼容的事件。 默认情况下，此属性处于关闭状态。

完成后，选择 **[!UICONTROL 连接到源]** 然后选择 **[!UICONTROL 下一个]** 以继续。

![new-account](../../../../images/tutorials/create/http/new.png)

## 选择数据

创建HTTP API连接后， **[!UICONTROL 选择数据]** 步骤，为您提供上传和预览数据的界面。

选择 **[!UICONTROL 上传文件]** 以上传您的数据。 或者，您也可以将数据拖放到 [!UICONTROL 拖放文件] 部分。

![add-data](../../../../images/tutorials/create/http/add-data.png)

上传数据后，您可以使用界面的右侧预览文件层次结构。 选择 **[!UICONTROL 下一个]** 以继续。

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## 将数据字段映射到XDM架构

此 [!UICONTROL 映射] 此时将显示步骤，其中提供了一个将源数据映射到Platform数据集的界面。

Parquet文件必须与XDM兼容，并且不需要手动配置映射，而CSV文件需要您明确配置映射，但允许您选择要映射的源数据字段。 如果标记为XDM投诉，则JSON文件不需要手动配置。 但是，如果它未标记为XDM兼容，则需要您明确配置映射。

选择要引入的集客数据的数据集。 您可以使用现有数据集或创建新数据集。

### 创建新数据集

要创建新数据集，请选择 **[!UICONTROL 新建数据集]**. 在显示的表单上，提供名称、可选描述以及数据集的目标架构。 如果您选择 [!DNL Profile]-enabled架构，您可以选择数据集是否还应 [!DNL Profile]-enabled.

![new-dataset](../../../../images/tutorials/create/http/new-dataset.png)

### 使用现有数据集

要使用现有数据集，请选择 **[!UICONTROL 现有数据集]**. 在显示的表单上，选择要使用的数据集。 选择数据集后，您可以选择数据集是否应为 [!DNL Profile]-enabled.

![existing-dataset](../../../../images/tutorials/create/http/existing-dataset.png)

### 映射标准字段


根据需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以派生计算值或计算值。 有关使用映射器界面和计算字段的综合步骤，请参阅 [数据准备UI指南](../../../../../data-prep/ui/mapping.md).

要添加新源字段，请选择 **[!UICONTROL 添加新映射]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

此时将显示一个新的源字段与目标字段配对。 要添加新源字段，请选择 [!UICONTROL 选择源字段] 输入栏。

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

此 [!UICONTROL 选择属性] 面板允许您浏览文件层次结构并选择要映射到目标XDM字段的特定源字段。 选择要映射的源字段后，选择 **[!UICONTROL 选择]** 以继续。

![select-attribute](../../../../images/tutorials/create/http/select-attributes.png)

选择源字段后，您现在可以标识要映射到的适当目标XDM字段。 选择目标字段部分下的架构图标。

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

此 [!UICONTROL 将源字段映射到目标字段] 窗口，为您提供用于浏览目标数据集架构的界面。 选择与源字段匹配的目标字段，然后选择 **[!UICONTROL 选择]** 以继续。

![映射到目标字段](../../../../images/tutorials/create/http/map-to-target-field.png)

将源字段全部映射到相应的目标XDM字段后，选择 **[!UICONTROL 下一个]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## 数据流详细信息

此 **[!UICONTROL 数据流详细信息]** 步骤。 在此页面上，您可以通过提供名称和可选描述来提供已创建数据流的详细信息。

为数据流提供详细信息后，选择 **[!UICONTROL 下一个]**.

![数据流 — 详细信息](../../../../images/tutorials/create/http/dataflow-detail.png)

## 请查看

此 **[!UICONTROL 审核]** 此时会显示步骤，允许您在创建数据流之前查看其详细信息。 详细信息分为以下类别：

- **[!UICONTROL 连接]**：显示帐户名称、源平台和源名称。
- **[!UICONTROL 分配数据集和映射字段]**：显示目标数据集以及该数据集所遵循的架构。

确认详细信息正确后，选择 **[!UICONTROL 完成]**.

![审核](../../../../images/tutorials/create/http/review.png)

## 获取流端点URL

创建连接后，将显示源详细信息页面。 此页面显示新创建连接的详细信息，包括以前运行的数据流、ID和流端点URL。

![端点](../../../../images/tutorials/create/http/endpoint.png)

## 后续步骤

通过遵循本教程，您已创建一个流HTTP连接，从而能够使用流端点访问各种内容 [!DNL Data Ingestion] API。 有关在API中创建流连接的说明，请阅读 [创建流连接教程](../../../api/create/streaming/http.md).

要了解如何将数据流式传输到Platform，请阅读以下任一教程： [流式时间序列数据](../../../../../ingestion/tutorials/streaming-time-series-data.md) 或上的教程 [流记录数据](../../../../../ingestion/tutorials/streaming-record-data.md).
