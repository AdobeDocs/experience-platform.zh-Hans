---
title: 数据收集端到端概述
description: 简要概述如何使用Adobe Experience Platform的数据收集功能将事件数据发送到Adobe Experience Cloud解决方案。
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '2621'
ht-degree: 0%

---

# 数据收集端到端概述

Adobe Experience Platform会收集您的数据并将其传输到其他Adobe产品和第三方目标。 要将事件数据从您的应用程序发送到Experience Platform边缘网络，请务必了解这些核心技术以及如何配置这些技术以在需要时将数据交付到所需目标。

本指南提供了有关如何使用Platform的数据收集功能通过边缘网络发送事件的高级教程。 具体而言，本教程将指导您完成在数据收集UI(以前称为Adobe Experience Platform)中安装和配置Adobe Experience Platform Launch Web SDK标记扩展的步骤。

>[!NOTE]
>
>如果您不想使用标记，也可以选择手动安装和配置SDK，但周边步骤仍必须完成，如下所述。
>
>还可以在Experience PlatformUI中执行涉及数据收集UI的所有步骤。

## 先决条件

本教程使用数据收集UI创建模式、配置数据流并安装Web SDK。 要在UI中执行这些操作，必须向您授予至少一个Web属性的访问权限，以及以下内容 [资产权限](../tags/ui/administration/user-permissions.md#property-rights):

* 开发
* 管理扩展

请参阅 [管理数据收集的权限](./permissions.md) 了解如何授予对资产和资产权限的访问权限。

要使用本指南中提到的各种数据收集产品，您还必须拥有数据流的访问权限以及创建和管理架构的功能。 如果您需要访问其中任一功能，请联系您的Adobe帐户团队以帮助您获得必要的访问权限。 请注意，如果您尚未购买Adobe Experience Platform,Adobe将为您配置使用SDK的必要访问权限，而无需支付额外费用。

如果您已经拥有平台的访问权限，则必须确保您拥有 [权限](../access-control/home.md#permissions) 在启用的以下类别下：

* 数据建模
* 标识

请参阅 [访问控制UI概述](../access-control/ui/overview.md) 了解如何向用户授予Platform功能的权限。

## 流程摘要

为网站配置数据收集的过程可概括如下：

1. [创建架构](#schema) 以确定在发送到边缘网络时数据的结构。
1. [创建数据流](#datastream) 配置您希望将数据发送到的目标。
1. [安装和配置Web SDK](#sdk) 用于在您的网站上发生某些事件时向数据流发送数据。

在能够将数据发送到边缘网络后，您还可以选择 [配置事件转发](#event-forwarding) 贵组织是否拥有许可证。

## 创建架构 {#schema}

[体验数据模型(XDM)](../xdm/home.md) 是一种开源规范，它以模式形式为数据提供通用结构和定义。 换句话说，XDM是一种数据结构和格式化数据的方式，其方式可由Edge Network和其他Adobe Experience Cloud应用程序使用。

设置数据收集操作的第一步是创建一个XDM架构来表示您的数据。 在本教程的后续步骤中，您会将要发送的数据映射到此架构的结构。

>[!NOTE]
>
>XDM模式是可以非常自定义的。 下面概述的步骤不是过于明确，而是专门针对Web SDK的架构要求。 在这些参数之外，您可以根据需要定义数据的其余结构。

在UI中，选择 **[!UICONTROL 模式]** 中。 从此处，您可以看到属于贵组织的先前创建的架构列表。 要继续，请选择 **[!UICONTROL 创建架构]**，然后选择 **[!UICONTROL XDM ExperienceEvent]** 下拉菜单中。

![模式工作区](./images/e2e/schemas.png)

出现一个对话框，提示您开始向架构添加字段组。 要使用Web SDK发送事件，您必须添加字段组 **[!UICONTROL AEP Web SDK ExperienceEvent Mixin]**. 此字段组包含由Web SDK库自动收集的数据属性的定义。

使用搜索栏缩小列表以帮助更轻松地查找此字段组。 找到它后，从列表中选择它，然后选择 **[!UICONTROL 添加字段组]**.

![模式工作区](./images/e2e/add-field-group.png)

此时会显示架构画布，其中显示了XDM架构的树结构，包括Web SDK字段组提供的字段。

![模式结构](./images/e2e/schema-structure.png)

选择树中要打开的根字段 **[!UICONTROL 架构属性]** 在右边栏中，您可以为架构提供名称和可选描述。

![命名架构](./images/e2e/name-schema.png)

如果要向架构添加更多字段，可通过选择 **[!UICONTROL 添加]** 下 **[!UICONTROL 字段组]** 区域。

![添加字段组](./images/e2e/add-field-groups.png)

>[!NOTE]
>
>请参阅 [添加字段组](../xdm/ui/resources/schemas.md#add-field-groups) ，以了解有关如何根据用例搜索不同字段组的详细步骤。
>
>最佳做法是仅为您计划通过边缘网络发送的数据添加字段。 将字段添加到架构并保存该架构后，以后只能对架构进行附加更改。 请参阅 [模式演化规则](../xdm/schema/composition.md#evolution) 以了解更多信息。

添加所需字段后，选择 **[!UICONTROL 保存]** 以保存架构。

![保存架构](./images/e2e/save-schema.png)

## 创建数据流 {#datastream}

数据流是一种配置，用于告知边缘网络您希望将数据发送到的位置。 具体而言，数据流指定要将数据发送到的Experience Cloud产品，以及希望如何处理数据并将其存储在每个产品中。

>[!NOTE]
>
>如果您想使用 [事件转发](../tags/ui/event-forwarding/overview.md) （假定贵组织已获得该功能的许可），则必须为数据流启用该功能，其方式与启用Adobe产品相同。 有关此过程的详细信息，请参阅 [稍后部分](#event-forwarding).

选择 **[!UICONTROL 数据流]** 中。 在此，您可以从列表中选择要编辑的现有数据流，也可以通过选择 **[!UICONTROL 新数据流]**.

![数据流](./images/e2e/datastreams.png)

数据流的配置要求取决于您将数据发送到的产品和功能。 有关每个产品的配置选项的详细信息，请参阅 [数据流概述](../edge/datastreams/overview.md).

## 安装和配置Web SDK {#install}

创建架构和数据流后，下一步是安装和配置Platform Web SDK以开始向边缘网络发送数据。

>[!NOTE]
>
>此部分使用数据收集UI配置Web SDK标记扩展，但您也可以改用原始代码安装和配置它。 有关更多信息，请参阅以下指南：
>
>* [安装SDK](../edge/fundamentals/installing-the-sdk.md)
>* [配置SDK](../edge/fundamentals/configuring-the-sdk.md)
>
>另请注意，即使您只想使用事件转发，您仍必须按照所述安装和配置SDK，然后才能在 [后续步骤](#event-forwarding).

该过程可概括如下：

1. [在标记属性上安装Adobe Experience Platform Web SDK](#install-sdk) 以获取其功能。
1. [创建XDM对象数据元素](#data-element) 将网站上的变量映射到您之前创建的XDM架构的结构。
1. [创建规则](#rule) 告知SDK何时应将数据发送到边缘网络。
1. [构建和安装库](#library) 以在您的网站上实施规则。

### 在标记资产上安装SDK {#install-sdk}

选择 **[!UICONTROL 标记]** 在左侧导航中显示标记属性列表。 您可以根据需要选择要编辑的现有属性，也可以选择 **[!UICONTROL 新建资产]** 中。

![资产](./images/e2e/properties.png)

如果创建新属性，请提供描述性名称并设置 [!UICONTROL 平台] to **[!UICONTROL Web]**. 为Web属性提供完整域，然后选择 **[!UICONTROL 保存]**.

![创建属性](./images/e2e/create-property.png)

此时会显示资产的概述页面。 从此处选择 **[!UICONTROL 扩展]** 在左侧导航中，选择 **[!UICONTROL 目录]**. 查找Platform Web SDK的列表（可选地使用搜索栏缩小结果范围）并选择 **[!UICONTROL 安装]**.

![安装Web SDK](./images/e2e/install-sdk.png)

此时会显示SDK的配置页面。 大多数必需值会自动填充默认值，您可以根据需要选择更改这些默认值。

![配置 Web SDK](./images/e2e/configure-sdk.png)

但是，在安装SDK之前，您必须选择一个数据流，以便它知道要将数据发送到的位置。 在 **[!UICONTROL 数据流]**，使用下拉菜单选择您在 [早期步骤](#datastream). 设置数据流后，选择 **[!UICONTROL 保存]** 完成将SDK安装到资产。

![设置数据流并保存](./images/e2e/set-datastream.png)

### 创建XDM数据元素 {#data-element}

为了使SDK将数据发送到边缘网络，该数据必须映射到您在 [上一步](#schema). 此映射是通过使用数据元素来完成的。

在UI中，选择 **[!UICONTROL 数据元素]**，然后选择 **[!UICONTROL 创建新数据元素]**.

![创建新数据元素](./images/e2e/data-elements.png)

在下一个屏幕上，选择 **[!UICONTROL Adobe Experience Platform Web SDK]** 下 [!UICONTROL 扩展] 下拉列表，然后选择 **[!UICONTROL XDM对象]** （对于数据元素类型）。

![XDM对象类型](./images/e2e/xdm-object.png)

将出现XDM对象类型的配置对话框。 该对话框会自动选择您的平台沙箱，从此处，您可以看到在该沙箱中创建的所有架构。 从列表中选择之前创建的XDM架构。

![XDM对象类型](./images/e2e/select-schema.png)

此时会显示架构的结构。 带星号(**\***)指示在事件触发时自动填充的字段。 对于所有其他字段，您可以浏览架构的结构并填写其余数据。

![将数据映射到XDM字段](./images/e2e/map-schema.png)

>[!NOTE]
>
>上面的屏幕截图演示了如何从网站的客户端映射可全局访问的变量(`cartAbandonsTotal`)，并在 [!UICONTROL 值] 字段，周围是百分号(`%`)。
>
>您还可以使用之前创建的其他数据元素来填充这些字段。 请参阅 [数据元素](../tags/ui/managing-resources/data-elements.md) （位于标记文档中）以了解更多信息。

完成将数据映射到架构后，请在选择 **[!UICONTROL 保存]**.

![命名并保存数据元素](./images/e2e/name-and-save.png)

### 创建规则

保存数据元素后，下一步是创建一个规则，当您的网站上发生特定事件时（例如，客户将产品添加到购物车时），该规则会将其发送到边缘网络。

您几乎可以为网站上可能发生的任何事件设置规则。 例如，本节将演示如何创建将在客户提交表单时触发的规则。 以下HTML表示一个包含“添加到购物车”表单的简单网页，该网页将成为规则的主题：

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

在数据收集UI中，选择 **[!UICONTROL 规则]** 在左侧导航中，选择 **[!UICONTROL 创建新规则]**.

![规则](./images/e2e/rules.png)

在下一个屏幕中，提供规则的名称。 从此处，下一步是确定规则的事件（即规则何时触发）。 选择 **[!UICONTROL 添加]** 在 [!UICONTROL 事件].

![名称规则](./images/e2e/name-rule.png)

将显示事件配置页面。 要配置事件，必须先选择事件类型。 事件类型由扩展提供。 例如，要设置“表单提交”事件，请选择 **[!UICONTROL 核心]** 扩展，然后选择 **[!UICONTROL 提交]** 事件类型位于 **[!UICONTROL 表单]** 类别。

>[!NOTE]
>
>有关AdobeWeb扩展提供的不同事件类型（包括如何配置事件类型）的更多信息，请参阅 [Adobe扩展参考](../tags/extensions/client/overview.md) （位于标记文档中）。

表单提交事件允许您使用 [CSS选择器](https://www.w3schools.com/css/css_selectors.asp) 引用规则要触发的特定元素。 在以下示例中，ID `add-to-cart-form` ，以便此规则仅针对“添加到购物车”表单触发。 选择 **[!UICONTROL 保留更改]** 将事件添加到规则。

![事件配置](./images/e2e/event-config.png)

此时将重新显示规则配置页面，其中显示已添加事件。 您可以缩小“[!UICONTROL 如果]“ ”来添加其他条件。

否则，下一步是为规则添加一个在触发时要执行的操作。 选择 **[!UICONTROL 添加]** 在 **[!UICONTROL 操作]** 继续。

![添加操作](./images/e2e/add-action.png)

此时将显示操作配置页面。 要获取将数据发送到边缘网络的规则，请选择 **[!UICONTROL Adobe Experience Platform Web SDK]** 对于扩展，和 **[!UICONTROL 发送事件]** （对于操作类型）。

![操作类型](./images/e2e/action-type.png)

屏幕会更新，以显示用于配置发送事件操作的其他选项。 在 **[!UICONTROL 类型]**，则可以提供自定义类型值，以填充 `eventType` XDM字段。 在 **[!UICONTROL XDM数据]**，提供您之前创建的XDM数据类型的名称（被百分比符号包围），或选择数据库图标(![“数据库”图标](./images/e2e/database-symbol.png))以从列表中选择它。 这是最终将发送到边缘网络的数据。

选择 **[!UICONTROL 保留更改]** 完成。

![操作配置](./images/e2e/action-config.png)

配置完规则后，选择 **[!UICONTROL 保存]** 来完成这个过程。

![保存规则](./images/e2e/save-rule.png)

### 构建和安装库 {#library}

配置规则后，您便可以将其添加到标记库，将该库构建到环境，然后在您的网站上安装该内部版本。

>[!NOTE]
>
>如果您尚未在数据收集UI中设置环境，则必须先设置环境，然后才能创建内部版本。 请参阅 [为web属性配置环境](../tags/ui/publishing/environments.md#web-configuration) （位于标记文档中）以了解更多信息。

要了解如何创建库、将扩展和规则添加到库，以及将库构建到环境，请参阅 [管理库](../tags/ui/publishing/libraries.md) （位于标记文档中）。 创建库时，请确保包含Platform Web SDK扩展以及之前创建的数据收集规则。

创建库并将其内部版本分配到环境后，即可在网站的客户端上安装该环境。 请参阅 [安装环境](../tags/ui/publishing/environments.md#installation) 以了解更多信息。

在网站上安装环境后，您可以 [测试实施](../tags/ui/publishing/embed-code-testing.md) 使用Adobe Experience Platform Debugger。

## 配置事件转发（可选） {#event-forwarding}

>[!NOTE]
>
>事件转发仅适用于已获得其许可的组织。

将SDK配置为将数据发送到边缘网络后，您可以设置事件转发以告知边缘网络您希望将数据发送到的位置。

要使用事件转发，您必须先创建事件转发属性。 选择 **[!UICONTROL 事件转发]** 在左侧导航中，选择 **[!UICONTROL 新建资产]**. 在选择之前，提供属性的名称 **[!UICONTROL 保存]**.

创建事件转发属性后，下一步是创建一个规则以确定应将数据发送到的位置。 事件转发属性的规则的构建方式与标记属性大致相同，但是无法指定任何事件（因为事件转发仅处理它直接从数据流接收的事件）。 对于规则的操作，您可以使用其中一个可用的事件转发扩展，也可以改用自定义代码来交付事件。

![事件转发规则](./images/e2e/event-forwarding-rule.png)

与之前类似，配置规则后，必须将其添加到库并将该库构建到环境。

生成完成后，最后一步是更新您的数据流 [之前配置的](#datastream) 和启用事件转发。 要开始，请导航到 **[!UICONTROL 数据流]** 并从列表中选择相关的数据流。 从此处，启用事件转发的切换开关，并提供您刚刚配置的属性和环境的名称。

![事件转发数据流](./images/e2e/event-forwarding-datastream.png)

## 后续步骤

本指南提供了有关如何使用Platform Web SDK将数据发送到边缘网络的高级端到端概述。 有关所涉及各个组件和服务的更多信息，请参阅本指南中链接的文档。
