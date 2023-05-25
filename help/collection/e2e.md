---
title: 数据收集端到端概述
description: 有关如何使用Adobe Experience Platform的数据收集功能将事件数据发送到Adobe Experience Cloud解决方案的简要概述。
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '2621'
ht-degree: 0%

---

# 数据收集端到端概述

Adobe Experience Platform收集您的数据并将其传输到其他Adobe产品和第三方目标。 要将应用程序中的事件数据发送到Experience Platform边缘网络，请务必了解这些核心技术，以及如何配置这些技术，以便在需要时将数据交付到所需的目的地。

本指南提供了有关如何使用Platform的数据收集功能通过Edge Network发送事件的高级教程。 具体而言，本教程将介绍在数据收集UI(以前称为Adobe Experience Platform Launch)中安装和配置Adobe Experience Platform Web SDK标记扩展的步骤。

>[!NOTE]
>
>如果您不想使用标记，还可以选择手动安装和配置SDK，但周围的步骤仍必须完成，如下所示。
>
>所有涉及数据收集UI的步骤也可以在Experience PlatformUI中执行。

## 先决条件

本教程使用数据收集UI创建架构、配置数据流和安装Web SDK。 要在UI中执行这些操作，必须至少向您授予一个Web属性的访问权限，并且您还必须获得以下权限 [资产权限](../tags/ui/administration/user-permissions.md#property-rights)：

* 开发
* 管理扩展

请参阅指南，网址为 [管理数据收集的权限](./permissions.md) 了解如何授予对资产和资产权限的访问权限。

要使用本指南中提到的各种数据收集产品，您还必须有权访问数据流，并能够创建和管理架构。 如果您需要访问其中任何一项功能，请联系您的Adobe帐户团队以帮助您获得必要的访问权限。 请注意，如果您尚未购买Adobe Experience Platform，Adobe将为您提供使用SDK所需的访问权限，而不需支付额外费用。

如果您已经拥有Platform的访问权限，则必须确保您拥有 [权限](../access-control/home.md#permissions) 启用以下类别：

* 数据建模
* 标识

请参阅 [访问控制UI概述](../access-control/ui/overview.md) 以了解如何向用户授予Platform功能的权限。

## 流程摘要

为您的网站配置数据收集的过程可概括如下：

1. [创建架构](#schema) 以确定数据在发送到边缘网络时的结构方式。
1. [创建数据流](#datastream) 以配置要将数据发送到哪些目标。
1. [安装和配置Web SDK](#sdk) 用于在网站上发生某些事件时将数据发送到数据流。

一旦能够将数据发送到Edge Network，您还可以 [配置事件转发](#event-forwarding) 您的组织拥有许可证。

## 创建架构 {#schema}

[体验数据模型(XDM)](../xdm/home.md) 是一个开源规范，以架构的形式为数据提供通用结构和定义。 换言之，XDM是一种通过Edge Network和其他Adobe Experience Cloud应用程序可操作的方式构造和格式化数据的方式。

设置数据收集操作的第一步是创建XDM架构来表示您的数据。 在本教程的后一步中，您将将要发送的数据映射到此架构的结构。

>[!NOTE]
>
>XDM架构非常可自定义。 下面列出的步骤不是过于规范化，而是专门针对Web SDK的架构要求。 在这些参数之外，您可以随意定义数据的其余结构。

在用户界面中，选择 **[!UICONTROL 架构]** 左侧导航栏中。 从这里，您可以看到以前创建的属于您组织的架构列表。 要继续，请选择 **[!UICONTROL 创建架构]**，然后选择 **[!UICONTROL XDM ExperienceEvent]** 下拉菜单中。

![架构工作区](./images/e2e/schemas.png)

出现一个对话框，提示您开始向架构添加字段组。 要使用Web SDK发送事件，您必须添加字段组 **[!UICONTROL AEP Web SDK ExperienceEvent Mixin]**. 此字段组包含由Web SDK库自动收集的数据属性的定义。

使用搜索栏缩小列表范围，以便更轻松地查找此字段组。 找到后，从列表中选择它，然后选择 **[!UICONTROL 添加字段组]**.

![架构工作区](./images/e2e/add-field-group.png)

此时将显示架构画布，显示XDM架构的树结构，包括Web SDK字段组提供的字段。

![模式结构](./images/e2e/schema-structure.png)

在树中选择要打开的根字段 **[!UICONTROL 架构属性]** 在右边栏中，您可以为架构提供名称和可选描述。

![命名架构](./images/e2e/name-schema.png)

如果要向架构添加更多字段，可以通过选择 **[!UICONTROL 添加]** 在 **[!UICONTROL 字段组]** 部分。

![添加字段组](./images/e2e/add-field-groups.png)

>[!NOTE]
>
>请参阅指南，网址为 [添加字段组](../xdm/ui/resources/schemas.md#add-field-groups) 请参阅XDM文档，以了解有关如何搜索不同的字段组以适合您的用例的详细步骤。
>
>最佳实践为计划通过Edge Network发送的数据仅添加字段。 将字段添加到架构并保存后，之后只能对架构进行添加性更改。 请参阅 [模式演化规则](../xdm/schema/composition.md#evolution) 了解更多信息。

添加所需的字段后，选择 **[!UICONTROL 保存]** 以保存架构。

![保存架构](./images/e2e/save-schema.png)

## 创建数据流 {#datastream}

数据流是一种配置，用于告知Edge Network您希望将数据发送到的位置。 具体而言，数据流指定要将数据发送到哪些Experience Cloud产品，以及您希望如何处理和存储每个产品中的数据。

>[!NOTE]
>
>如果您要使用 [事件转发](../tags/ui/event-forwarding/overview.md) （假定您的组织获得了使用相关功能的许可），则必须按照启用Adobe产品的相同方式，为数据流启用该功能。 有关此过程的详细信息，请参见 [后续部分](#event-forwarding).

选择 **[!UICONTROL 数据流]** 左侧导航栏中。 在此处，您可以从列表中选择要编辑的现有数据流，也可以通过选择创建新配置 **[!UICONTROL 新建数据流]**.

![数据流](./images/e2e/datastreams.png)

数据流的配置要求取决于要将数据发送到的产品和功能。 有关每个产品的配置选项的详细信息，请参阅 [数据流概述](../edge/datastreams/overview.md).

## 安装和配置Web SDK {#install}

创建架构和数据流后，下一步是安装和配置Platform Web SDK以开始向Edge Network发送数据。

>[!NOTE]
>
>此部分使用数据收集UI配置Web SDK标记扩展，但您也可以使用原始代码来安装和配置该扩展。 有关更多信息，请参阅以下指南：
>
>* [安装SDK](../edge/fundamentals/installing-the-sdk.md)
>* [配置SDK](../edge/fundamentals/configuring-the-sdk.md)
>
>另请注意，即使您只想使用事件转发，您仍然必须按照相关说明安装和配置SDK，然后才能在 [后续步骤](#event-forwarding).

该过程可概括如下：

1. [在标记属性上安装Adobe Experience Platform Web SDK](#install-sdk) 获取对其功能的访问权限。
1. [创建XDM对象数据元素](#data-element) 将网站上的变量映射到您之前创建的XDM架构的结构。
1. [创建规则](#rule) 告知SDK应何时向Edge Network发送数据。
1. [生成并安装库](#library) 以在您的网站上实施规则。

### 在标记属性上安装SDK {#install-sdk}

选择 **[!UICONTROL 标记]** 在左侧导航中显示标记属性的列表。 您可以根据需要选择要编辑的现有资产，也可以选择 **[!UICONTROL 新建属性]** 而是。

![资产](./images/e2e/properties.png)

如果创建新资产，请提供描述性名称并设置 [!UICONTROL Platform] 到 **[!UICONTROL Web]**. 提供Web属性的完整域，然后选择 **[!UICONTROL 保存]**.

![创建属性](./images/e2e/create-property.png)

此时将显示该资产的概述页面。 从此处选择 **[!UICONTROL 扩展]** 在左侧导航中，然后选择 **[!UICONTROL 目录]**. 查找Platform Web SDK的列表（可以选择使用搜索栏缩小结果范围）并选择 **[!UICONTROL 安装]**.

![安装Web SDK](./images/e2e/install-sdk.png)

此时将显示SDK的配置页面。 大多数必需值都会自动填充默认值，您可以根据需要更改这些默认值。

![配置 Web SDK](./images/e2e/configure-sdk.png)

但是，在安装SDK之前，您必须选择一个数据流，以便它知道要将您的数据发送到何处。 下 **[!UICONTROL 数据流]**，使用下拉菜单选择您在上配置的数据流 [更早的步骤](#datastream). 设置数据流后，选择 **[!UICONTROL 保存]** 以完成将SDK安装到资产。

![设置数据流并保存](./images/e2e/set-datastream.png)

### 创建XDM数据元素 {#data-element}

为了使SDK将数据发送到Edge Network，该数据必须映射到您在中创建的XDM架构 [上一步](#schema). 此映射通过使用数据元素来完成。

在用户界面中，选择 **[!UICONTROL 数据元素]**，然后选择 **[!UICONTROL 创建新数据元素]**.

![创建新数据元素](./images/e2e/data-elements.png)

在下一个屏幕上，选择 **[!UICONTROL Adobe Experience Platform Web SDK]** 在 [!UICONTROL 扩展] 下拉列表，然后选择 **[!UICONTROL XDM对象]** （数据元素类型）。

![XDM对象类型](./images/e2e/xdm-object.png)

此时将显示用于XDM对象类型的配置对话框。 该对话框会自动选择您的Platform沙盒，从这里您可以看到在该沙盒中创建的所有架构。 从列表中选择您之前创建的XDM架构。

![XDM对象类型](./images/e2e/select-schema.png)

此时将显示架构的结构。 所有带星号(**\***)指示在事件触发时将自动填充的字段。 对于所有其他字段，您可以浏览架构的结构并填写其余数据。

![将数据映射到XDM字段](./images/e2e/map-schema.png)

>[!NOTE]
>
>上面的屏幕快照演示了如何从网站的客户端(`cartAbandonsTotal`)到XDM字段，方法是在 [!UICONTROL 值] 字段，由百分比符号(`%`)。
>
>您还可以使用其他以前创建的数据元素来填充这些字段。 请参阅参考资料： [数据元素](../tags/ui/managing-resources/data-elements.md) 有关更多信息，请参阅标记文档。

完成将数据映射到架构后，请先提供数据元素的名称，然后再选择 **[!UICONTROL 保存]**.

![命名并保存数据元素](./images/e2e/name-and-save.png)

### 创建规则

保存数据元素后，下一步是创建一个规则，每当网站上发生特定事件（例如，当客户将产品添加到购物车时）时，该规则会将其发送到Edge Network。

您可以为网站上发生的几乎任何事件设置规则。 例如，此部分说明如何创建将在客户提交表单时触发的规则。 以下HTML表示一个具有“添加到购物车”表单的简单网页，该表单将是规则的主题：

```html
<!DOCTYPE html>
<html>
<body>

  <form id="add-to-cart-form">
    <label for="item">Product:</label><br>
    <input type="text" id="item" name="item"><br>
    <label for="amount">Amount:</label><br>
    <input type="number" id="amount" name="amount" value="1"><br><br>
    <input type="submit" value="Add to Cart">
  </form> 

</body>
</html>
```

在数据收集UI中，选择 **[!UICONTROL 规则]** 在左侧导航中，然后选择 **[!UICONTROL 创建新规则]**.

![规则](./images/e2e/rules.png)

在下一个屏幕上，提供规则的名称。 从此处开始，下一步是确定规则的事件（换句话说，规则将触发的时间）。 选择 **[!UICONTROL 添加]** 下 [!UICONTROL 事件].

![名称规则](./images/e2e/name-rule.png)

此时将显示事件配置页面。 要配置事件，必须首先选择事件类型。 事件类型由扩展提供。 例如，要设置“表单提交”事件，请选择 **[!UICONTROL 核心]** 扩展，然后选择 **[!UICONTROL 提交]** 事件类型位于 **[!UICONTROL 表单]** 类别。

>[!NOTE]
>
>有关AdobeWeb扩展提供的各种事件类型（包括如何配置它们）的更多信息，请参阅 [Adobe扩展参考](../tags/extensions/client/overview.md) 标记文档中的。

表单提交事件允许您使用 [CSS选择器](https://www.w3schools.com/css/css_selectors.asp) 以引用规则要触发的特定元素。 在以下示例中，ID `add-to-cart-form` 使用此规则，以便该规则仅在“添加到购物车”表单中触发。 选择 **[!UICONTROL 保留更改]** 以将事件添加到规则。

![事件配置](./images/e2e/event-config.png)

此时会重新显示规则配置页面，指示事件已添加。 您可以缩小&quot;[!UICONTROL 如果]”，向规则添加更多条件。

否则，下一步是添加一个操作，以便规则在触发时执行。 选择 **[!UICONTROL 添加]** 下 **[!UICONTROL 操作]** 以继续。

![添加操作](./images/e2e/add-action.png)

此时将显示操作配置页面。 要获取将数据发送到边缘网络的规则，请选择 **[!UICONTROL Adobe Experience Platform Web SDK]** 对于扩展，以及 **[!UICONTROL 发送事件]** 操作类型对应的。

![操作类型](./images/e2e/action-type.png)

屏幕将更新，以显示用于配置send event操作的其他选项。 下 **[!UICONTROL 类型]**，则可以提供自定义类型值来填充 `eventType` XDM字段。 下 **[!UICONTROL XDM数据]**，提供您之前创建的XDM数据类型的名称（由百分比符号括起来），或选择数据库图标(![“数据库”图标](./images/e2e/database-symbol.png))，以从列表中选择它。 最终将发送到边缘网络的数据。

选择 **[!UICONTROL 保留更改]** 完成后。

![操作配置](./images/e2e/action-config.png)

配置完规则后，选择 **[!UICONTROL 保存]** 完成该过程。

![保存规则](./images/e2e/save-rule.png)

### 生成并安装库 {#library}

配置规则后，便可以将其添加到标记库，将该库构建到环境，并在您的网站上安装该版本。

>[!NOTE]
>
>如果尚未在数据收集UI中设置环境，则必须先设置环境，然后才能创建内部版本。 请参阅以下部分： [为Web属性配置环境](../tags/ui/publishing/environments.md#web-configuration) 有关更多信息，请参阅标记文档。

要了解如何创建库、将扩展和规则添加到库以及将库生成到环境，请参阅以下指南中的内容： [管理库](../tags/ui/publishing/libraries.md) 标记文档中的。 创建库时，请确保包含Platform Web SDK扩展和您之前创建的数据收集规则。

创建库并将其内部版本分配给环境后，便可以在网站的客户端上安装该环境。 请参阅以下部分： [安装环境](../tags/ui/publishing/environments.md#installation) 了解更多信息。

在网站上安装环境后，您可以 [测试实施](../tags/ui/publishing/embed-code-testing.md) 使用Adobe Experience Platform Debugger。

## 配置事件转发（可选） {#event-forwarding}

>[!NOTE]
>
>事件转发仅适用于已获得相应许可的组织。

在将SDK配置为将数据发送到边缘网络后，可以设置事件转发以告知边缘网络您希望将数据发送到何处。

要使用事件转发，必须首先创建事件转发属性。 选择 **[!UICONTROL 事件转发]** 然后，在左侧导航中选择 **[!UICONTROL 新建属性]**. 在选择之前提供属性的名称 **[!UICONTROL 保存]**.

创建事件转发属性后，下一步是创建一个规则以确定应将数据发送到何处。 事件转发属性的规则构建方式与标记属性大致相同，但可以指定任何事件（因为事件转发仅处理直接从数据流接收的事件）。 对于规则的操作，您可以使用某个可用的事件转发扩展，也可以使用自定义代码来交付事件。

![事件转发规则](./images/e2e/event-forwarding-rule.png)

与之前类似，配置规则后，必须将其添加到库并将该库构建到环境。

构建完成后，最后一步是更新您的数据流 [先前配置](#datastream) 并启用事件转发。 要开始，请导航到 **[!UICONTROL 数据流]** 并从列表中选择相关的数据流。 从此处，启用事件转发的切换开关，并提供刚刚配置的属性和环境的名称。

![事件转发数据流](./images/e2e/event-forwarding-datastream.png)

## 后续步骤

本指南提供了有关如何使用Platform Web SDK向Edge Network发送数据的高级端到端概述。 请参阅本指南中链接的文档，了解涉及的各种组件和服务的更多信息。
