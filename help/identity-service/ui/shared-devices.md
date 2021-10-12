---
keywords: Experience Platform；主页；热门主题；Identity Service;Identity Service；共享设备；共享设备
solution: Experience Platform
title: Shared Devices Overview (Beta)
topic-legacy: tutorial
description: “共享设备检测”可识别同一设备的经过身份验证的不同用户，从而允许在身份图中更准确地表示客户数据
hide: true
hidefromtoc: true
source-git-commit: 1cdab6ce71c748ae174700ce50f50b143e46b40f
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# 共享设备检测概述（测试版）

>[!IMPORTANT]
>
>The [!DNL Shared Device Detection] feature is in beta. Its features and documentation are subject to change.

Adobe Experience Platform [!DNL Identity Service]通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而帮助您更好地了解客户及其行为。

[!DNL Shared Device] refers to devices that are used by more than one individual. 共享设备的示例包括平板电脑、库计算机和网亭。 通过[!DNL Shared Device Detection]功能，可以阻止同一设备的不同用户合并到单个标识中，从而更准确地表示个人。

With [!DNL Shared Device Detection] you can:

* Create separate identity graphs for different users of the same device;
* 防止使用同一设备的不同个人混合数据；
* Generate a cleaner and more accurate view of your customers.

>[!TIP]
>
>必须在启用数据集的“配置文件”之前完成[!DNL Shared Device Detection]的配置，因为在[!DNL Identity Service]中生成图形后，您将无法再修订设置。

## 快速入门

使用[!DNL Shared Device Detection]需要了解所涉及的各种平台服务。 开始使用[!DNL Shared Device Detection]之前，请查阅以下服务的文档：

* [[!DNL Identity Service]](../home.md):通过跨设备和系统桥接身份，更好地了解各个客户及其行为。
   * [身份图查看器](./identity-graph-viewer.md):可视化身份图形查看器并与之进行交互，以便更好地了解客户身份如何拼合在一起，以及以何种方式拼合在一起。
   * [Identity namespaces](../namespaces.md): See the components of a fully qualified identity, and how identity namespaces allows you to distinguish the context and type of an identity.

### 术语

下表包含理解[!DNL Shared Device Detection]所必需的术语列表：

| 术语 | 定义 |
| --- | --- |
| 共享设备 | 共享设备是指多个个人使用的任何设备。 共享设备的示例包括平板电脑、库计算机和网亭。 |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] refers to a configuration setting that allows for data from different users of the same device to be separated from one another. |
| [!UICONTROL 共享身份命名空间] | A [!UICONTROL Shared Identity Namespace] is used to represent a single device that is shared by multiple different users. |
| [!UICONTROL 用户身份命名空间] | [!UICONTROL 用户身份命名空间]用于表示已验证或已登录的共享设备用户。 |

## 共享设备UI

在Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL Identities]**，然后选择&#x200B;**[!UICONTROL Identity settings]**。

![identity-dashboard](../images/shared-device/identity-dashboard.png)

The [!UICONTROL Shared device settings] page appears, providing you with an interface to configure shared device settings for your data. 默认情况下，共享设备设置处于禁用状态。

启用共享设备设置后，共享设备设置允许将来自同一设备不同用户的数据彼此分离。 此配置设置允许更简洁、更准确地表示身份图，其中同一设备的用户身份不会合并在一起。

选择&#x200B;**[!UICONTROL 启用]**&#x200B;以开始修改共享设备设置。

![enable-shared-device](../images/shared-device/enable-shared-device.png)

此时会显示[!UICONTROL 共享身份命名空间]和[!UICONTROL 用户身份命名空间]配置选项，允许您修改要使用的身份命名空间。

![set-namespaces](../images/shared-device/set-namespaces.png)

[!UICONTROL Shared Identity Namespace] represents a single device that is used by multiple different users. 此命名空间始终设置为&#x200B;**[!UICONTROL ECID]**，因为所有Platform用户都使用&#x200B;**[!UICONTROL ECID]**&#x200B;作为Web浏览器标识符。

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
