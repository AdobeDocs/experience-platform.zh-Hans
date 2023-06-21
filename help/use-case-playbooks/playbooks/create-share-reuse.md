---
solution: Experience Platform
title: 创建、共享和重用剧本实例
description: 了解如何创建、共享和重用剧本实例以完成您的营销用例。
badgeBeta: label="Beta" type="Informative"
source-git-commit: e61e200b148e4d17041b3711bd63c796a44b05c8
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---


# （测试版）创建、共享和重用剧本实例

>[!AVAILABILITY]
>
>此功能当前为测试版，并非对所有用户都可用。 文档和功能可能会发生变化。

要使用行动手册，请导航到 **[!UICONTROL 用例行动手册] > [!UICONTROL 行动手册]**. 浏览并使用页面上的各种搜索和筛选选项，选择并开始使用特定的行动手册。

## 创建行动手册实例 {#create-playbook-instance}

在创建行动手册实例之前，请探索可用的行动手册，以 [探索适合您的剧本](/help/use-case-playbooks/playbooks/discover.md). 当您准备好继续使用剧本并创建实例时，请选择 **[!UICONTROL 创建实例]** 以继续编写剧本并生成技术资产。

![创建剧本实例。](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

此操作会生成多个资源，供您用于实现行动手册中所述的用例。

![启用后生成的资产的剧本视图。](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### 使用配置控件编辑实例名称和说明 {#edit-instance-metadata}

根据剧本创建实例后，您可以对其进行个性化设置，以将其与从同一剧本创建的其他实例区分开来。 选择配置控件，如下所示。 编辑名称、说明和注释，然后选择 **[!UICONTROL 保存]** 等你完事了。

![编辑实例的名称和描述。](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### 了解生成的资源 {#understand-assets}

>[!IMPORTANT]
>
>不用担心！ 这是一个安全的实验空间，你无法破坏任何东西。 目前还没有与您创建的任何资产关联的数据。 您必须先摄取数据才能实现用例。

请务必了解，生成的资源因您启用的用例而异：

* 为不同类型的行动手册生成了不同的资产。 这些资源是专门为通过行动手册实现的用例创建的。 例如，行动手册生成架构、区段、历程和消息。 另一个行动手册生成架构、区段和将数据激活到的目标。
* 资产本身因行动手册而异。 例如，对于 **[!UICONTROL 向来宾发送生日消息]** 剧本，创建的受众具有规则 `birthday=today AND year=any`.

举例来说，对于 **[!UICONTROL 放弃的购物车：商品]** 行动手册，您可以看到已创建特定历程，其中包括为此用例创建的消息。

![根据用例剧本创建的历程。](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### 使用和编辑生成的资源 {#use-and-edit-assets}

在您探索创建行动手册实例后生成的资源时，您可以编辑创建的任何资源。

如果您或您团队中的某人创建了剧本的其他实例，则会保留编辑过的资产，并为剧本的新实例创建新资产。

上述行为适用于已创建的所有资产，但架构除外。 对于架构，在创建新的剧本实例时不会创建新架构，因此您将使用新创建的实例中剧本另一实例的已编辑架构。

>[!TIP]
>
>在开发沙盒中测试，并在准备就绪后移至生产环境。
>
>生成对象后，您可以通过添加数据继续在开发沙盒中测试。 您可以根据需要在开发沙盒中测试资产，并在准备就绪后在生产沙盒中复制资产逻辑（区段定义、历程、架构等）。

## 重用行动手册 {#reuse-playbooks}

通过创建同一行动手册的多个实例，您可以稍后实施相同的用例，而无需修改之前实施用例的详细信息。

## 与其他团队成员共享行动手册和生成的资产 {#share-playbook}

您可以与其他团队成员共享生成的实例和资产。 为此，请复制浏览器中的URL链接并与您的团队共享，以便他们大致了解生成的资源。

![用例剧本视图中突出显示的URL。](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## 后续步骤 {#next-steps}

通过阅读本指南和关于为您发现正确剧本的指南，您现在知道如何解释剧本的各个部分，以及如何使用在创建剧本实例后生成的资源。

接下来，您可以浏览行动手册目录，找到适合您用例的行动手册，并阅读 [疑难解答指南](/help/use-case-playbooks/playbooks/troubleshooting.md) 如果您遇到任何问题。