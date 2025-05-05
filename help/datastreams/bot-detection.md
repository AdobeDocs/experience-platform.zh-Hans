---
title: 为数据流配置机器人检测
description: 了解如何为数据流配置机器人检测，以区分人类和非人类流量。
exl-id: 6b221d97-0145-4d3e-a32d-746d72534add
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 0%

---

# 为数据流配置机器人检测

来自自动化程序、网页抓取程序、蜘蛛程序和脚本扫描程序的非人为流量可能会使识别来自人为访客的事件变得困难。 此类流量可能会对重要的业务量度产生负面影响，从而导致不正确的流量报表。

机器人检测允许您识别由[Web SDK](../web-sdk/home.md)、[Mobile SDK](https://developer.adobe.com/client-sdks/home/)和[[!DNL Edge Network API]](https://developer.adobe.com/data-collection-apis/docs/api/)生成的事件，这些事件是由已知的蜘蛛程序和机器人生成的。

通过为数据流配置机器人检测，您可以识别特定的IP地址、IP范围和请求标头，以分类为机器人事件。 这有助于更准确地测量您的网站或移动应用程序上的用户活动。

当对Edge Network的请求与任何机器人检测规则匹配时，XDM架构将更新为机器人得分（始终设置为1），如下所示：

```json
{
  "botDetection": {
    "score": 1
  }
}
```

此机器人评分可帮助接收请求的解决方案正确识别机器人流量。

>[!IMPORTANT]
>
>机器人检测不会丢弃任何机器人请求。 它仅使用机器人评分更新XDM架构，并将事件转发到您配置的[数据流服务](configure.md)。
>
>Adobe解决方案可能会以不同的方式处理机器人评分。 例如，Adobe Analytics使用自己的[机器人过滤服务](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/bot-removal/bot-rules.html)，而不使用Edge Network设置的分数。 这两个服务使用相同的[IAB机器人列表](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/)，因此机器人得分相同。

机器人检测规则在创建后可能需要15分钟才能在Edge Network中传播。

## 先决条件 {#prerequisites}

要使机器人检测在您的数据流上工作，您必须将&#x200B;**[!UICONTROL 机器人检测信息]**&#x200B;字段组添加到您的架构中。 请参阅[XDM架构](../xdm/ui/resources/schemas.md#add-field-groups)文档，了解如何将字段组添加到架构。

## 为数据流配置机器人检测 {#configure}

您可以在创建数据流配置后配置机器人检测。 请参阅有关如何[创建和配置数据流](configure.md)的文档，然后按照以下说明向数据流添加机器人检测功能。

转到数据流列表并选择要向其添加机器人检测的数据流。

![数据流用户界面显示数据流列表。](assets/bot-detection/datastream-list.png)

在数据流详细信息页面中，选择右边栏上的&#x200B;**[!UICONTROL 机器人检测]**&#x200B;选项。

数据流用户界面中高亮显示的![机器人检测选项。](assets/bot-detection/bot-detection.png)

将显示&#x200B;**[!UICONTROL 机器人检测规则]**&#x200B;页。

数据流设置页面中的![机器人检测设置。](assets/bot-detection/bot-detection-page.png)

在机器人检测规则页面中，您可以使用以下功能配置机器人检测：

* 使用[[!DNL [IAB/ABC International Spiders and Bots List]]](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/)。
* 创建自己的机器人检测规则。

### 使用IAB/ABC国际蜘蛛程序和机器人列表 {#iab-list}

[IAB/ABC国际蜘蛛程序和机器人列表](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/)是第三方行业标准的网络蜘蛛程序和机器人列表。 此列表可帮助您识别自动流量，例如搜索引擎爬网程序、监控工具以及其他您可能不希望包含在分析计数中的非人为流量。

要将数据流配置为使用IAB/ABC国际蜘蛛程序和机器人列表，请执行以下操作：

1. 切换&#x200B;**[!UICONTROL 在此数据流上使用IAB/ABC国际蜘蛛程序和机器人列表进行机器人检测选项]**。
2. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以将机器人检测设置应用于数据流。

![IAB蜘蛛程序和机器人列表已启用。](assets/bot-detection/bot-detection-list.png)

### 创建机器人检测规则 {#rules}

除了使用[IAB/ABC国际蜘蛛程序和机器人列表](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/)之外，您还可以为每个数据流定义自己的机器人检测规则。

您可以根据&#x200B;**IP地址**&#x200B;和&#x200B;**IP地址范围**&#x200B;创建机器人检测规则。

如果需要更细粒度的机器人检测规则，可以将IP条件与请求标头条件结合使用。 机器人检测规则可以使用以下标头：

| HTTP标头 | 描述 |
| --- | --- |
| `user-agent` | 允许服务器和网络对等方识别请求用户代理的应用程序、操作系统、供应商和/或版本的标头。 |
| `content-type` | 指示资源的原始媒体类型（在为发送应用任何内容编码之前）。 |
| `referer` | 标识从中请求资源的网页的地址。 |
| `sec-ch-ua` | 以逗号分隔列表的形式提供与浏览器关联的每个品牌的品牌和重要版本。 |
| `sec-ch-ua-mobile` | 指示浏览器是否位于移动设备上。 桌面浏览器也可以使用此参数来指示移动设备用户体验的偏好设置。 |
| `sec-ch-ua-platform` | 提供运行用户代理的平台或操作系统。 例如：“Windows”或“Android”。 |
| `sec-ch-ua-platform-version` | 提供运行用户代理的操作系统的版本。 |
| `sec-ch-ua-arch` | 提供user-agent的底层CPU体系结构，如ARM或x86。 |
| `sec-ch-ua-model` | 指示运行浏览器的设备型号。 |
| `sec-ch-ua-bitness` | 提供user-agent的底层CPU架构的“位数”。 这是整数或内存地址的大小（通常为64位或32位）。 |
| `sec-ch-ua-wow64` | 指示用户代理二进制文件是否在64位Windows上以32位模式运行。 |

要创建机器人检测规则，请执行以下步骤：

1. 选择&#x200B;**[!UICONTROL 添加新规则]**。

   ![突出显示了“添加新规则”按钮的机器人检测设置屏幕。](assets/bot-detection/bot-detection-new-rule.png)

2. 在&#x200B;**[!UICONTROL 规则名称]**&#x200B;字段中键入规则的名称。

   ![规则名称高亮显示的“机器人检测”规则屏幕。](assets/bot-detection/rule-name.png)

3. 选择&#x200B;**[!UICONTROL 添加新IP条件]**&#x200B;以添加新的基于IP的规则。 您可以按IP地址或IP地址范围定义规则。

   ![IP地址字段突出显示的机器人检测规则屏幕。](assets/bot-detection/ip-address-rule.png)

   ![IP范围字段突出显示的机器人检测规则屏幕。](assets/bot-detection/ip-range-rule.png)

   >[!TIP]
   >
   >IP条件基于逻辑`OR`操作。 如果请求与您定义的任何IP条件相匹配，则将其标记为来自机器人。

4. 如果要向规则添加标头条件，请选择&#x200B;**[!UICONTROL 添加标头条件组]**，然后选择要让规则使用的标头。

   ![标头条件高亮显示的Bot检测规则屏幕。](assets/bot-detection/header-conditions.png)

   然后，添加要用于所选标头的条件。

   ![标头条件高亮显示的Bot检测规则屏幕。](assets/bot-detection/header-condition-rule.png)

5. 配置所需的机器人检测规则后，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以将规则应用于数据流。

   ![标头条件高亮显示的Bot检测规则屏幕。](assets/bot-detection/bot-detection-save.png)


## 机器人检测规则示例 {#examples}

为了帮助您开始使用机器人检测，您可以使用下面详述的示例来创建机器人检测规则。

### 基于一个IP地址的机器人检测 {#one-ip}

要将所有来自特定IP地址的请求标记为机器人流量，请创建一个新的机器人检测规则，以评估单个IP地址，如下图所示。

![基于一个IP地址的机器人检测规则。](assets/bot-detection/bot-detection-one-ip.png)

### 基于两个IP地址的机器人检测 {#two-ip}

要将来自两个特定IP地址之一的所有请求标记为机器人流量，请创建一个新的机器人检测规则，该规则将评估两个IP地址，如下图所示。

![基于两个IP地址的机器人检测规则。](assets/bot-detection/bot-detection-two-ips.png)

### 基于IP地址范围的机器人检测 {#range}

要将来自特定范围内任何IP地址的所有请求标记为机器人流量，请创建一个新的机器人检测规则，以评估整个IP地址范围，如下图所示。

![基于IP范围的机器人检测规则。](assets/bot-detection/bot-detection-range.png)

### 基于IP地址和请求头的机器人检测 {#ip-header}

要将所有来自特定IP地址并包含特定请求标头的请求标记为机器人流量，请创建新的机器人检测规则，如下图所示。

此规则检查请求是否来自特定IP地址，以及`referer`请求标头是否以`www.adobe.com`开头。

![基于IP地址和请求标头的Bot检测规则。](assets/bot-detection/bot-detection-header-ip.png)

### 基于多种条件的机器人检测 {#multiple-conditions}

您可以根据以下内容创建机器人检测规则：

* **多个不同的条件**：将不同的条件评估为逻辑`AND`操作，这意味着需要同时满足这些条件，才能将请求识别为源自机器人。
* **同一类型的多个条件**：将同一类型的条件作为逻辑`OR`操作进行评估，这意味着如果满足任何条件，则将该请求标识为源自机器人。

下图中所示的规则在符合以下条件时标识源自机器人的请求：

请求来自两个IP地址中的任意一个，`referer`标头以`www.adobe.com`开头，`sec-ch-ua-mobile`标头将请求标识为来自桌面浏览器。

![基于多个条件的机器人检测规则。](assets/bot-detection/bot-detection-multiple.png)
