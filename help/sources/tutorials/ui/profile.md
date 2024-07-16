---
keywords: Experience Platform；主页；热门主题；激活入站数据；填充配置文件；填充rtcp；填充的统一配置文件
solution: Experience Platform
title: 激活入站Source数据以在UI中填充客户配置文件
type: Tutorial
description: 来自您的源连接器的入站数据可用于扩充和填充您的Real-time Customer Profile数据。
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# 激活入站源数据以填充客户配置文件

来自源连接器的入站数据可用于扩充和填充您的[!DNL Real-Time Customer Profile]数据。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   - [架构组合的基础知识](../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   - [架构编辑器教程](../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

此外，本教程要求您已创建和配置源连接器。  有关在UI中创建不同连接器的教程列表，请参阅[源连接器概述](../../home.md)。

## 填充您的[!DNL Real-Time Customer Profile]数据

为了丰富客户配置文件，目标数据集的源架构必须兼容以在[!DNL Real-Time Customer Profile]中使用。 兼容的架构满足以下要求：

- 架构至少有一个指定为标识属性的属性。
- 架构具有定义为主标识的标识属性。
- 数据流内存在映射，其中主标识是目标属性。

在源工作区中，单击&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡列出您的基本连接。 在显示的列表中，查找包含要填充用户档案的数据流的连接。 单击连接的名称可访问其详细信息。

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

此时将显示连接的&#x200B;**[!UICONTROL Source活动]**&#x200B;屏幕，其中显示该连接正在将源数据摄取到的数据集。 单击要为[!DNL Profile]启用的数据集的名称。

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

将显示&#x200B;**[!UICONTROL 数据集活动]**&#x200B;屏幕。 屏幕右侧的&#x200B;**[!UICONTROL Properties]**&#x200B;列显示数据集的详细信息，并包含一个&#x200B;**[!UICONTROL Profile]**&#x200B;开关和一个指向数据集所坚持的架构的链接。 单击方案的名称可查看其构成。

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

出现&#x200B;**[!UICONTROL 架构编辑器]**，其中显示中心画布中架构的结构。 在画布中，选择要设置为主标识的字段。 在出现的&#x200B;**[!UICONTROL 字段属性]**&#x200B;选项卡下，选中&#x200B;**[!UICONTROL 标识]**&#x200B;复选框，然后选择&#x200B;**[!UICONTROL 主标识]**。 最后，选择适当的&#x200B;**[!UICONTROL 身份命名空间]**，然后单击&#x200B;**[!UICONTROL 应用]**。

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

单击架构结构的顶级对象，将显示&#x200B;**[!UICONTROL 架构属性]**&#x200B;列。 通过切换&#x200B;**[!UICONTROL 配置文件]**&#x200B;开关来启用[!DNL Profile]的架构。 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以完成更改。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

现在该架构已为[!DNL Profile]启用，请返回到&#x200B;**[!UICONTROL 数据集活动]**&#x200B;屏幕，并通过在&#x200B;**[!UICONTROL 属性]**&#x200B;列中单击&#x200B;**[!UICONTROL 配置文件]**&#x200B;切换来为[!DNL Profile]启用数据集。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

为[!DNL Profile]启用架构和数据集后，摄取到该数据集中的数据现在也将填充客户配置文件。

>[!NOTE]
>
>[!DNL Profile]不会使用最近启用的数据集中的现有数据。

## 后续步骤

通过学习本教程，您已成功激活[!DNL Profile]群体的入站数据。 有关详细信息，请参阅[[!DNL Real-Time Customer Profile] 概述](../../../profile/home.md)。
