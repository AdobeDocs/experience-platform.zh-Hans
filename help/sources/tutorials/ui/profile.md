---
keywords: Experience Platform；主页；热门主题；激活入站数据；填充配置文件；填充rtcp；填充的统一配置文件
solution: Experience Platform
title: 激活入站源数据以在UI中填充客户配置文件
type: Tutorial
description: 来自源连接器的入站数据可用于扩充和填充实时客户资料数据。
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# 激活入站源数据以填充客户用户档案

来自源连接器的入站数据可用于丰富和填充您的 [!DNL Real-Time Customer Profile] 数据。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   - [架构组合的基础知识](../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   - [模式编辑器教程](../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

此外，本教程还要求您已创建并配置源连接器。  有关在UI中创建不同连接器的教程列表，请参阅 [源连接器概述](../../home.md).

## 填充 [!DNL Real-Time Customer Profile] 数据

为了扩充客户配置文件，目标数据集的源架构必须兼容才能在中使用 [!DNL Real-Time Customer Profile]. 兼容的架构满足以下要求：

- 架构至少具有一个指定为标识属性的属性。
- 架构具有定义为主标识的标识属性。
- 数据流中存在映射，其中主标识是目标属性。

在“源”工作区中，单击 **[!UICONTROL 浏览]** 选项卡，以列出基本连接。 在显示的列表中，找到包含要用来填充用户档案的数据流的连接。 单击连接的名称以访问其详细信息。

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

连接 **[!UICONTROL 源活动]** 屏幕，显示连接将源数据摄取到的数据集。 单击要为启用的数据集的名称 [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

的 **[!UICONTROL 数据集活动]** 屏幕。 的 **[!UICONTROL 属性]** 屏幕右侧的列会显示数据集的详细信息，并包含一个 **[!UICONTROL 用户档案]** 切换和指向数据集所遵守架构的链接。 单击架构的名称可查看其组成。

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

的 **[!UICONTROL 架构编辑器]** 显示中心画布中架构的结构。 在画布中，选择要设置为主标识的字段。 在 **[!UICONTROL 字段属性]** 选项卡，选择 **[!UICONTROL 身份]** 复选框，然后 **[!UICONTROL 主标识]**. 最后，选择适当的 **[!UICONTROL 身份命名空间]**，然后单击 **[!UICONTROL 应用]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

单击架构结构的顶级对象和 **[!UICONTROL 架构属性]** 列。 为启用架构 [!DNL Profile] 切换 **[!UICONTROL 用户档案]** 切换。 单击 **[!UICONTROL 保存]** 完成更改。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

现在，已为 [!DNL Profile]，返回到 **[!UICONTROL 数据集活动]** 屏幕，并为 [!DNL Profile] 单击 **[!UICONTROL 用户档案]** 在 **[!UICONTROL 属性]** 列。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

启用架构和数据集后， [!DNL Profile]，则摄取到该数据集的数据现在也会填充客户用户档案。

>[!NOTE]
>
>最近启用的数据集中的现有数据不会被 [!DNL Profile].

## 后续步骤

通过阅读本教程，您已成功激活 [!DNL Profile] 人口。 有关更多信息，请参阅 [[!DNL Real-Time Customer Profile] 概述](../../../profile/home.md).
