---
keywords: Experience Platform；主页；热门主题；Identity服务；Identity服务；共享设备；共享设备
title: 共享设备概述(Beta)
description: 共享设备检测可识别同一设备的不同经过身份验证的用户，从而允许在标识图中更准确地表示客户数据
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 0%

---

# 共享设备检测概述(Beta)

>[!IMPORTANT]
>
>[!DNL Shared Device Detection]功能处于测试阶段。 其功能和文档可能会发生更改。

Adobe Experience Platform [!DNL Identity Service]通过跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，从而帮助您更好地了解客户及其行为。

[!DNL Shared Device]是指由多个用户使用的设备。 共享设备的示例包括平板电脑、库计算机和信息亭。 通过[!DNL Shared Device Detection]功能，可防止同一设备的不同用户被合并为单个身份，从而更准确地表示个人。

通过[!DNL Shared Device Detection]，您可以：

* 为同一设备的不同用户创建单独的身份图；
* 使用同一设备防止混合不同个人的数据；
* 生成更清晰、更准确的客户视图。

>[!TIP]
>
>在启用数据集的配置文件之前，必须完成[!DNL Shared Device Detection]的配置，因为一旦在[!DNL Identity Service]中生成图形，您将无法再修订设置。

## [!DNL Shared Device Detection] 入门

使用[!DNL Shared Device Detection]需要了解所涉及的各种Platform服务。 在开始使用[!DNL Shared Device Detection]之前，请查看以下服务的文档：

* [[!DNL Identity Service]](./home.md)：通过跨设备和系统桥接身份，更好地了解个人客户及其行为。
   * [身份图查看器](./features/identity-graph-viewer.md)：可视化身份图查看器并与之交互，以便更好地了解客户身份如何拼接以及拼接方式。
   * [身份命名空间](./features/namespaces.md)：查看完全限定的身份的组件，以及身份命名空间如何允许您区分身份的上下文和类型。

## 了解 [!DNL Shared Device Detection]

在使用时，请务必了解以下术语
[!DNL Shared Device Detection]。 请参阅下表，获取理解[!DNL Shared Device Detection]所必需术语的列表。

### 术语

| 术语 | 定义 |
| --- | --- |
| 共享设备 | 共享设备是指由多个用户使用的任何设备。 共享设备的示例包括平板电脑、库计算机和信息亭。 |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection]是指允许来自同一设备的不同用户的数据相互分离的配置设置。 |
| 共享标识命名空间 | 共享身份命名空间表示可供多个用户使用的设备。 共享身份命名空间通常是ECID，但可以设置为其他设备ID。 |
| 用户标识命名空间 | 用户身份命名空间表示共享设备的已验证（已登录）用户。 |
| 上次验证用户 | 如果某个设备正由多个帐户登录，则最后一个经过身份验证的用户表示上次登录到设备的用户。 |

{style="table-layout:auto"}

[!DNL Shared Device Detection]通过建立两个命名空间来工作：**共享身份命名空间**&#x200B;和&#x200B;**用户身份命名空间**。

* 共享身份命名空间表示可供多个用户使用的设备。 Adobe建议客户使用ECID作为共享设备标识符。
* 用户身份命名空间将映射到与用户的登录ID对应的身份命名空间，这可以是用户的CRMID、电子邮件地址、散列电子邮件或电话号码。

共享设备（如平板电脑）具有单个&#x200B;**共享身份命名空间**。 另一方面，共享设备的每个用户都有自己的指定&#x200B;**用户标识命名空间**，该命名空间与其各自的登录ID相对应。 例如，Kevin和Nora共享用于电子商务的平板电脑具有自己的ECID `1234`，而Kevin具有映射到其`kevin@email.com`帐户的用户身份命名空间，并且Nora具有映射到其`nora@email.com`帐户的用户身份命名空间。

[!DNL Shared Device Detection]可以通过链接共享身份命名空间(例如， ECID)，并具有上次验证用户的用户身份命名空间（登录ID）。

### 如何将身份数据发送到身份图

请考虑以下示例，以帮助您了解[!DNL Shared Device Detection]的工作方式：

>[!NOTE]
>
>在此图表中，共享身份命名空间配置为ECID，用户身份命名空间配置为CRMID。

![图表](./images/shared-device/diagram.png)

* Kevin和Nora共享平板电脑访问电子商务网站。 然而，他们都有自己的独立账户，用于在线浏览和购物；
   * 作为共享设备，平板电脑具有相应的ECID，它表示平板电脑的网页浏览器Cookie ID；
* 假设Kevin使用平板电脑并&#x200B;**登录**&#x200B;到他的电子商务帐户来浏览耳机，这就意味着Kevin的CRMID （**用户身份命名空间**）现在与平板电脑的ECID （**共享身份命名空间**）相关联。 现在，平板电脑的浏览数据已与Kevin的身份图相结合。
   * 如果Kevin **注销**，且Nora使用平板电脑，**登录**&#x200B;到自己的帐户并购买摄像头，则其CRMID现在已链接到平板电脑的ECID。 因此，平板电脑的浏览数据现在与Nora的身份图相结合。
   * 如果Nora **未注销**，而Kevin使用平板电脑，但&#x200B;**未登录**，则平板电脑的浏览数据仍会与Nora合并，因为她仍为经过身份验证的用户，并且她的CRMID仍与平板电脑的ECID关联。
   * 如果Nora **确实注销**，而Kevin使用平板电脑，但&#x200B;**没有登录**，则平板电脑的浏览数据仍会与Nora的标识图合并，因为作为&#x200B;**上次经过身份验证的用户**，她的CRMID仍与平板电脑的ECID相关联。
   * 如果Kevin **再次登录**，则他的CRMID现在链接到平板电脑的ECID，因为他是最后一个经过身份验证的用户，并且平板电脑的浏览数据现在已合并到他的身份图中。

### [!DNL Profile Service]如何在启用[!DNL Shared Device Detection]的情况下合并配置文件片段

[!DNL Profile Service]记下配置文件片段和合并的配置文件。 每个单独的客户配置文件都由多个配置文件片段组成，这些片段已合并以形成该客户的单一视图。 例如，如果客户跨多个渠道与您的品牌互动，则您的组织将在多个数据集中显示多个与该单个客户相关的配置文件片段。 将这些片段摄取到Platform后，会合并在一起，以便为该客户创建一个配置文件。

启用[!DNL Shared Device Detection]后，[!DNL Profile]根据体验事件是经过身份验证还是未经身份验证来定义配置文件片段的主身份

**已验证的体验事件**&#x200B;是用户登录设备时完成的操作。 对于经过身份验证的体验事件，主标识是&#x200B;**用户标识命名空间** （登录ID）。 **未经身份验证的体验事件**&#x200B;是由未登录到设备的用户完成的操作。 对于未经身份验证的体验事件，主身份是&#x200B;**共享身份命名空间** (ECID)。

有关详细信息，请参阅[[!DNL Real-Time Customer Profile] 概述](../profile/home.md)。

## 共享设备UI

在Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 标识]**，然后选择&#x200B;**[!UICONTROL 标识设置]**。

![identity-dashboard](./images/shared-device/identity-dashboard.png)

此时会显示[!UICONTROL 共享设备设置]页面，该页面为您提供了一个配置共享设备设置的数据界面。 默认情况下，共享设备设置处于禁用状态。

启用后，共享设备设置允许来自同一设备的不同用户的数据相互分离。 此配置设置允许更简洁且更准确地表示同一设备的用户身份图，其中不会将同一设备的用户身份组合在一起。

选择&#x200B;**[!UICONTROL 启用]**&#x200B;以开始修改共享设备设置。

![启用共享设备](./images/shared-device/enable-shared-device.png)

将显示[!UICONTROL 共享身份命名空间]和[!UICONTROL 用户身份命名空间]配置选项，允许您修改要使用的身份命名空间。

![设置命名空间](./images/shared-device/set-namespaces.png)

[!UICONTROL 共享身份命名空间]表示多个不同用户使用的单个设备。 此命名空间始终设置为&#x200B;**[!UICONTROL ECID]**，因为所有Platform用户都使用&#x200B;**[!UICONTROL ECID]**&#x200B;作为Web浏览器标识符。

![共享身份命名空间](./images/shared-device/shared-identity-namespace.png)

[!UICONTROL 用户身份命名空间]允许您识别同一设备的不同用户，并防止数据合并到同一身份图中。

![用户标识命名空间](./images/shared-device/user-identity-namespace.png)

选择&#x200B;**[!UICONTROL 用户身份命名空间]**&#x200B;搜索栏，然后输入身份命名空间或从下拉菜单中选择身份命名空间。

>[!TIP]
>
>[!UICONTROL 用户身份命名空间]应映射到与最终用户的登录ID对应的身份命名空间。 相关选项包括客户ID、电子邮件和经过哈希处理的电子邮件。

![电子邮件](./images/shared-device/emails.png)

配置[!UICONTROL 共享设备设置]后，选择&#x200B;**[!UICONTROL 保存]**。

![保存](./images/shared-device/save.png)

此时会出现一个弹出窗口，提示您确认您的选择。 选择&#x200B;**[!UICONTROL 是]**&#x200B;以完成配置设置。

![确认](./images/shared-device/confirm.png)
