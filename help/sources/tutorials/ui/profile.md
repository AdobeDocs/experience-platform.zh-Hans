---
keywords: Experience Platform；主页；热门主题；激活入站数据；填充配置文件；填充rtcp；填充的统一配置文件
solution: Experience Platform
title: 激活入站源数据以在UI中填充客户配置文件
type: Tutorial
description: 来自您的源连接器的入站数据可用于扩充和填充您的Real-time Customer Profile数据。
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# 激活入站源数据以填充客户配置文件

来自源连接器的入站数据可用于扩充和填充 [!DNL Real-Time Customer Profile] 数据。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

- [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   - [模式组合基础](../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   - [架构编辑器教程](../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

此外，本教程要求您已创建和配置源连接器。  有关在UI中创建不同连接器的教程列表，请参阅 [源连接器概述](../../home.md).

## 填充您的 [!DNL Real-Time Customer Profile] 数据

为了扩充客户用户档案，目标数据集的源架构必须兼容以用于 [!DNL Real-Time Customer Profile]. 兼容模式满足以下要求：

- 架构至少有一个指定为标识属性的属性。
- 架构具有被定义为主标识的标识属性。
- 数据流内存在映射，其中主标识为目标属性。

在源工作区中，单击 **[!UICONTROL 浏览]** 选项卡，列出基本连接。 在显示的列表中，查找包含要填充用户档案的数据流的连接。 单击连接的名称可访问其详细信息。

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

连接的 **[!UICONTROL 源活动]** 屏幕，显示连接正在将源数据摄取到的数据集。 单击要为其启用的数据集的名称 [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

此 **[!UICONTROL 数据集活动]** 屏幕。 此 **[!UICONTROL 属性]** 屏幕右侧的列显示了数据集的详细信息，并包括 **[!UICONTROL 个人资料]** 切换并链接到数据集所遵循的架构。 单击方案的名称可查看其组成。

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

此 **[!UICONTROL 架构编辑器]** 显示，在中心画布中显示架构的结构。 在画布中，选择要设置为主标识的字段。 在 **[!UICONTROL 字段属性]** 选项卡，选择 **[!UICONTROL 身份]** 复选框，然后 **[!UICONTROL 主要身份]**. 最后，选择适当的 **[!UICONTROL 身份命名空间]**，然后单击 **[!UICONTROL 应用]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

单击架构结构的顶级对象，然后 **[!UICONTROL 架构属性]** 列显示。 为以下项启用架构 [!DNL Profile] 通过切换 **[!UICONTROL 个人资料]** 切换。 单击 **[!UICONTROL 保存]** 以完成更改。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

现在已为以下项启用架构： [!DNL Profile]，返回到 **[!UICONTROL 数据集活动]** 屏幕并启用数据集 [!DNL Profile] 单击 **[!UICONTROL 个人资料]** 在中切换 **[!UICONTROL 属性]** 列。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

架构和数据集均启用后 [!DNL Profile]，摄取到该数据集中的数据现在也将填充客户档案。

>[!NOTE]
>
>最近启用的数据集中的现有数据不由使用 [!DNL Profile].

## 后续步骤

通过学习本教程，您已成功激活的集客数据 [!DNL Profile] 群体。 欲了解更多信息，请参见 [[!DNL Real-Time Customer Profile] 概述](../../../profile/home.md).
