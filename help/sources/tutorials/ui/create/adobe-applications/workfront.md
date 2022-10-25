---
keywords: Experience Platform；主页；热门主题；
title: （测试版）在UI中创建Adobe Workfront源连接
description: 本教程提供了创建Adobe Workfront源连接以使用用户界面将Workfront数据引入Adobe Experience Platform的步骤。
source-git-commit: 1af0863766e29c599e02f2a553d237bc62f455d2
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# （测试版）在UI中创建Adobe Workfront源连接

>[!NOTE]
>
>Adobe Workfront源是测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

本教程提供了创建Adobe Workfront源连接以使用用户界面将Workfront数据引入Adobe Experience Platform的步骤。

## 快速入门

>[!IMPORTANT]
>
>您必须在Adobe Admin Console中配置为管理员才能访问Workfront源。

本教程需要对Experience Platform的以下组件有一定的了解：

* [Experience Data Model(XDM)系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [实时客户资料](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 在UI中创建Workfront源连接

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕显示可用于创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 您还可以使用搜索栏来缩小显示的源范围。

在 **[!UICONTROL Adobe应用程序]** 类别，选择 **[!UICONTROL Adobe Workfront]** 然后选择 **[!UICONTROL 添加数据]**.

![突出显示Adobe Workfront源的源目录。](../../../../images/tutorials/create/workfront/catalog.png)

## 选择数据

的 [!UICONTROL 选择数据] 中。 在此，必须为Workfront子域和Datalane提供值。 您的Workfront子域是用于访问Workfront实例的相同URL，例如 `https://acme.workfront.com/`，而datalane则表示您要使用的workfront环境。

添加子域和数据栏后，选择 **[!UICONTROL 下一个]**.

![包含子域和数据栏占位符值的“选择数据”页。](../../../../images/tutorials/create/workfront/select-data.png)

## 提供数据流详细信息

数据流详细信息步骤允许您为数据流提供名称和可选描述。 在此步骤中，您还可以订阅警报以接收有关数据流状态的通知。 有关警报的更多信息，请访问 [在源UI中订阅警报](../../alerts.md).

提供数据流详细信息并配置所需的警报设置后，请选择 **[!UICONTROL 下一个]**.

![数据流详细信息页，其中包含有关数据流名称、描述和警报通知的信息](../../../../images/tutorials/create/workfront/dataflow-detail.png)

## 审阅

的 **[!UICONTROL 审阅]** 步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **[!UICONTROL 分配数据集和映射字段]**:显示源数据被摄取到的数据集，包括该数据集附加的架构。

审核数据流后，选择 **[!UICONTROL 完成]** 并为创建数据流留出一些时间。

![概述连接信息的审核页面。](../../../../images/tutorials/create/workfront/review.png)

## 附录

以下各节提供了有关Workfront源的其他信息。

### Workfront更改事件架构

Platform中的Workfront数据表示为时间系列记录数据，其中数据的每一行都有一个时间戳，显示事件发生的时间以及与该事件相关的属性。

在设置过程中，会创建一个名为“从流中更改事件”的Workfront架构。

| 架构字段 | 描述 |
| --- | --- |
| `timestamp` | 选定事件发生的时间。 时间戳以GTM时区表示。 |
| `_workfront.objectType` | 对象类型。 可用值可以包括 `project`, `task`, `portfolio`、和其他对象，具体取决于已更改或创建的对象。 |
| `_workfront.objectID` | 与对象类型对应的ID。 |
| `_workfront.created` | 此值设置为 `1` 如果事件表示对象创建。 |
| `_workfront.deleted` | 此值设置为 `1` 如果删除了对象。 |
| `_worfkront.updated` | 此值设置为 `1` 如果对象已更新。 |
| `_workfront.completed` | 此值设置为 `1` 对象标记为已完成。 |
| `_workfront.parentObjectType` | （可选）与对象的父级对应的对象类型。 |
| `_workfront.parentID` | 父对象的ID。 |
| `_workfront.customData` | 事件期间填充的所有自定义表单字段和值的映射。 |

>[!IMPORTANT]
>
>只会填充已更改或已作为事件的一部分创建的属性。 例如，如果只更改对象的名称，则将填充的字段仅包括：<ul><li>`timestamp`</li><li>`_workfront.update (=1)`</li><li>`_workfront.objectType`</li><li>`_workfront.objectID`</li><li>`_workfront.objectName`</li></ul>

## 后续步骤

在本教程之后，您现在已创建了一个数据流，用于将数据从WorkfrontExperience Platform到数据。 您现在可以使用 [查询服务](../../../../../query-service/home.md) 以进一步分析您的数据。 有关Workfront的更多信息，请阅读 [Workfront概述](../../../../connectors/adobe-applications/workfront.md).