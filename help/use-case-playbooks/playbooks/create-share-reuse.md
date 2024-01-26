---
solution: Experience Platform
title: 创建、共享和重用战术手册实例
description: 了解如何创建、共享和重用战术手册实例来完成您的营销用例。
badgeBeta: label="Beta 版" type="Informative"
exl-id: b06d8186-c41f-4150-bac4-69c616151ef9
source-git-commit: f477cb4d410058b8bf2692a7afde70bf23a5aac7
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 97%

---

# (Beta) 创建、共享和重用战术手册实例

>[!AVAILABILITY]
>
>此功能当前正在接受测试，无法为所有用户提供。文档和功能可能会发生变化。

要使用战术手册，请导航至&#x200B;**[!UICONTROL 用例战术手册] > [!UICONTROL 战术手册]**。浏览并使用页面上的各种搜索和过滤选项来选择并开始使用特定的战术手册。

## 创建一个战术手册实例。 {#create-playbook-instance}

>[!CONTEXTUALHELP]
>id="platform_playbooks_create"
>title="创建实例"
>abstract="生成要在历程或激活场景中使用的资源（如历程、受众、架构或目标）列表。"

在创建战术手册实例之前，请探索可用的战术手册以[发现适合您的战术手册](/help/use-case-playbooks/playbooks/discover.md)。当您准备好继续使用战术手册并创建实例时，请选择&#x200B;**[!UICONTROL 创建实例]**，以继续执行战术手册，并生成技术资产。

![创建一个战术手册实例。](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

此操作会生成多个资产，供您用来实现战术手册中描述的用例。

![启用后生成的资产的战术手册视图。](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### 使用配置控件编辑实例名称和描述 {#edit-instance-metadata}

基于战术手册创建实例后，您可以对其进行个性化设置，以将其与从同一战术手册创建的其他实例区分开来。选择配置控件，如下所示。编辑名称、描述和注释，并在完成时选择&#x200B;**[!UICONTROL 保存]**。

![编辑实例的名称和描述。](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### 了解生成的资产 {#understand-assets}

>[!IMPORTANT]
>
>不用担心！这是一个安全的试验空间，您不会造成任何破坏。目前还没有与您创建的任何资产关联的数据。您必须首先摄取数据才能实现用例。

您需要知道，所生成的资产根据您启用的用例而有所不同：

* 不同类型的战术手册会生成不同的资产。这些资产是专门为通过战术手册实现的用例创建的。例如，战术手册会生成架构、区段、历程和消息。另一个战术手册会生成一个架构、一个区段和一个要激活数据的目标。
* 不同战术手册之间的资产本身有所不同。例如，对于&#x200B;**[!UICONTROL 向宾客发送生日消息]**&#x200B;战术手册，创建的受众具有规则 `birthday=today AND year=any`。

为了举例说明，对于&#x200B;**[!UICONTROL 已放弃购物车：商品]**&#x200B;战术手册中，您可以看到创建了一个特定的历程，其中包括为此用例创建的消息。

![根据用例战术手册创建的历程。](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### 使用和编辑生成的资源 {#use-and-edit-assets}

当您探索创建战术手册实例后生成的资产时，您可以编辑创建的任何资产。

如果您或您团队中的某人创建了该战术手册的另一个实例，则会保留已编辑的资产，并会为战术手册的新实例创建新资产。

上述操作适用于所创建的所有资产（架构除外）。对于架构，在创建战术手册的新实例时不会创建新架构，因此您会在新创建的实例中使用来自战术手册的另一个实例的已编辑架构。

>[!TIP]
>
>在开发沙盒中进行测试，准备就绪后即可转移到生产环境。
>
>生成对象后，您可以通过添加数据继续在开发沙盒中进行测试。您可以在开发沙盒中根据需要测试资产，并且在准备好后可以在生产沙盒中复制资产逻辑（区段定义、历程、架构等）。

## 重用战术手册 {#reuse-playbooks}

通过创建同一战术手册的多个实例，您以后可以实施相同的用例，而无需修改用例先前实施的详细信息。

## 与其他团队成员共享战术手册和生成的资产 {#share-playbook}

您可以与其他团队成员共享生成的实例和资产。若要这样做，请在浏览器中复制 URL 链接并与您的团队共享，以便他们了解生成的资产。

![在用例战术手册视图中突出显示的 URL。](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## 后续步骤 {#next-steps}

通过阅读本指南以及有关找到适合您的战术手册的指南，您现在知道如何解读战术手册的各个部分，以及如何使用创建战术手册实例后生成的资产。

接下来，您可以浏览战术手册目录以找到适合您的用例的战术手册，如果遇到任何问题，可阅读[故障排除指南](/help/use-case-playbooks/playbooks/troubleshooting.md)。
