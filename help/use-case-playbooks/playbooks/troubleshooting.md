---
solution: Experience Platform
title: 行动手册的已知限制和疑难解答
description: 详细了解行动手册的已知问题和常见问题以及如何对其进行故障诊断
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: d6be5d3e21ea924ff98c400b972709b1f60c25eb
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 2%

---


# 故障排除和已知限制 {#troubleshooting-known-limitations}

## 故障排除 {#troubleshooting}

### 未配置Adobe Journey Optimizer表面

在创建行动手册的实例时，您可能会看到下面显示的消息。

![疑难解答](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

这是因为Journey Optimizer行动手册为电子邮件、推送和短信渠道创建消息。 阅读 [入门](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) 指导您配置不同的表面。

### 状态 *失败* 创建新实例时

如果您在尝试创建实例时看到失败消息，这可能是因为管理员未向您授予所需的用户权限。 行动手册包含大量不同的资产，您的用户需要拥有创建这些资产的权限，才能成功创建行动手册的实例。 请参阅 [权限](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) 部分，了解如何设置权限。

## 已知限制

在创建剧本实例并生成资产时，会显示一些已知限制。

* 对于生成的架构，如果在剧本的一个实例中生成了一个架构，并且您编辑了该架构，则另外生成了一个架构 *不会* 如果启用剧本的另一个实例，则会生成。 相反，请继续使用您在实例中编辑的架构。

* 使用时 [数据感知功能](/help/use-case-playbooks/playbooks/data-awareness.md) 要将架构从启发型沙盒提升到开发沙盒，您可能会看到一些与以下类似的错误：

![schema-errors](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png)

这是因为从架构生成的某些字段在要复制到其中的开发沙盒的架构中不存在。 查查那些栏位是什么。 然后，返回开发沙盒，您可以在其中执行以下操作：

* 创建一个包含这些字段的新字段组或者
* 在您的架构中包含一个标准的预定义字段组，其中包括缺少的字段。

在开发沙盒的架构中包含这些字段后，返回工作流以将架构字段从创意沙盒复制到开发沙盒。 错误现已消失。

有关更多信息，请观看以下视频以创建架构字段组。

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
