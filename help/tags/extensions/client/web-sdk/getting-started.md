---
title: Web SDK标记扩展快速入门
description: 使用Web SDK标记扩展将事件数据发送到Adobe Experience Platform Edge Network。
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 3%

---

# Web SDK标记扩展快速入门

使用Adobe Experience Platform的&#x200B;**标记**（以前为Launch）将事件数据从您的网站发送到Edge Network和下游Adobe解决方案。

在执行以下步骤之前，请确保您可以访问以下[属性权限](/help/tags/ui/administration/user-permissions.md)：

* [!UICONTROL Develop]
* [!UICONTROL Manage extensions]

此外，请确保您拥有以下类别的所有[权限](/help/access-control/home.md#permissions)：

* 数据建模
* 身份标识

## 创建 XDM 架构 {#schema}

[体验数据模型(XDM)](/help/xdm/home.md)是一个开源规范，以架构的形式为数据提供通用结构和定义。 在向Edge Network发送数据时，强烈建议配置架构。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Schemas]**。
1. 选择 **[!UICONTROL Create schema]**。
1. 选择&#x200B;**[!UICONTROL Experience Event]**，然后选择&#x200B;**[!UICONTROL Next]**。
1. 为架构指定所需的名称，然后选择&#x200B;**[!UICONTROL Finish]**。
1. （可选）您可以为要收集的任何其他数据添加更多字段或[字段组](/help/xdm/ui/resources/field-groups.md)。

![架构画布](assets/getting-started/schema-structure.png)

>[!NOTE]
>\
>保存后，架构仅允许&#x200B;*累加*&#x200B;更改。 有关详细信息，请参阅[架构演变](/help/xdm/schema/composition.md#evolution)。

## 创建数据流 {#datastream}

[数据流](/help/datastreams/overview.md)是一种配置，用于告知Edge Network如何处理您向其发送的数据。 当您将数据流配置为将数据发送到给定产品时，数据流会以特定产品所理解的方式自动将相关数据传递到每个相应的产品。

1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**。
1. 选择 **[!UICONTROL New datastream]**。
1. 为数据流指定所需的名称，并在&#x200B;**[!UICONTROL Mapping schema]**&#x200B;下选择最近创建的架构。
1. 选择 **[!UICONTROL Save]**。

![数据流列表](assets/getting-started/datastreams.png)

## 创建标记属性

创建架构和数据流后，即可创建和配置标记属性。

1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择 **[!UICONTROL New property]**。
1. 为标记属性指定所需的名称和域，然后选择&#x200B;**[!UICONTROL Save]**。

## 安装标记扩展

Web SDK标记扩展安装在给定的标记属性上。

1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]** > **[!UICONTROL Extensions]**。
1. 选择 **[!UICONTROL Catalog]** 选项卡。
1. 使用搜索功能查找&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;扩展。
1. 选择扩展卡片，然后选择右侧的&#x200B;**[!UICONTROL Install]**。

![安装SDK](assets/getting-started/install-sdk.png)

## 配置标记扩展

安装Web SDK标记扩展时，您会自动转到[配置](configure/config-overview.md)页面。

1. 在[数据流部分](configure/datastreams.md)下，为每个环境选择所需的数据流。

所有其他配置设置均由您填写或可选。 设置任何所需的配置设置，然后选择&#x200B;**[!UICONTROL Save]**。

## 创建变量数据元素

Adobe建议使用[变量](data-element-types.md#variable)数据元素来存储要发送到Adobe的有效负载。 XDM对象也是可用的数据元素，但在适用的用例中较旧，并且更有限。

1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 选择&#x200B;**[!UICONTROL Data elements]** > **[!UICONTROL Create new data element]**。
1. 在左侧为数据元素指定以下属性：
   * **[!UICONTROL Name]**：任何所需的名称
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Data element type]**: [!UICONTROL Variable]
1. 在右侧设置以下属性：
   **变量类型**： XDM
   **[!UICONTROL Sandbox]**：您在其中创建架构的沙盒
   **[!UICONTROL Schema]**：所需的架构
1. 选择 **[!UICONTROL Save]**。

## 创建规则

规则决定您何时要触发某些操作或设置变量。 通过创建在加载库时运行的规则，您可以轻松填充要在每个页面上包含值的变量。

1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 选择&#x200B;**[!UICONTROL Rules]** > **[!UICONTROL Add rule]**。
1. 为规则指定所需的名称。
1. 选择`+`旁边的“**[!UICONTROL Events]**”图标。
1. 为事件指定以下设置：
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL Event type]**: [!UICONTROL Library loaded (page top)]
1. 选择 **[!UICONTROL Keep changes]**。

上述步骤建立了规则的标准部分，该部分将在库加载后触发。 以下步骤确定在满足该标准时应采取的操作。

1. 选择`+`旁边的“**[!UICONTROL Actions]**”图标。
1. 在左侧为操作指定以下设置：
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Send event]
1. 在右侧设置以下字段：
   * **[!UICONTROL XDM]**： XDM变量数据元素
1. 选择 **[!UICONTROL Keep changes]**。

![操作配置](assets/getting-started/action-config.png)

## 发布

tag属性包含将数据发送到Edge Network所需的所有组件。

1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Publishing flow]**。
1. 选择 **[!UICONTROL Add library]**。
1. 为库指定所需的名称。 在版本控制软件中工作时，请考虑此名称与提交名称类似。
1. 将环境下拉菜单设置为&#x200B;**[!UICONTROL Development]**。
1. 选择 **[!UICONTROL Add all changed resources]**。
1. 选择 **[!UICONTROL Save & build to Development]**。

现在，您的更改将部署到开发环境。

1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Environments]**。
1. 选择开发环境旁边的安装图标
1. 在网站的测试网页中安装嵌入代码。

验证标记是否适用于开发环境后，您可以使用[!UICONTROL Publishing flow]界面将库发布到暂存环境，然后最终发布到生产环境。

1. 将扩展和规则添加到&#x200B;**库**，将其构建到&#x200B;**环境**，并在您的网站上安装嵌入代码。
2. 使用&#x200B;**Adobe Experience Platform Debugger**&#x200B;进行验证。

您现在有一个精简设置，用于捕获事件并将它们发送到Edge Network。 您现在可以通过以下方式进一步构建实施：将字段添加到架构、将产品添加到数据流或将数据元素添加到标记属性。
