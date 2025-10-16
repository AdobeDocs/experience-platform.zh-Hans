---
title: 毛细管流事件概述
description: 了解如何将数据从Capillary流式传输到Experience Platform。
badge: Beta 版
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: 428aed259343f56a2bf493b40ff2388340fffb7b
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>[!DNL Capillary Streaming Events]源为测试版。 有关使用测试版标记源的更多信息，请阅读源概述中的[条款和条件](../../home.md#terms-and-conditions)。

[!DNL Capillary Technologies]是一个领先的忠诚度和参与平台，受到全球300多个品牌的信任。 使用[!DNL Capillary Streaming Events]源使您的企业能够无缝地将[!DNL Capillary]中的客户个人资料、忠诚度数据和事务性事件流式传输到Adobe Experience Platform中。 连接您的[!DNL Capillary]源以启用实时个性化、高级受众分段和全渠道营销活动编排。

通过将[!DNL Capillary]与Experience Platform集成，您可以：

* 实时同步&#x200B;**会员积分、层级和奖励**。
* 将&#x200B;**事务性数据**&#x200B;发送到Experience Platform以进行分析和激活。
* 利用Real-Time CDP、Experience Platform和Adobe Journey Optimizer进行分段、历程编排和个性化。

## 先决条件

在将[!DNL Capillary]连接到Adobe Experience Platform之前，请确保您具备以下条件：

* 有效的&#x200B;**Adobe组织ID**&#x200B;以及对已启用的Experience Platform沙盒的访问权限。
* 若要将您的&#x200B;**[!UICONTROL 帐户连接到Experience Platform，您必须同时为您的帐户启用]**&#x200B;查看源&#x200B;**[!UICONTROL 和]**&#x200B;管理源[!DNL Capillary]权限。 请联系您的产品管理员以获取必要的权限。 有关详细信息，请阅读[访问控制UI指南](../../../access-control/ui/overview.md)。

### 创建架构

您必须创建体验数据模型(XDM)架构以描述一个数据集，该数据集可以存储可能从[!DNL Capillary]发送的字段和数据类型。

1. 登录到Adobe Experience Platform，然后通过贵组织的登录信息访问Experience Platform。
2. 在左侧导航面板中，选择&#x200B;**[!UICONTROL 架构]**&#x200B;以打开[!UICONTROL 架构]工作区。
3. 选择右上角的&#x200B;**[!UICONTROL 创建架构]**。
4. 在“创建架构”对话框中，选择&#x200B;**[!UICONTROL 手动创建]**（自行添加字段和字段组）或&#x200B;**[!UICONTROL ML辅助创建]**（上传CSV文件并使用机器学习生成推荐的架构）。
5. 为您的架构选择一个基类（例如，XDM Individual Profile、XDM ExperienceEvent或其他）。 如果选择&#x200B;**[!UICONTROL 其他]**，则可以从可用的自定义类或标准类中进行选择。
6. 为您的架构输入人类友好的名称和描述。
7. 使用架构编辑器：添加字段组（可重复使用的字段块），定义单个字段（自定义名称、数据类型和选项），以及（可选）创建自定义数据类型或字段组（如果现有数据类型或字段组无法满足您的需求）。
8. 查看画布中的架构结构。 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以创建架构。
9. （可选）在架构编辑器中根据需要编辑字段、添加描述并调整字段组。

有关如何创建XDM架构的详细说明，请阅读有关使用架构编辑器[创建架构](../../../xdm/tutorials/create-schema-ui.md)的指南。

### 创建数据集

接下来，您必须创建一个引用刚刚创建的架构的数据集。

1. 在Experience Platform UI中，从左侧导航中选择[!UICONTROL 数据集]以打开[!UICONTROL 数据集]工作区。
2. 选择右上方的&#x200B;**[!UICONTROL 创建数据集]**。
3. 在创建选项中，选择&#x200B;**[!UICONTROL 从架构创建数据集]**。
4. 从列表中，搜索并选择您之前创建的XDM架构。 找到架构后，选择&#x200B;**[!UICONTROL 下一步]**。
5. 为数据集输入唯一的描述性名称。
6. 或者，添加帮助未来用户识别数据集的描述。
7. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以创建数据集。

有关如何创建数据集的详细说明，请阅读[数据集UI指南](../../../catalog/datasets/user-guide.md)。

## 将[!DNL Capillary Streaming Events]连接到Experience Platform

完成[!DNL Capillary]的先决条件设置后，请阅读[[!DNL Capillary Streaming Events] UI教程](../../tutorials/ui/create/loyalty/capillary.md)，了解如何将帐户连接并从[!DNL Capillary]将数据流式传输到Experience Platform。
