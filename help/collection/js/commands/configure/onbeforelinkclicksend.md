---
title: onBeforeLinkClickSend
description: 在发送链接跟踪数据之前运行的回调。
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>此回调已弃用。 请改用[`clickCollection.filterClickDetails`](clickcollection.md)。

`onBeforeLinkClickSend`回调允许您注册JavaScript函数，该函数可以更改您在将数据发送到Adobe之前发送的链接跟踪数据。 它允许您处理`xdm`或`data`对象，包括添加、编辑或删除元素的功能。 您还可以有条件地完全取消发送数据，例如使用检测到的客户端机器人流量。

此回调仅在启用[`clickCollectionEnabled`](clickcollectionenabled.md)且`filterClickDetails`不包含注册的函数时运行。

如果[`onBeforeEventSend`](onbeforeeventsend.md)和`onBeforeLinkClickSend`都包含已注册的函数，则首先执行`onBeforeLinkClickSend`。

>[!WARNING]
>
>此回调允许使用自定义代码。 如果您包含在回调中的任意代码引发未捕获的异常，则对事件的处理将中止。 数据不会发送到Adobe。

## `onBeforeLinkClickSend` 和 `filterClickDetails`

[`clickCollection.filterClickDetails`](clickcollection.md)回调旨在替换`onBeforeLinkClickSend`。 Adobe强烈建议不要将回调函数同时分配给两者。 如果将回调函数分配给`filterClickDetails`和`onBeforeLinkClickSend`，则库将使用以下逻辑：

* 只有`filterClickDetails`执行；`onBeforeLinkClickSend`不执行。
* 事件分组`clickCollection.eventGroupingEnabled`不起作用。
