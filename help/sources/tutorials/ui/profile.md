---
keywords: Experience Platform；主页；热门主题；激活入站数据；填充用户档案；填充rtcp；填充统一用户档案
solution: Experience Platform
title: 激活入站源数据以在UI中填充客户用户档案
topic-legacy: overview
type: Tutorial
description: 来自源连接器的入站数据可用于丰富和填充实时客户用户档案数据。
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# 激活入站源数据以填充客户用户档案

来自源连接器的入站数据可用于丰富和填充[!DNL Real-time Customer Profile]数据。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成的基础](../../../xdm/schema/composition.md):了解XDM模式的基本构建基块，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

此外，本教程要求您已经创建并配置了源连接器。  [源连接器概述](../../home.md)中提供了有关在UI中创建不同连接器的列表教程。

## 填充[!DNL Real-time Customer Profile]数据

为了丰富客户用户档案,目标集的源模式必须兼容，才能在[!DNL Real-time Customer Profile]中使用。 兼容模式满足以下要求：

- 该模式至少具有一个指定为标识属性的属性。
- 模式具有定义为主标识的标识属性。
- 数据流内存在映射，其中主标识是目标属性。

在“源”工作区中，单击&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡以列表基本连接。 在显示的列表中，找到包含要用来填充用户档案的数据流的连接。 单击连接名称以访问其详细信息。

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

将显示连接的&#x200B;**[!UICONTROL Source activity]**&#x200B;屏幕，显示连接正在将源数据引入的数据集。 单击要为[!DNL Profile]启用的数据集的名称。

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

出现&#x200B;**[!UICONTROL Dataset activity]**&#x200B;屏幕。 屏幕右侧的&#x200B;**[!UICONTROL Properties]**&#x200B;列显示数据集的详细信息，包括&#x200B;**[!UICONTROL Profile]**&#x200B;开关和指向数据集附带的模式的链接。 单击模式的名称以视图其合成。

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

出现&#x200B;**[!UICONTROL Schema Editor]**，显示中心画布中模式的结构。 在画布中，选择要设置为主标识的字段。 在出现的&#x200B;**[!UICONTROL Field properties]**&#x200B;选项卡下，选中&#x200B;**[!UICONTROL Identity]**&#x200B;复选框，然后选择&#x200B;**[!UICONTROL Primary identity]**。 最后，选择相应的&#x200B;**[!UICONTROL Identity namespace]**，然后单击&#x200B;**[!UICONTROL Apply]**。

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

单击模式结构的顶级对象，将显示&#x200B;**[!UICONTROL Schema properties]**&#x200B;列。 通过切换&#x200B;**[!UICONTROL Profile]**&#x200B;交换机，为[!DNL Profile]启用模式。 单击&#x200B;**[!UICONTROL Save]**&#x200B;完成更改。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

既然[!DNL Profile]已启用模式，请返回至&#x200B;**[!UICONTROL Dataset activity]**&#x200B;屏幕，并通过单击&#x200B;**[!UICONTROL Properties]**&#x200B;列中的&#x200B;**[!UICONTROL Profile]**&#x200B;切换键为[!DNL Profile]启用数据集。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

在[!DNL Profile]启用模式和数据集后，摄取到该数据集中的数据现在也将填充客户用户档案。

>[!NOTE]
>
>[!DNL Profile]未使用最近启用的数据集中的现有数据。

## 后续步骤

通过本教程，您已成功激活[!DNL Profile]人口的入站数据。 有关详细信息，请参阅[[!DNL Real-time Customer Profile] overview](../../../profile/home.md)。
