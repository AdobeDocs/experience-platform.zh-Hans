---
title: Adobe客户端数据层扩展的发行说明
description: Adobe Experience Platform中Adobe客户端数据层标记扩展的最新发行说明。
exl-id: 8fa3a210-6c85-4162-84cf-15c6e3cfcb9e
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 4%

---

# Adobe客户端数据层扩展发行说明

## 版本 2.0.2

* 加载ACDL核心库（版本2.0.2）
* ACDL核心库版本2.0.0删除了利用event.beforeState和event.afterState的功能。 因此，我们修改了这些对象，以始终返回空对象。 转到此版本时，需要更新依赖此功能的实施。

## 版本 1.1.3

* Loading the ACDL core library (version 1.1.3)

## 版本 1.1.2

扩展在初始版本时提供了以下功能：

* Loading the ACDL core library (version 1.1.1)
* 重命名Adobe数据层
* 事件：
   * 侦听所有事件
   * 侦听所有推送的数据
   * Listening to a specific event pushed
   * 所有事件都可以在不同的范围中侦听
* 数据元素:
   * 计算状态：全局或特定状态
   * Data Layer Size
* 操作:
   * Reset the data layer size (keeping the latest Computed State)
   * Push object to the Data Layer
