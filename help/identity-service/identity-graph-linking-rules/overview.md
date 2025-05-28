---
title: 身份图链接规则
description: 了解Identity Service中的Identity Graph链接规则。
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 38d331bd9265f25a3aebdcbd20ae5fc30a93e960
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 7%

---

# [!DNL Identity Graph Linking Rules] 概述 {#identity-graph-linking-rules-overview}

>[!CONTEXTUALHELP]
>id="platform_identities_linkingrules_overview"
>title="身份标识图链接规则"
>abstract="要防止这些不需要的合并，您可以使用通过Identity Graph链接规则提供的配置，并允许对用户进行准确的个性化。"

>[!IMPORTANT]
>
>[!DNL Identity Graph Linking Rules]现已正式可用。 如果您有一个现有的沙盒，需要在启用身份设置后取消折叠图形（“已修复”），请联系您的Adobe客户团队或Adobe支持。

通过Adobe Experience Platform Identity服务和实时客户个人资料，可以轻松假设您的数据被完全摄取，并且所有合并的个人资料都通过人员标识符（如CRMID）表示单个个人。 但是，在某些情况下，某些数据可能会尝试将多个不同的配置文件合并到单个配置文件中（“图形折叠”）。 为了防止这些不需要的合并，您可以使用通过[!DNL Identity Graph Linking Rules]提供的配置，并允许用户的准确个性化。

## 快速入门

以下文档是了解[!DNL Identity Graph Linking Rules]所必需的。

* [身份优化算法](./identity-optimization-algorithm.md)
* [实施指南](./implementation-guide.md)
* [图形配置示例](./example-configurations.md)
* [疑难解答和常见问题](./troubleshooting.md)
* [命名空间优先级](./namespace-priority.md)
* [图形模拟UI](./graph-simulation.md)
* [身份设置UI](./identity-settings-ui.md)

## 视频库

观看以下视频，了解身份图链接规则的一些基本方面。

<!-- CARDS
{target = _blank}
* https://experienceleague.adobe.com/zh-hans/docs/platform-learn/tutorials/identities/graph-linking-rules/overview
* https://experienceleague.adobe.com/zh-hans/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation 

    {description = Learn how to use the graph simulator to test out identity graph linking rules.}

* https://experienceleague.adobe.com/zh-hans/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings
    {description = Learn how to enable and configure identity graph linking rules to build accurate customer profiles}
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules overview">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/zh-hans/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" title="身份标识图链接规则概述" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3448282/?format=jpeg&nocache=1747851655227&captions=chi_hans" alt="身份标识图链接规则概述"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/zh-hans/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" target="_blank" rel="referrer" title="身份标识图链接规则概述">身份标识图链接规则概述</a>
                    </p>
                    <p class="is-size-6">获取身份标识图链接规则如何帮助数据架构师维护准确的客户轮廓并防止图形崩溃的概述。</p>
                </div>
                <a href="https://experienceleague.adobe.com/zh-hans/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">观看</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules - Graph Simulation">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/zh-hans/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" title="身份图形链接规则 — 图形模拟" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3444053/?format=jpeg&nocache=1747851655237&captions=chi_hans" alt="身份图形链接规则 — 图形模拟"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/zh-hans/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" target="_blank" rel="referrer" title="身份图形链接规则 — 图形模拟">身份标识图链接规则 - 图形模拟</a>
                    </p>
                    <p class="is-size-6">了解如何使用图形模拟器来测试身份图形链接规则。</p>
                </div>
                <a href="https://experienceleague.adobe.com/zh-hans/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">观看</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules - Identity settings">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/zh-hans/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" title="身份图链接规则 — 身份设置" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3458487/?format=jpeg&nocache=1747851655218" alt="身份图链接规则 — 身份设置"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/zh-hans/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" target="_blank" rel="referrer" title="身份图链接规则 — 身份设置">身份图形链接规则 — 身份设置</a>
                    </p>
                    <p class="is-size-6">了解如何启用和配置身份图链接规则以构建准确的客户个人资料</p>
                </div>
                <a href="https://experienceleague.adobe.com/zh-hans/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">观看</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


## 图形折叠场景 {#graph-collapse-scenarios}

>[!CONTEXTUALHELP]
>id="platform_identities_graphcollapsescenarios"
>title="图形折叠场景"
>abstract="图形可能“折叠”或代表多个人物实体的原因有多种。"

本节概述配置[!DNL Identity Graph Linking Rules]时可以考虑的示例场景。

### 共享设备

在某些情况下，单个设备可能会发生多次登录：

| 共享设备 | 描述 |
| --- | --- |
| 家用计算机和平板电脑 | 丈夫和妻子均登录各自的银行账户。 |
| 公共信息亭 | 在机场登机的旅客使用他们的忠诚身份证登记签到行李并打印登机牌。 |
| 呼叫中心 | 呼叫中心人员代表致电客户支持以解决问题的客户在单个设备上登录。 |

![一些常用共享设备的图表。](../images/identity-settings/shared-devices.png "一些常用共享设备的图表。"){zoomable="yes"}

在这些情况下，从图形的角度来看，未启用任何限制，单个ECID将链接到多个CRMID。

使用[!DNL Identity Graph Linking Rules]，您可以：

* 配置用于作为唯一标识符登录的ID。 例如，您可以限制图形仅存储一个具有CRMID命名空间的身份，从而将CRMID定义为共享设备的唯一标识符。
   * 通过这样做，您可以确保ECID不会合并CRMID。

### 电子邮件/电话方案无效

还有一些用户在注册时提供虚假值作为电话号码和/或电子邮件地址的实例。 在这些情况下，如果未启用限制，则电话/电子邮件相关的身份最终会链接到多个不同的CRMID。

![表示无效电子邮件或电话方案的图表。](../images/identity-settings/invalid-email-phone.png "表示无效电子邮件或电话方案的图表。"){zoomable="yes"}

使用[!DNL Identity Graph Linking Rules]，您可以：

* 将CRMID、电话号码或电子邮件地址配置为唯一标识符，因此将一个人限制为只能有一个与其帐户关联的CRMID、电话号码和/或电子邮件地址。

### 标识值错误或错误

在某些情况下，会在系统中摄取非唯一、错误的标识值，而不管命名空间如何。 示例包括：

* 标识值为“user_null”的IDFA命名空间。
   * IDFA标识值应包含36个字符：32个字母数字字符和4个连字符。
* 标识值为“未指定”的电话号码命名空间。
   * 电话号码不应包含任何字母字符。

这些标识可能会导致以下图表，其中多个CRMID与“坏”标识合并：

![具有错误或错误标识值的标识数据的图形示例。](../images/identity-settings/bad-data.png "具有错误或错误标识值的标识数据的图形示例。"){zoomable="yes"}

使用[!DNL Identity Graph Linking Rules]，您可以将CRMID配置为唯一标识符，以防止由于此类数据而造成不需要的配置文件折叠。

## [!DNL Identity Graph Linking Rules] {#identity-graph-linking-rules}

通过[!DNL Identity Graph Linking Rules]，您可以：

* 通过配置唯一的命名空间，为每个用户创建单个身份图/合并的配置文件，这将阻止两个不同的人员标识符合并到一个身份图中。
* 通过配置优先级，将经过身份验证的在线事件与人员关联

### 术语 {#terminology}

| 术语 | 描述 |
| --- | --- |
| 唯一命名空间 | 唯一命名空间是已设置为在身份图上下文中不同的身份命名空间。 您可以使用UI将命名空间配置为唯一。 将命名空间定义为唯一后，图形只能有一个包含该命名空间的标识。 |
| 命名空间优先级 | 命名空间优先级是指命名空间彼此相比的相对重要性。 命名空间优先级可通过UI进行配置。 您可以在给定的身份图中对命名空间进行排名。 启用后，名称优先级将用于各种场景，例如身份优化算法的输入以及确定体验事件片段的主要身份。 |
| 身份优化算法 | 身份优化算法确保在给定的身份图中实施通过配置唯一的命名空间和命名空间优先级创建的准则。 |

### 唯一命名空间 {#unique-namespace}

您可以使用身份设置UI工作区将命名空间配置为唯一。 这样做会通知身份优化算法，给定图形可能只有一个包含该唯一命名空间的身份。 这可以防止在同一图形中合并两个不同的人员标识符。

请考虑以下方案：

* Scott使用平板电脑打开Google Chrome浏览器前往acme<span>.com，登录并浏览新篮球鞋。
   * 在幕后，此场景记录以下身份：
      * 用于表示浏览器使用情况的ECID命名空间和值
      * 用于表示经过身份验证的用户（Scott使用其用户名和密码组合登录）的CRMID命名空间和值。
* 然后，他的儿子彼得使用同一台平板电脑，并使用Google Chrome访问acme<span>.com，他在那里使用自己的帐户登录以浏览足球设备。
   * 在幕后，此场景记录以下身份：
      * 表示浏览器的相同ECID命名空间和值。
      * 用于表示经过身份验证的用户的新CRMID命名空间和值。

如果将CRMID配置为唯一命名空间，则身份优化算法会将CRMID拆分为两个单独的身份图，而不是将它们合并在一起。

如果不配置唯一的命名空间，最终可能会导致不需要的图形合并，例如具有相同CRMID命名空间但不同标识值的两个标识（此类情况通常表示同一图形中的两个不同人员实体）。

您必须配置唯一的命名空间，以通知身份优化算法强制对摄取到给定身份图中的身份数据实施限制。

### 命名空间优先级 {#namespace-priority}

命名空间优先级是指命名空间彼此相比的相对重要性。 命名空间优先级可通过UI进行配置，并且您可以在给定的身份图中对命名空间进行排名。

使用命名空间优先级的一种方式是，确定实时客户配置文件中体验事件片段（用户行为）的主要身份。 如果配置了优先级设置，则将不再使用Web SDK上的主要身份设置来确定存储了哪些配置文件片段。

唯一的命名空间和命名空间优先级可以在身份设置UI工作区中进行配置。 但是，其配置的影响是不同的：

| | 身份标识服务 | 实时客户轮廓 |
| --- | --- | --- |
| 唯一命名空间 | 在Identity Service中，身份优化算法通过引用唯一的命名空间来确定被摄取到给定身份图的身份数据。 | 唯一的命名空间不影响实时客户资料。 |
| 命名空间优先级 | 在Identity Service中，对于具有多个层的图形，命名空间优先级将确定删除了相应的链接。 | 在配置文件中摄取体验事件时，具有最高优先级的命名空间成为配置文件片段的主要身份。 |

* 当达到每个图形50个标识的限制时，命名空间优先级不会影响图形行为。
* **命名空间优先级是分配给命名空间的数值**，用于指示其相对重要性。 这是命名空间的属性。
* **主标识是针对**&#x200B;存储配置文件片段的标识。 配置文件片段是存储有关特定用户的信息的数据记录：属性（通常通过CRM记录摄取）或事件（通常从体验事件或在线数据中摄取）。
* 命名空间优先级确定体验事件片段的主要身份。
   * 对于配置文件记录，您可以使用Experience Platform UI中的架构工作区来定义身份字段，包括主要身份。 有关详细信息，请阅读[在UI](../../xdm/ui/fields/identity.md)中定义标识字段的指南。
* 如果体验事件在identityMap中具有两个或多个具有最高命名空间优先级的身份，则该事件将被拒绝引入，因为它将被视为“错误数据”。 例如，如果identityMap包含`{ECID: 111, CRMID: John, CRMID: Jane}`，则整个事件将作为错误数据被拒绝，因为它意味着该事件同时与`CRMID: John`和`CRMID: Jane`相关联。

有关详细信息，请阅读有关[命名空间优先级](./namespace-priority.md)的指南。

## 后续步骤

有关[!DNL Identity Graph Linking Rules]的详细信息，请阅读以下文档：

* [身份优化算法](./identity-optimization-algorithm.md)
* [实施指南](./implementation-guide.md)
* [图形配置示例](./example-configurations.md)
* [疑难解答和常见问题](./troubleshooting.md)
* [命名空间优先级](./namespace-priority.md)
* [图形模拟UI](./graph-simulation.md)
* [身份设置UI](./identity-settings-ui.md)