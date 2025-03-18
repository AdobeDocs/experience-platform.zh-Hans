---
title: Graph Simulation UI指南
description: 了解如何在Identity Service UI中使用图形模拟。
exl-id: 89f0cf6e-c43f-40ec-859a-f3b73a6da8c8
source-git-commit: 7174c2c0d8c4ada8d5bba334492bad396c1cfb34
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 3%

---

# [!DNL Graph Simulation] UI 指南 {#graph-simulation}

>[!CONTEXTUALHELP]
>id="platform_identities_graphsimulation"
>title="图形模拟"
>abstract="模拟图形以了解身份标识服务如何链接身份标识，以及身份标识优化算法是如何工作的。"

>[!AVAILABILITY]
>
>* 标识图链接规则当前处于“有限可用”状态。 有关如何访问开发沙盒中的功能的信息，请与您的Adobe客户团队联系。
>
>* 您的帐户必须具有&#x200B;**查看身份图形**&#x200B;权限才能访问[!DNL Graph Simulation]工具。 有关详细信息，请阅读关于基于属性的访问控制中的权限的[指南](../../access-control/abac/ui/permissions.md)。

[!DNL Graph Simulation]是Identity Service UI中的一个工具，可用于模拟给定特定身份组合时身份图的行为方式以及配置[身份优化算法](./identity-optimization-algorithm.md)的方式。

观看以下视频，了解有关在Identity Service UI工作区中使用[!DNL Graph Simulation]界面的更多信息：

>[!VIDEO](https://video.tv.adobe.com/v/3444032/?learn=on&enablevpops)

阅读本文档以了解如何使用[!DNL Graph Simulation]更好地了解身份图行为以及图算法如何运行。

## 了解[!DNL Graph Simulation]界面 {#interface}

您可以在Adobe Experience Platform用户界面中访问[!DNL Graph Simulation]。 从左侧导航中选择&#x200B;**[!UICONTROL 标识]**，然后从顶部标题中选择&#x200B;**[!UICONTROL 图形模拟]**。

![Adobe Experience Platform UI中的图形模拟界面。](../images/graph-simulation/graph-simulation.png)

[!DNL Graph Simulation]接口可以分为三个部分：

>[!BEGINTABS]

>[!TAB 事件]

事件：使用&#x200B;**[!UICONTROL Events]**&#x200B;面板添加身份以模拟图形。 完全限定的身份必须具有身份命名空间及其相应的身份值。 您必须至少添加两个身份才能模拟图形。 您还可以选择&#x200B;**[!UICONTROL 加载示例]**&#x200B;来输入预配置的事件和算法设置。

![图形模拟工具的事件面板。](../images/graph-simulation/events.png)

>[!TAB 算法配置]

算法配置：使用&#x200B;**[!UICONTROL 算法配置]**&#x200B;面板为命名空间添加和配置优化算法。 您可以拖放命名空间以修改其各自的优先级排名。 您还可以选择&#x200B;**[!UICONTROL 每个图形唯一]**&#x200B;以确定命名空间是否唯一。

![图形模拟工具的算法配置。](../images/graph-simulation/algorithm-configuration.png)

>[!TAB 模拟图形查看器]

模拟的图形查看器：模拟的图形查看器根据您添加的事件和您配置的算法显示生成的图形。 两个身份之间的直线表示已建立链接。 虚线表示链接已被删除。

![模拟图形查看器面板，带有模拟图形的示例。](../images/graph-simulation/simulated-graph.png)

>[!ENDTABS]

## 添加事件 {#add-events}

要开始，请选择&#x200B;**[!UICONTROL 添加事件]**。

![已选择“添加事件”按钮。](../images/graph-simulation/add-events.png)

出现[!UICONTROL 事件#1]的弹出窗口。 在此处，输入您的身份命名空间和身份值组合。 您可以使用下拉菜单选择身份命名空间。 或者，您可以键入命名空间的前几个字母，然后选择下拉菜单中提供的选项。 选择命名空间后，请提供与命名空间对应的身份值。

![带有空接口的Event #1窗口。](../images/graph-simulation/event-one.png)

>[!TIP]
>
>您在[!DNL Graph Simulation]练习中输入的标识值不必是真实标识值，也可以是简单的占位符。

完成第一个身份后，选择添加图标(**`+`**)以添加第二个身份。

![在“图形模拟”的“事件”面板中输入{Email： tom@acme.com}的第一个完全限定标识。](../images/graph-simulation/event-one-added.png)

接下来，重复相同的步骤并添加第二个标识。 要生成标识图，需要两个完全限定的标识。 在以下示例中，ECID被添加为命名空间，并且被提供值为`111`。 完成后，选择&#x200B;**[!UICONTROL 保存]**。

![已将{ECID： 111}的第二个标识添加到事件#1。](../images/graph-simulation/first-event.png)

[!UICONTROL 事件]界面更新以显示您的第一个事件，在本例中为： `{Email: tom@acme.com, ECID: 111}`。

![更新的事件界面带有{Email： tom@acme.com，ECID： 111}。](../images/graph-simulation/add-second-event.png)

接下来，重复相同的步骤以添加第二个事件。 对于事件#2，添加`{Email: summer@acme.com}`作为您的第一个标识，然后添加相同的`{ECID: 111}`作为第二个标识，从而创建第二个事件： `{Email: summer@acme.com}, {ECID: 111}`。 完成后，您应该有两个事件，一个用于`{Email: tom@acme.com, ECID: 111}`，另一个用于`{Email: summer@acme.com}, {ECID: 111}`。

![更新的事件界面包含两个事件。](../images/graph-simulation/two-events.png)

### 加载示例 {#load-example}

选择&#x200B;**[!UICONTROL 加载示例]**&#x200B;以使用预设算法和事件配置设置示例图形。

![已选择“加载示例”选项。](../images/graph-simulation/load-example.png)

此时会出现一个弹出窗口，为您提供可以从以下内容中选择的可用图形方案：

| 示例图表 | 描述 | 示例 |
| --- | --- | --- |
| 共享设备 | 共享设备是指两个不同的用户登录到同一台设备的情况。 | 夫妻共享一个iPad用于互联网浏览和电子商务。 |
| 无效（非唯一）电话 | 无效或非唯一电话是指两个不同的用户使用相同的电话号码创建帐户的情况。 | 母亲和女儿使用共享的家庭电话号码注册任何电子商务帐户。 |
| “坏”的身份标识值 | “错误”标识值是指标识服务因错误实施而生成非唯一IDFA的情况。 | 由于代码实施问题，WebSDK错误地为每个事件发送了`user_null`值。 |

![显示可用预配置示例的窗口：共享设备、无效电话和错误标识值。](../images/graph-simulation/example-options.png)

选择任何选项以使用预配置的事件和算法加载[!DNL Graph Simulation]。 您仍然可以对任何预加载的图形方案示例进行进一步的配置。

![为无效电话配置的事件和算法。](../images/graph-simulation/example-loaded.png)

完成后，选择&#x200B;**[!UICONTROL 模拟]**。

![为无效电话模拟的示例图形。](../images/graph-simulation/example-simulated.png)

### 使用文本版本 {#use-text-version}

您还可以使用文本模式配置事件。 要使用文本模式，请选择设置图标，然后选择&#x200B;**[!UICONTROL 文本（高级用户）]**。

![选择的设置图标。](../images/graph-simulation/settings.png)

您可以使用文本模式手动输入身份。 使用冒号(`:`)区分与您输入的命名空间对应的标识值，然后使用逗号(`,`)分隔您的标识。 要区分不同的事件，请为每个事件使用新行。

![事件面板使用文本模式版本。](../images/graph-simulation/text-version.png)

### 编辑事件 {#edit-event}

要编辑事件，请选择给定事件旁边的省略号(`...`)，然后选择&#x200B;**[!UICONTROL 编辑]**。

![选定的编辑事件图标。](../images/graph-simulation/edit.png)

### 删除事件 {#delete-event}

要删除某个事件，请选择给定事件旁边的省略号(`...`)，然后选择&#x200B;**[!UICONTROL 删除]**。

![选择的删除事件图标。](../images/graph-simulation/delete.png)

## 配置算法 {#configure-algorithm}

>[!IMPORTANT]
>
>您配置的算法规定了Identity Service如何处理您在事件中输入的命名空间。 您在[!DNL Graph Simulation UI]中组合的任何配置都不会保存在身份设置中。

添加事件后，您现在可以配置将用于模拟图形的算法。 要开始，请选择&#x200B;**[!UICONTROL 添加配置]**。

![算法配置面板。](../images/graph-simulation/add-config.png)

出现空的配置行。 首先，输入您用于事件的同一命名空间。 在这种情况下，请先输入电子邮件。 输入命名空间后，[!UICONTROL 身份符号]和[!UICONTROL 身份类型]的列将自动填充。

![第一个配置条目。](../images/graph-simulation/add-namespace.png)

接下来，重复相同的步骤并添加第二个命名空间，在本例中为ECID。 输入所有命名空间后，即可开始配置其优先级和唯一性。

* **命名空间优先级**：命名空间的优先级决定了它与给定身份图中其他命名空间相比的相对重要性。 例如，如果身份图有四个不同的命名空间：CRMID、ECID、Email和Apple IDFA，则可以配置优先级以确定四个命名空间的重要性顺序。
* **唯一命名空间**：如果命名空间被指定为唯一，则标识服务将生成图形，并告诫只能存在一个具有给定唯一命名空间的标识。 例如，如果电子邮件命名空间指定为唯一的命名空间，则图表只能有一个电子邮件身份。 如果电子邮件命名空间中有多个身份，则将删除最早的链接。

要配置命名空间优先级，请选择命名空间行并将其拖动到所需的优先级排序，其中顶行表示较高的优先级，底行表示较低的优先级。 要将命名空间指定为唯一，请选中&#x200B;**[!UICONTROL 每个图形唯一]**&#x200B;复选框。

完成后，选择&#x200B;**[!UICONTROL 模拟]**。

![已配置所有命名空间。](../images/graph-simulation/all-namespaces.png)

## 查看模拟图形

[!UICONTROL 模拟图形]部分显示基于您添加的事件和您配置的算法生成的身份图形。

| 图表图标 | 描述 |
| --- | --- |
| 实线 | 实线表示两个身份之间已建立的链接。 |
| 虚线 | 虚线表示两个身份之间删除的链接。 |
| 联机编号 | 行中的数字表示生成该给定链接的时间戳。 最低数字(1)表示最早建立的链接。 |

在下面的示例图形中，`{Email: tom@acme.com}`到`{ECID: 111}`之间有虚线，原因如下：

* 在算法配置步骤中，电子邮件被指定为唯一的。 因此，一个图中可能只有一个具有电子邮件命名空间的身份。
* `{Email: tom@acme.com}`和`{ECID: 111}`之间的链接是第一个建立的标识(事件#1)。 它是最早的链接，因此被删除。

![模拟图形查看器面板，带有模拟图形的示例。](../images/graph-simulation/simulated-graph.png)

## 后续步骤

通过阅读本文档，您现在知道如何使用[!DNL Graph Simulation]工具来更好地了解在给定一组特定的规则和配置的情况下如何对待您的身份数据。 有关详细信息，请阅读以下文档：

* [身份图链接规则概述](./overview.md)
* [身份标识优化算法](./identity-optimization-algorithm.md)
* [实施指南](./implementation-guide.md)
* [疑难解答和常见问题](./troubleshooting.md)
* [图形配置示例](./example-configurations.md)
* [命名空间优先级](./namespace-priority.md)
* [身份设置UI](./identity-settings-ui.md)
