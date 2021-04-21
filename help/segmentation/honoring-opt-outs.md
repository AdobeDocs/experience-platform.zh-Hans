---
keywords: Experience Platform；主页；热门主题；选择退出；分段；分段服务；分段服务；荣誉退出；选择退出选择退出；选择退出；
solution: Experience Platform
title: 支持区段中的退出请求
topic-legacy: overview
description: Adobe Experience Platform允许您的客户发送有关在实时客户用户档案中使用和存储其数据的选择退出请求]。 这些选择退出请求是加利福尼亚消费者隐私法(CCPA)的一部分，CCPA为加州居民提供访问和删除其个人数据以及了解其个人数据是出售还是披露（以及向谁）的权利。
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# 支持区段中的退出请求

Adobe Experience Platform允许您的客户发送关于[!DNL Real-time Customer Profile]中数据使用和存储的退出请求。 这些选择退出请求是[!DNL California Consumer Privacy Act](CCPA)的一部分，CCPA为加利福尼亚州居民提供了访问和删除其个人数据以及了解其个人数据是出售还是披露（以及向谁）的权利。

客户选择退出后，在为营销活动生成受众时，贵组织应遵守这些选择退出的规定。 本文档介绍了有关支持退出请求的重要详细信息。

## 入门指南

支持退出请求需要了解所涉及的各种[!DNL Adobe Experience Platform]服务。 在处理退出请求之前，请查看以下服务的文档：

- [[!DNL Real-time Customer Profile]](../profile/home.md):根据来自多个来源的汇总数据实时提供统一的客户用户档案。
- [[!DNL Adobe Experience Platform Segmentation Service]](./home.md):允许您根据数据构建受众 [!DNL Real-time Customer Profile] 区段。
- [[!DNL Experience Data Model (XDM)]](../xdm/home.md):平台通过该标准化框架组织客户体验数据。
- [[!DNL Adobe Experience Platform Privacy Service]](../privacy-service/home.md):帮助组织自动遵守与内部客户数据相关的数据隐私法规 [!DNL Platform]。

## 选择退出混音

为了满足CCPA退出请求，作为合并模式一部分的模式之一必须包含必需的[!DNL Experience Data Model](XDM)退出字段。 有两种混音可用于向模式添加退出字段，下面各节将更详细地介绍它们：

- [用户档案隐私](#profile-privacy):用于捕获不同的退出类型（常规或销售/共享）。
- [用户档案首选项详细信息](#profile-preferences-details):用于捕获特定XDM渠道的退出请求。

有关如何向模式添加混音的分步说明，请参阅以下XDM文档中的“添加混音”部分：
- [模式注册表API教程](../xdm/api/getting-started.md)。:使用模式 Registry API构建模式。
- [模式编辑器教程](../xdm/tutorials/create-schema-ui.md):使用平台用户界面构建模式。

下面是一个示例图像，其中显示了添加到用户界面中的模式的选择退出混音：

![](images/opt-outs/opt-out-mixins-user-interface.png)

以下各节将更详细地介绍每个混音的结构，以及它们对模式所贡献的字段。

### [!DNL Profile Privacy] {#profile-privacy}

[!DNL Profile Privacy] mixin允许您捕获来自客户的两种CCPA选择退出请求：

1. 一般退出
2. 销售/共享选择退出

![](images/opt-outs/profile-privacy.png)

[!DNL Profile Privacy] mixin包含以下字段：

- 隐私退出(`privacyOptOuts`):包含退出对象列表的数组。
- 退出类型(`optOutType`):选择退出的类型。 此字段是具有两个可能值的枚举：
   - 常规退出(`general_opt_out`)
   - 销售共享退出(`sales_sharing_opt_out`)
- 退出值(`optOutValue`):根据指定的退出类型，退出的活动状态，也称为退出信号的值。 此字段是具有四个可能值的枚举：
   - 未提供(`not_provided`):尚未提供退出请求。
   - 待验证(`pending`):退出请求正在等待验证。
   - 退出(`out`):客户已选择退出。
   - 选择加入(`in`):客户已选择加入。
- 退出时间戳(`timestamp`):接收的退出信号的时间戳。

要视图[!DNL Profile Privacy]混音的完整结构，请参阅[ XDM公共GitHub存储库](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json)或使用平台UI预览混音。

### [!DNL Profile Preferences Details] {#profile-preferences-details}

[!DNL Profile Preferences Details] mixin提供了几个表示客户用户档案偏好的字段(如电子邮件格式、首选语言和时区)。 此混合中包含的字段之一OptInOut(`optInOut`)允许为各个渠道设置退出值。

![](images/opt-outs/profile-preferences-details.png)

[!DNL Profile Preferences Details] mixin包含与退出相关的以下字段：

- OptInOut(`optInOut`):一个对象，其中每个键代表通信渠道的有效且已知的URI以及每个渠道的退出活动状态。 每个渠道可能具有以下四种可能值之一：
   - 未提供(`not_provided`):尚未为此渠道提供退出请求。
   - 待验证(`pending`):此渠道的退出请求正在等待验证。
   - 退出(`out`):客户已选择退出此渠道。
   - 选择加入(`in`):客户已选择加入此渠道。
- 全局退出(`globalOptout`):一个布尔值，当设置为true时，它为用户档案设置全局退出覆盖。 此字段的默认值为false。

以下示例JSON重点说明了OptInOut对象如何针对不同通信渠道捕获多个退出信号：

```json
{
  "xdm:optInOut": {
    "https://ns.adobe.com/xdm/channels/email": "pending",
    "https://ns.adobe.com/xdm/channels/phone": "out",
    "https://ns.adobe.com/xdm/channels/sms": "in",
    "https://ns.adobe.com/xdm/channels/fax": "not_provided",
    "https://ns.adobe.com/xdm/channels/direct-mail": "not_provided",
    "https://ns.adobe.com/xdm/channels/apns": "not_provided",
    "xdm:globalOptout": false
  }
}
```

要视图“用户档案首选项详细信息”混音的完整结构，请访问[ XDM公共GitHub存储库](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json)或使用[!DNL Platform] UI预览混音。

## 处理分段中的退出功能

为了确保在区段中不包括带有CCPA退出标志的用户档案，必须向现有区段添加特殊字段，或在区段创建过程中包括特殊字段。

以下部分说明如何为两种类型的退出标记添加相应的字段：
1. 一般退出
2. 销售/共享选择退出

### 一般退出

[!DNL Segmentation] 自动接受包含“”标志的[!UICONTROL General Opt-Out]所有用户档案，这意味着默认情况下，这些用户档案不会包括在受众或导出中。但是，最好添加相应的字段，以确保在受众和营销活动中不包括选择退出的用户档案。

可通过添加&#x200B;**[!UICONTROL Privacy Opt-Outs]**&#x200B;属性，使用用户界面完成此操作。 在此实例中，区段设置为仅包括已选择的群体(即，他们的用户档案上没有一般选择退出标志)。 为此，请声明“[!UICONTROL Opt-Out Type]”等于“[!UICONTROL General Opt-Out]”，“[!UICONTROL Opt-Out Value]”等于“[!UICONTROL Opt-in]”。

![](images/opt-outs/segment-general-opt-out.png)

### 销售/共享选择退出

如果用户的用户档案上设置了销售/共享退出标志，则此用户档案不应再用于任何区段创建或营销活动。 为确保执行此标志，“[!UICONTROL Opt-Out Type]”必须等于“[!UICONTROL Sales Sharing Opt-Out]”，而“[!UICONTROL Opt-Out Value]”必须等于“[!UICONTROL Opt-in]”。

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## 后续步骤

有关分段的详细信息(包括通过API和用户界面使用段定义和受众)，请首先阅读[分段概述](./home.md)。

要进一步了解[!DNL Platform]中的数据隐私，包括[!DNL Privacy Service]如何帮助促进自动遵守法律和组织隐私法规，请参阅[[!DNL Privacy Service]](../privacy-service/home.md)上的文档。
