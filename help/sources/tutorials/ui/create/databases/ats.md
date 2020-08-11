---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Azure表存储源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# 在UI [!DNL Azure Table Storage] 中创建源连接器

>[!NOTE]
>连接 [!DNL Azure Table Storage] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用 [!DNL Azure Table Storage] 户界面创建（下称“ATS”）源连接器 [!DNL Platform] 的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的ATS连接，您可以跳过本文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

要访问您的ATS帐户， [!DNL Platform]您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 连接到实例的连接 [!DNL Azure Table Storage] 字符串。 要连接到ATS实例的连接字符串。 ATS的连接字符串模式是 `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 |

有关快速入门的详细信息，请参 [阅此Azure表存储文档](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction)。

## 连接帐 [!DNL Azure Table Storage] 户

收集所需凭据后，您可以按照以下步骤创建新的ATS帐户以连接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 *[!UICONTROL “源”以访问]* “源”工作区。 “目 *[!UICONTROL 录]* ”屏幕显示您可以为其创建入站帐户的各种源，每个源显示与它们关联的现有帐户和数据集流的数量。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“ *[!UICONTROL 类别]* ”下， **[!UICONTROL 选择“Azure表存储]** ”，在屏幕的右侧显示一个信息栏。 信息栏提供所选源的简短描述以及与源或视图其文档的选项。 要创建新的入站连接，请选择“添 **[!UICONTROL 加数据”]**。

![目录](../../../../images/tutorials/create/ats/catalog.png)

将显 *[!UICONTROL 示“连接到Azure表存储]* ”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，为连接提供名称、可选说明和ATS凭据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新帐户。

![connect](../../../../images/tutorials/create/ats/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的ATS帐户，然后选择“下 **[!UICONTROL 一步]** ”以继续。

![现有](../../../../images/tutorials/create/ats/existing.png)

## 后续步骤

通过遵循本教程，您已建立了与ATS帐户的连接。 您现在可以继续阅读下一个教程， [并配置数据流以将数据引入平台](../../dataflow/databases.md)。