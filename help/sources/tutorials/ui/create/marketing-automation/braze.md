---
title: 在UI中为Braze数据创建数据流
description: 了解如何使用Adobe Experience Platform UI为您的Braze帐户创建数据流。
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta 版
source-git-commit: bfcea2a30a0ecadcafaddf7660eef90952dcade6
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 1%

---

# 创建 [!DNL Braze Currents] UI中的源连接

>[!NOTE]
>
>此 [!DNL Braze Currents] 源为测试版。 请阅读 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记源代码的更多信息。

[!DNL Braze] 支持消费者和品牌之间以客户为中心的实时互动。 [!DNL Braze Currents] 是来自Braze平台的参与事件的实时数据流，是最强大但最精细的导出 [!DNL Braze] 平台。

请阅读以下教程，了解如何从您的网站获取参与事件数据。 [!DNL Braze] Adobe Experience Platform帐户。

## 先决条件

要完成本指南中的步骤，您将需要：

* 登录至 [Adobe Experience Platform](https://platform.adobe.com) 和创建新的流源连接的权限。
* 登录您的 [[!DNL Braze] 仪表板](https://dashboard.braze.com/sign_in)，未使用 [电流连接器许可证](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)、和创建连接器的权限。 欲知更多信息，请参阅 [设置要求 [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

此外，还需要您实际了解本教程 [[!DNL Braze] 电流](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents).

如果您已经拥有 [!DNL Braze] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/marketing-automation.md).

## 连接您的 [!DNL Braze] 帐户到Experience Platform

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 *营销自动化* 类别，选择 **[!UICONTROL 钎焊电流]**，然后选择 **[!UICONTROL 添加数据]**.

![已选中“钎焊电流”源的Experience PlatformUI上的源目录。](../../../../images/tutorials/create/braze/catalog.png)

接下来，上传提供的 [钎焊电流示例文件](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json). 此文件包含Braze可能作为事件的一部分发送的所有可能字段。

![“添加数据”屏幕。](../../../../images/tutorials/create/braze/select-data.png)

上传文件后，必须提供数据流详细信息，包括有关数据集和要映射到的架构的信息。
![“数据流详细信息”屏幕高亮显示“数据集详细信息”。](../../../../images/tutorials/create/braze/dataflow-detail.png)

然后，使用映射界面配置数据的映射。

![“映射”屏幕。](../../../../images/tutorials/create/braze/mapping.png)

>[!IMPORTANT]
>
>钎焊时间戳不是以毫秒为单位表示，而是以秒为单位表示。 为了准确反映Experience Platform中的时间戳，您需要创建以毫秒为单位的计算字段。 “time * 1000”的计算将正确地转换为毫秒，适合映射到Experience Platform内的时间戳字段。
>
>![为时间戳创建计算字段 ](../../../../images/tutorials/create/braze/create-calculated-field.png)

### 收集所需的凭据

创建连接后，必须收集以下凭据值，随后将在钎焊仪表板中提供这些凭据值，以将数据发送到Experience Platform。 欲知更多信息，请参阅 [!DNL Braze] [导航到洋流的指南](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

| 字段 | 描述 |
| --- | --- |
| 客户端ID | 与您的Experience Platform源关联的客户端ID。 |
| 客户端密码 | 与您的Experience Platform源关联的客户端密钥。 |
| 租户ID | 与您的Experience Platform源关联的租户ID。 |
| 沙盒名称 | 与您的Experience Platform源关联的沙盒。 |
| 数据流ID | 与您的Experience Platform源关联的数据流ID。 |
| 流端点 | 与您的Experience Platform源关联的流端点。 **注意**： [!DNL Braze] 自动将其转换为批处理流端点。 |

### 配置 [!DNL Braze Currents] 以将数据流式传输到数据源

在 [!DNL Braze Dashboard]，导航到合作伙伴集成 **->** 数据导出，然后选择 **[!DNL Create New Current]**. 系统将提示您提供连接器的名称、有关连接器的通知的联系信息以及上面列出的凭据。 选择要接收的事件，或者配置任何所需的字段排除/转换，然后选择 **[!DNL Launch Current]**.

## 后续步骤

通过学习本教程，您已建立与的连接 [!DNL Braze] 帐户。 您现在可以继续下一教程和 [配置数据流以将营销自动化系统数据引入 [!DNL Platform]](../../dataflow/marketing-automation.md).