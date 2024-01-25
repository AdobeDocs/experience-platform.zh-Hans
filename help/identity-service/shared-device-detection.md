---
keywords: Experience Platform；主页；热门主题；Identity服务；Identity服务；共享设备；共享设备
title: 共享设备概述（测试版）
description: 共享设备检测可识别同一设备的不同经过身份验证的用户，从而允许在标识图中更准确地表示客户数据
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: d7c7bed74d746aba2330ecba62f9f810fbaf0d63
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# 共享设备检测概述(Beta)

>[!IMPORTANT]
>
>此 [!DNL Shared Device Detection] 功能处于测试阶段。 其功能和文档可能会发生更改。

Adobe Experience Platform [!DNL Identity Service] 通过跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，帮助您更好地了解客户及其行为。

[!DNL Shared Device] 是指由多个用户使用的设备。 共享设备的示例包括平板电脑、库计算机和信息亭。 通过 [!DNL Shared Device Detection] 能够防止同一设备的不同用户被合并为单个身份，从而能够更准确地表示个人。

替换为 [!DNL Shared Device Detection] 您可以：

* 为同一设备的不同用户创建单独的身份图；
* 使用同一设备防止混合不同个人的数据；
* 生成更清晰、更准确的客户视图。

>[!TIP]
>
>的配置 [!DNL Shared Device Detection] 必须为数据集启用配置文件之前完成，因为一旦在中生成图形，您将无法再修订设置 [!DNL Identity Service].

## [!DNL Shared Device Detection] 入门

使用 [!DNL Shared Device Detection] 需要了解所涉及的各种Platform服务。 开始使用之前 [!DNL Shared Device Detection]，请查看以下服务的文档：

* [[!DNL Identity Service]](./home.md)：通过跨设备和系统桥接身份，更好地了解个人客户及其行为。
   * [身份图查看器](./features/identity-graph-viewer.md)：可视化身份图查看器并与之交互，以更好地了解客户身份如何拼接以及拼接方式。
   * [身份命名空间](./features/namespaces.md)：查看完全限定的身份的组件，以及身份命名空间如何允许您区分身份的上下文和类型。

## 了解 [!DNL Shared Device Detection]

在使用时，请务必了解以下术语
[!DNL Shared Device Detection]. 有关理解所必需术语的列表，请参见下表 [!DNL Shared Device Detection].

### 术语

| 术语 | 定义 |
| --- | --- |
| 共享设备 | 共享设备是指由多个用户使用的任何设备。 共享设备的示例包括平板电脑、库计算机和信息亭。 |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] 指允许来自同一设备的不同用户的数据相互分离的配置设置。 |
| 共享身份命名空间 | 共享身份命名空间表示可供多个用户使用的设备。 共享身份命名空间通常是ECID，但可以设置为其他设备ID。 |
| 用户身份命名空间 | 用户身份命名空间表示共享设备的已验证（已登录）用户。 |
| 上次验证用户 | 如果某个设备正由多个帐户登录，则最后一个经过身份验证的用户表示上次登录到设备的用户。 |

{style="table-layout:auto"}

[!DNL Shared Device Detection] 通过建立两个命名空间来工作： **共享身份命名空间** 和 **用户身份命名空间**.

* 共享身份命名空间表示可供多个用户使用的设备。 Adobe建议客户使用ECID作为共享设备标识符。
* 用户身份命名空间将映射到与用户的登录ID对应的身份命名空间，这可以是用户的CRM ID、电子邮件地址、散列电子邮件或电话号码。

共享设备（如平板电脑）只有一个 **共享身份命名空间**. 另一方面，共享设备的每个用户都有自己的指定 **用户身份命名空间** 与其各自登录ID对应的证书。 例如，Kevin和Nora共享用于电子商务的平板电脑具有自己的ECID `1234`，而Kevin具有映射到其的用户身份命名空间 `kevin@email.com` 帐户和Nora具有映射到其自身的用户身份命名空间 `nora@email.com` 帐户。

[!DNL Shared Device Detection] 能够通过链接共享身份命名空间(例如， ECID)，并具有上次验证用户的用户身份命名空间（登录ID）。

### 如何将身份数据发送到身份图

请考虑以下示例，以帮助您了解如何 [!DNL Shared Device Detection] 工作：

>[!NOTE]
>
>在此图表中，共享身份命名空间配置为ECID，用户身份命名空间配置为CRM ID。

![图](./images/shared-device/diagram.png)

* Kevin和Nora共享平板电脑访问电子商务网站。 然而，他们都有自己的独立账户，用于在线浏览和购物；
   * 作为共享设备，平板电脑具有相应的ECID，它表示平板电脑的网页浏览器Cookie ID；
* 假设Kevin使用平板电脑 **登录** 转到他的电子商务帐户以浏览耳机，然后这意味着Kevin的CRM ID (**用户身份命名空间**)现在与平板电脑的ECID相关联(**共享身份命名空间**)。 现在，平板电脑的浏览数据已与Kevin的身份图相结合。
   * 如果Kevin **注销** 诺拉用平板电脑 **登录** 到她自己的帐户并购买相机，然后她的CRM ID现在与平板电脑的ECID相关联。 因此，平板电脑的浏览数据现在与Nora的身份图相结合。
   * 如果Nora **不注销** 凯文用平板电脑，但是 **未登录**，则平板电脑的浏览数据仍会与Nora合并，因为她仍为经过身份验证的用户，并且她的CRM ID仍会与平板电脑的ECID关联。
   * 如果Nora **确实注销** 凯文用平板电脑，但是 **未登录**，则平板电脑的浏览数据仍会与Nora的身份图相结合，因为作为 **上次验证用户**，则她的CRM ID仍与平板电脑的ECID相关联。
   * 如果Kevin **登录** 同样地，他的CRM ID现在链接到平板电脑的ECID，因为他现在是最后一个经过身份验证的用户，而且平板电脑的浏览数据现在与他的身份图相结合。

### 如何 [!DNL Profile Service] 将配置文件片段与合并 [!DNL Shared Device Detection] 已启用

[!DNL Profile Service] 记录配置文件片段和合并的配置文件。 每个单独的客户配置文件都由多个配置文件片段组成，这些片段已合并以形成该客户的单一视图。 例如，如果客户跨多个渠道与您的品牌互动，则您的组织将在多个数据集中显示多个与该单个客户相关的配置文件片段。 将这些片段摄取到Platform后，会合并在一起，以便为该客户创建一个配置文件。

时间 [!DNL Shared Device Detection] 已启用， [!DNL Profile] 根据体验事件是经过身份验证还是未经身份验证，定义配置文件片段的主要身份

An **经过身份验证的体验事件** 是用户在登录到设备时完成的操作。 对于经过身份验证的体验事件，主要标识为 **用户身份命名空间** （登录ID）。 An **未经身份验证的体验事件** 是未登录到设备的用户完成的操作。 对于未经身份验证的体验事件，主要标识是 **共享身份命名空间** (ECID)。

欲了解更多信息，请参见  [[!DNL Real-Time Customer Profile] 概述](../profile/home.md).

## 共享设备UI

在Platform UI中，选择 **[!UICONTROL 身份]** 从左侧导航中，然后选择 **[!UICONTROL 身份设置]**.

![identity-dashboard](./images/shared-device/identity-dashboard.png)

此 [!UICONTROL 共享设备设置] 页面显示，为您提供一个界面，用于配置数据的共享设备设置。 默认情况下，共享设备设置处于禁用状态。

启用后，共享设备设置允许来自同一设备的不同用户的数据相互分离。 此配置设置允许更简洁且更准确地表示同一设备的用户身份图，其中不会将同一设备的用户身份组合在一起。

选择 **[!UICONTROL 启用]** 以开始修改共享设备设置。

![启用 — 共享设备](./images/shared-device/enable-shared-device.png)

此 [!UICONTROL 共享身份命名空间] 和 [!UICONTROL 用户身份命名空间] 此时会显示配置选项，允许您修改要使用的身份命名空间。

![set-namespaces](./images/shared-device/set-namespaces.png)

[!UICONTROL 共享身份命名空间] 表示由多个不同用户使用的单个设备。 此命名空间始终设置为 **[!UICONTROL ECID]** 因为所有平台用户都使用 **[!UICONTROL ECID]** 作为Web浏览器标识符。

![shared-identity-namespace](./images/shared-device/shared-identity-namespace.png)

此 [!UICONTROL 用户身份命名空间] 用于识别同一设备的不同用户，并防止数据合并到同一身份图中。

![user-identity-namespace](./images/shared-device/user-identity-namespace.png)

选择 **[!UICONTROL 用户身份命名空间]** 搜索栏，然后输入身份命名空间或从下拉菜单中选择身份命名空间。

>[!TIP]
>
>此 [!UICONTROL 用户身份命名空间] 应映射到与最终用户的登录ID对应的身份命名空间。 相关选项包括客户ID、电子邮件和经过哈希处理的电子邮件。

![电子邮件](./images/shared-device/emails.png)

配置您的 [!UICONTROL 共享设备设置]，选择 **[!UICONTROL 保存]**.

![保存](./images/shared-device/save.png)

此时会出现一个弹出窗口，提示您确认您的选择。 选择 **[!UICONTROL 是]** 以完成配置设置。

![确认](./images/shared-device/confirm.png)
