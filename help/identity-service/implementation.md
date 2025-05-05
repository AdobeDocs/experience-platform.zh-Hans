---
title: Identity Service实施指南
description: 了解提供给Adobe Experience Platform的数据在Identity Service用于构建身份图之前如何进行处理。
exl-id: c961bbf6-6b46-470f-a671-93ff4173876c
source-git-commit: 4ba25ed684ff126ab1c4f1a33e6503f0342e8720
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# Identity Service实施指南

本文档提供了有关向Adobe Experience Platform提供的数据在Identity Service用于为给定客户构建身份图之前如何进行处理的信息。

## 决定标识字段

根据您的企业数据收集策略，标记为身份的数据字段将确定您的身份映射中包含哪些数据。 要实现Experience Platform的最大优势和最全面的客户身份，您应该上传在线和离线数据。

* 在线数据是描述在线状态和行为的数据，如用户名和电子邮件地址。

* 离线数据是指与在线状态不直接相关的数据，例如CRM系统的ID。 此类数据使您的身份更加稳健，并支持不同系统中的数据聚合。

## 创建其他身份命名空间

虽然Experience Platform提供了各种标准命名空间，但您可能需要创建其他命名空间来对您的身份正确分类。 有关详细信息，请阅读[为您的组织](./features/namespaces.md)创建自定义命名空间的指南。

>[!NOTE]
>
>标识命名空间是标识的限定符。 因此，创建命名空间后，便无法删除该命名空间。

## 包括体验数据模型(XDM)中的身份数据

作为Experience Platform组织客户数据的标准化框架，Experience Data Model (XDM)允许跨Experience Platform共享和理解数据以及与Experience Platform交互的其他服务。 有关详细信息，请参阅[XDM系统概述](../xdm/home.md)。

记录架构和时序架构均提供了包含身份数据的方法。 在摄取数据时，如果发现来自不同命名空间的数据片段共享共同的身份数据，则身份图将在这些片段之间创建新的关系。

## 将XDM字段标记为身份

实现记录或时间序列XDM类的架构中任何类型为`string`的字段都可以标记为标识字段。 因此，摄取到该字段中的所有数据都将被视为身份数据。

如果标识字段共享公共PII数据，则还允许关联标识。
例如，通过将电话号码字段标记为身份字段，Identity Service会自动绘制与其他使用相同电话号码的个人的关系图形。

>[!NOTE]
>
>* 数组字段和映射类型字段不受支持，并且无法标记为标识字段。
>* 在标记字段时，会提供生成的身份命名空间。
>* 只要某个字段不在数组对象下，该字段就可以标记为标识。

有关详细信息，请阅读[在UI中定义标识字段的指南](../xdm/ui/fields/identity.md)。

## 为Identity服务配置数据集

在流式摄取过程中，Identity Service会自动从记录和时间序列数据中提取身份数据。 但是，在摄取数据之前，必须为Identity Service启用该功能。 有关详细信息，请阅读有关[使用API为Real-time Customer Profile和Identity服务配置数据集](../profile/tutorials/dataset-configuration.md)的教程。

## 将数据摄取到Identity服务

身份服务使用通过[批处理摄取](../ingestion/batch-ingestion/overview.md)或[流式摄取](../ingestion/streaming-ingestion/overview.md)发送到Experience Platform的符合XDM的数据。

以下视频旨在支持您了解Identity Service。 此视频介绍如何将数据字段标记为身份，以及在引入身份数据后，如何验证该数据是否已写入Adobe Experience Platform Identity Service专用图。

>[!WARNING]
>
>以下视频中显示的Experience PlatformUI已过期。 请参阅文档以了解最新的UI屏幕截图和功能。

>[!VIDEO](https://video.tv.adobe.com/v/31671?quality=12&learn=on&captions=chi_hans)
