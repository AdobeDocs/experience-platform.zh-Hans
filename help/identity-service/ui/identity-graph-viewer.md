---
keywords: Experience Platform；主页；热门主题；标识图查看器；标识图查看器；图形查看器；标识命名空间；标识命名空间；标识；标识；标识服务；标识服务
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: tutorial
description: 标识图是特定客户不同标识之间关系的映射，可直观地展示客户如何跨不同渠道与品牌互动。
translation-type: tm+mt
source-git-commit: 7c9c81492df9333945ac62602f10b6097296d62b
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 1%

---


# （测试版）标识图查看器

>[!NOTE]
>
>标识图查看器当前处于测试版中。 其功能可能会发生变化。

标识图是特定客户不同标识之间关系的映射，可直观地展示客户如何跨不同渠道与品牌互动。 所有客户身份图均由Adobe Experience Platform身份服务以响应客户活动的方式近期实时进行集体管理和更新。

通过平台用户界面中的标识图查看器，您可以直观地了解哪些客户标识是拼接在一起的，以及以哪些方式拼接在一起。 查看器允许您拖动图形的不同部分并与之交互，从而检查复杂的身份关系、更高效地调试并从信息利用方式提高的透明度中受益。

## 入门指南

使用标识图查看器需要了解涉及的各种Adobe Experience Platform服务。 在开始使用标识图查看器之前，请查看以下服务的相关文档：

- [[!DNL Identity Service]](../home.md):通过跨设备和系统桥接身份，更好地视图个别客户及其行为。

### 术语

- **标识（节点）:** 标识或节点是实体（通常是人）特有的数据。标识由命名空间和标识值组成。
- **链接（边）：链** 接或边表示标识之间的连接。
- **图（群集）:** 图或群集是一组代表人的身份和链接。

## 访问标识图查看器

要在UI中使用标识图查看器，请在左侧导航中选择&#x200B;**[!UICONTROL 标识]**，然后选择&#x200B;**[!UICONTROL 标识图]**&#x200B;选项卡。 在&#x200B;**[!UICONTROL 标识命名空间]**&#x200B;屏幕中，单击&#x200B;**[!UICONTROL 选择标识命名空间]**&#x200B;图标以搜索要使用的命名空间。

![命名空间屏](../images/identity-graph-viewer/identity-namespace.png)

出现&#x200B;**[!UICONTROL 选择标识命名空间]**&#x200B;面板。 此屏幕包含可供您的组织使用的列表，包括有关命名空间的&#x200B;**[!UICONTROL 显示名称]**、**[!UICONTROL 标识符]**、**[!UICONTROL 所有者]**、**[!UICONTROL 上次更新日期]**&#x200B;和&#x200B;**[!UICONTROL 说明]**&#x200B;的信息。 只要您有有效的标识值连接到它们，就可以使用提供的任何命名空间。

选择要使用的命名空间，然后单击&#x200B;**[!UICONTROL 选择]**&#x200B;以继续。

![select-identity-命名空间](../images/identity-graph-viewer/select-identity-namespace.png)

选择命名空间后，在&#x200B;**[!UICONTROL 标识值]**&#x200B;文本框中为特定客户输入其相应值，然后选择&#x200B;**[!UICONTROL 视图]**。

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

将显示标识图查看器。 屏幕左侧是标识图，显示与您选择的命名空间链接的所有标识以及您输入的标识值。 每个标识节点都包含一个命名空间及其对应的ID值。 您可以选择并保留任何标识以拖动图形并与其交互。 或者，您也可以将鼠标悬停在某个标识上，以查看有关其ID值的信息。 图形输出也以表格列表显示在屏幕的中央。

>[!IMPORTANT]
>
>身份图需要至少两个链接身份才能生成，以及有效的命名空间和ID对。 图形查看器可显示的最大身份数为150。 有关详细信息，请参见下面的[附录](#appendix)部分。

![身份图](../images/identity-graph-viewer/graph-viewer.png)

选择标识以更新&#x200B;**[!UICONTROL Identities]**&#x200B;表上突出显示的行并更新右边栏上提供的信息，该信息包括标识的&#x200B;**[!UICONTROL 值]**、**[!UICONTROL 批ID]**&#x200B;及其&#x200B;**[!UICONTROL 上次更新的]**&#x200B;日期。

![select-identity](../images/identity-graph-viewer/select-identity.png)

您可以在图形中进行过滤，并使用&#x200B;**[!UICONTROL Identities]**&#x200B;表顶部的排序选项隔离特定命名空间。 从下拉菜单中，选择要突出显示的命名空间。

![逐命名空间](../images/identity-graph-viewer/filter-namespace.png)

图形查看器返回，突出显示您选择的命名空间。 过滤器选项还更新&#x200B;**[!UICONTROL 标识]**&#x200B;表，以仅返回所选命名空间的信息。

![已过滤](../images/identity-graph-viewer/filtered.png)

图形查看器框的右上方包含放大选项。 选择&#x200B;**(+)**&#x200B;图标以放大图形，或选择&#x200B;**(-)**&#x200B;图标以缩小图形。

![缩放](../images/identity-graph-viewer/zoom.png)

您可以通过从标题中选择&#x200B;**[!UICONTROL 数据源]**&#x200B;来视图有关批的详细信息。 **[!UICONTROL 数据源]**&#x200B;表显示与图形关联的&#x200B;**[!UICONTROL 批ID]**&#x200B;的列表，以及其&#x200B;**[!UICONTROL 链接ID]**、源模式和摄取日期。

![数据源](../images/identity-graph-viewer/data-source-table.png)

您可以选择标识图中的任何链接，以查看贡献到该链接的所有源批。

![select-links](../images/identity-graph-viewer/select-edge.png)

或者，您可以选择一个批来查看此批贡献的所有链接。

![select-links](../images/identity-graph-viewer/select-batch.png)

通过标识图查看器也可以访问具有较大标识簇的标识图。

![大集群](../images/identity-graph-viewer/large-cluster.png)

## 附录

以下部分提供了有关使用标识图查看器的其他信息。

### 了解错误消息

访问标识图查看器时可能会出错。 以下是使用标识图查看器时要注意的先决条件和限制列表。

- 选定命名空间中必须存在标识值。
- 要生成标识图查看器，至少需要两个链接标识。
- 标识图查看器不能超过150个标识。

![错误屏幕](../images/identity-graph-viewer/error-screen.png)

## 后续步骤

通过阅读此文档，您学习了如何在平台UI中浏览客户的身份图。 有关平台中身份的详细信息，请参阅[Identity Service概述](../home.md)