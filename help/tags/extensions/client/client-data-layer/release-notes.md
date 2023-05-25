---
title: Adobe客户端数据层扩展的发行说明
description: Adobe Experience Platform中的Adobe客户端数据层标记扩展的最新发行说明。
exl-id: 8fa3a210-6c85-4162-84cf-15c6e3cfcb9e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 4%

---

# Adobe客户端数据层扩展发行说明

## 版本 2.0.2

* 加载ACDL核心库（版本2.0.2）
* ACDL核心库版本2.0.0移除了利用event.beforeState和event.afterState的功能。 因此，我们修改了这些对象以始终返回空对象。 迁移到此版本时，需要更新依赖此功能的实施。

## 版本 1.1.3

* 加载ACDL核心库（版本1.1.3）

## 版本 1.1.2

初始版本中的扩展提供了以下功能：

* 加载ACDL核心库（版本1.1.1）
* 重命名Adobe数据层
* 事件：
   * 收听所有事件
   * 侦听所有推送的数据
   * 侦听推送的特定事件
   * 所有事件都可以在不同范围中侦听
* 数据元素:
   * 计算状态：全局或特定状态
   * 数据层大小
* 操作:
   * 重置数据层大小（保持最新的计算状态）
   * 将对象推送到Data Layer
