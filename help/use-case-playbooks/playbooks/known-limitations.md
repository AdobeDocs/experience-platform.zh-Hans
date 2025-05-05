---
solution: Experience Platform
title: 行动手册的已知限制
description: 详细了解行动手册的已知问题和常见问题以及如何对其进行故障诊断
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: e24334bb4ac788770abe20ec2324efa1e64bc0e8
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%

---


# 已知限制 {#known-limitations}

了解在使用用例行动手册时如何排查错误，并了解正式发布版本的已知限制。

## 已知限制

在创建剧本实例并生成资产时，会显示一些已知限制。

* 对于生成的架构，如果在行动手册的一个实例中生成了一个架构，并且您编辑了该架构，那么如果启用行动手册的另一个实例，则不会&#x200B;*生成另一个架构。*&#x200B;相反，请继续使用您在实例中编辑的架构。

* 使用[数据感知功能](/help/use-case-playbooks/playbooks/data-awareness.md)将架构从启发型沙盒提升到开发沙盒时，您可能会看到类似于以下内容的一些错误：

![架构映射工作流中显示错误。](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

这是因为从架构生成的某些字段在要复制到其中的开发沙盒的架构中不存在。 查查那些栏位是什么。 然后，返回开发沙盒，您可以在其中执行以下操作：

* 创建一个包含这些字段的新字段组或者
* 在您的架构中包含一个标准的预定义字段组，其中包括缺少的字段。

在开发沙盒的架构中包含这些字段后，返回工作流以将架构字段从创意沙盒复制到开发沙盒。 错误现已消失。

有关更多信息，请观看以下视频以创建架构字段组。

>[!VIDEO](https://video.tv.adobe.com/v/3413600/?learn=on&captions=chi_hans)
