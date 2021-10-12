---
keywords: Experience Platform；主页；热门主题；Identity Service;Identity Service；共享设备；共享设备
solution: Experience Platform
title: 共享设备概述（测试版）
topic-legacy: tutorial
description: “共享设备检测”可识别同一设备的经过身份验证的不同用户，从而允许在身份图中更准确地表示客户数据
hide: true
hidefromtoc: true
source-git-commit: 9c0d360b39bf69a44ac6298724dbab0f8456dc90
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# 共享设备检测概述（测试版）

>[!IMPORTANT]
>
>[!DNL Shared Device Detection]功能处于测试阶段。 其功能和文档可能会发生更改。

Adobe Experience Platform [!DNL Identity Service]通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而帮助您更好地了解客户及其行为。

[!DNL Shared Device] 是指由多个个人使用的设备。共享设备的示例包括平板电脑、库计算机和网亭。 通过[!DNL Shared Device Detection]功能，可以阻止同一设备的不同用户合并到单个身份中，从而实现更准确的表示。

通过[!DNL Shared Device Detection]，您可以：

* 为同一设备的不同用户创建单独的身份图；
* 防止使用同一设备的不同个人混合数据；
* 更清晰、更准确地查看客户。

>[!TIP]
>
>在为数据集启用[!DNL Profile]之前，必须完成[!DNL Shared Device Detection]的配置，因为在[!DNL Identity Service]中生成图形后，您将不再修订设置。

## 快速入门

使用[!DNL Shared Device Detection]需要了解所涉及的各种平台服务。 开始使用[!DNL Shared Device Detection]之前，请查阅以下服务的文档：

* [[!DNL Identity Service]](../home.md):通过跨设备和系统桥接身份，更好地了解各个客户及其行为。
   * [身份图查看器](./identity-graph-viewer.md):可视化身份图形查看器并与之进行交互，以便更好地了解客户身份如何拼合在一起，以及以何种方式拼合在一起。
   * [身份命名空间](../namespaces.md):请参阅完全限定身份的组件，以及身份命名空间如何让您区分身份的上下文和类型。

### 术语

下表包含理解[!DNL Shared Device Detection]所必需的术语列表：

| 术语 | 定义 |
| --- | --- |
| 共享设备 | 共享设备是指多个个人使用的任何设备。 共享设备的示例包括平板电脑、库计算机和网亭。 |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] 是指一种配置设置，允许将来自同一设备的不同用户的数据彼此分离。 |
| [!UICONTROL 共享身份命名空间] | [!UICONTROL 共享身份命名空间]用于表示由多个不同用户共享的单个设备。 |
| [!UICONTROL 用户身份命名空间] | [!UICONTROL 用户身份命名空间]用于表示已验证或已登录的共享设备用户。 |

## 共享设备UI

在Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL Identities]**，然后选择&#x200B;**[!UICONTROL Identity settings]**。

![identity-dashboard](../images/shared-device/identity-dashboard.png)

出现[!UICONTROL 共享设备设置]页面，为您提供一个界面来配置数据的共享设备设置。 默认情况下，共享设备设置处于禁用状态。

启用共享设备设置后，共享设备设置允许将来自同一设备不同用户的数据彼此分离。 此配置设置允许更简洁、更准确地表示身份图，其中同一设备的用户身份不会合并在一起。

选择&#x200B;**[!UICONTROL 启用]**&#x200B;以开始修改共享设备设置。

![enable-shared-device](../images/shared-device/enable-shared-device.png)

此时会显示[!UICONTROL 共享身份命名空间]和[!UICONTROL 用户身份命名空间]配置选项，允许您修改要使用的身份命名空间。

![set-namespaces](../images/shared-device/set-namespaces.png)

[!UICONTROL 共享身份] 名称包表示由多个不同用户使用的单个设备。此命名空间始终设置为&#x200B;**[!UICONTROL ECID]**，因为所有Platform用户都使用&#x200B;**[!UICONTROL ECID]**&#x200B;作为Web浏览器标识符。

![shared-identity-namespace](../images/shared-device/shared-identity-namespace.png)

[!UICONTROL 用户身份命名空间]允许您识别同一设备的不同用户，并阻止数据合并到同一身份图中。

![user-identity-namespace](../images/shared-device/user-identity-namespace.png)

选择&#x200B;**[!UICONTROL 用户身份命名空间]**&#x200B;搜索栏，然后输入身份命名空间或从下拉菜单中选择身份命名空间。

>[!TIP]
>
>应将[!UICONTROL 用户身份命名空间]映射到与最终用户登录ID对应的身份命名空间。 选项包括客户ID、电子邮件和经过哈希处理的电子邮件。

![电子邮件](../images/shared-device/emails.png)

配置[!UICONTROL 共享设备设置]后，选择&#x200B;**[!UICONTROL 保存]**。

![保存](../images/shared-device/save.png)

出现一个弹出窗口，提示您确认您的选择。 选择&#x200B;**[!UICONTROL 是]**&#x200B;以完成配置设置。

![confirm](../images/shared-device/confirm.png)
