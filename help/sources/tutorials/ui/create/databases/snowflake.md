---
title: 使用UI将Snowflake连接到Experience Platform
type: Tutorial
description: 了解如何使用Snowflake UI创建Adobe Experience Platform源连接。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 80ea8b5aa46e7aa4fdecfee3c962a77989a9b191
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 2%

---

# 使用UI将[!DNL Snowflake]连接到Experience Platform

>[!IMPORTANT]
>
>[!DNL Snowflake]源在源目录中可供已购买Real-Time Customer Data Platform Ultimate的用户使用。

阅读本指南，了解如何使用用户界面将您的[!DNL Snowflake]帐户连接到Adobe Experience Platform。

## 快速入门

>[!WARNING]
>
>[!DNL Snowflake]源的基本身份验证（或帐户密钥身份验证）将于2025年11月被弃用。 您必须迁移到基于密钥对的身份验证，才能继续使用源并从数据库中摄取数据到Experience Platform。 有关弃用的详细信息，请阅读关于降低凭据泄露风险的[[!DNL Snowflake] 最佳实践指南](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/)。

本教程需要对以下Experience Platform组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

>[!NOTE]
>
>必须将`PREVENT_UNLOAD_TO_INLINE_URL`标志设置为`FALSE`，以允许将数据从[!DNL Snowflake]数据库卸载到Experience Platform。

## 导航源目录 {#navigate}

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;**[!DNL Snowflake]**&#x200B;数据库&#x200B;*[!UICONTROL 类别下选择]*，然后选择&#x200B;**[!UICONTROL 设置]**。

>[!TIP]
>
>当给定的源尚未具有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL 设置]**&#x200B;选项。 一旦存在经过身份验证的帐户，此选项将更改为&#x200B;**[!UICONTROL 添加数据]**。

![已选择Snowflake卡的源目录……](../../../../images/tutorials/create/snowflake/catalog.png)

## 使用现有帐户 {#existing}

接下来，您将进入源工作流的身份验证步骤。 在此，您可以使用现有帐户或创建新帐户。

若要使用现有帐户，请选择要连接的[!DNL Snowflake]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![源工作流中的现有帐户接口。](../../../../images/tutorials/create/snowflake/existing.png)

## 创建新帐户 {#create}

如果您没有现有帐户，则必须通过提供与您的源对应的必需身份验证凭据来创建新帐户。

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后提供名称并选择性地为您的帐户添加描述。

### 连接到Azure上的Experience Platform {#azure}

您可以使用帐户密钥身份验证或密钥对身份验证将您的[!DNL Snowflake]帐户连接到Azure上的Experience Platform。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

若要使用帐户密钥身份验证，请选择&#x200B;**[!UICONTROL 帐户密钥身份验证]**，在输入表单中提供您的连接字符串，然后选择&#x200B;**[!UICONTROL 连接到源]**。

![帐户密钥身份验证接口。](../../../../images/tutorials/create/snowflake/account-key-auth.png)

| 凭据 | 描述 |
| --- | --- |
| 帐户 | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须跨不同的[!DNL Snowflake]组织唯一标识帐户。 要实现此目的，您必须在帐户名称前添加组织名称。 例如： `orgname-account_name`。 请阅读有关[检索 [!DNL Snowflake] 帐户标识符](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier)的指南，以获取其他指导。 有关更多信息，请参阅[[!DNL Snowflake] 文档](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)。 |
| 仓库 | [!DNL Snowflake]仓库管理应用程序的查询执行过程。 每个[!DNL Snowflake]仓库彼此独立，在将数据传送到Experience Platform时必须单独访问。 |
| 数据库 | [!DNL Snowflake]数据库包含要带Experience Platform的数据。 |
| 用户名 | [!DNL Snowflake]帐户的用户名。 |
| 密码 | [!DNL Snowflake]用户帐户的密码。 |
| 角色 | 在[!DNL Snowflake]会话中使用的默认访问控制角色。 该角色应为已分配给指定用户的现有角色。 默认角色为`PUBLIC`。 |
| 连接字符串 | 用于连接到[!DNL Snowflake]实例的连接字符串。 [!DNL Snowflake]的连接字符串模式为`jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB 密钥对身份验证]

要使用密钥对身份验证，请选择&#x200B;**[!UICONTROL 密钥对身份验证]**，提供帐户、用户名、私钥、私钥密码、数据库和仓库的值，然后选择&#x200B;**[!UICONTROL 连接到源]**。

![帐户密钥对身份验证接口。](../../../../images/tutorials/create/snowflake/key-pair-auth.png)

使用密钥对身份验证，您必须生成2048位RSA密钥对，然后在为[!DNL Snowflake]源创建帐户时提供以下值。

| 凭据 | 描述 |
| --- | --- |
| 帐户 | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须跨不同的[!DNL Snowflake]组织唯一标识帐户。 要实现此目的，您必须在帐户名称前添加组织名称。 例如： `orgname-account_name`。 请阅读有关[检索 [!DNL Snowflake] 帐户标识符](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier)的指南，以获取其他指导。 有关更多信息，请参阅[[!DNL Snowflake] 文档](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)。 |
| 用户名 | [!DNL Snowflake]帐户的用户名。 |
| 私钥 | [!DNL Base64-]帐户的[!DNL Snowflake]编码私钥。 您可以生成加密或未加密的私钥。 如果您使用的是加密的私钥，那么在针对Experience Platform进行身份验证时，还必须提供私钥密码。 有关详细信息，请阅读[检索 [!DNL Snowflake] 私钥](../../../../connectors/databases/snowflake.md)的指南。 |
| 私钥密码 | 私钥密码是附加的安全层，在使用加密的私钥进行身份验证时必须使用该安全层。 如果您使用未加密的私钥，则无需提供密码。 |
| 数据库 | 包含要摄取到Experience Platform的数据的[!DNL Snowflake]数据库。 |
| 仓库 | [!DNL Snowflake]仓库管理应用程序的查询执行过程。 每个[!DNL Snowflake]仓库彼此独立，在将数据传送到Experience Platform时必须单独访问。 |

有关这些值的详细信息，请参阅[此Snowflake文档](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

>[!ENDTABS]

### 连接到AWS上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../../../landing/multi-cloud.md)。

要创建新的[!DNL Snowflake]帐户并连接到AWS上的Experience Platform，请确保您处于VA6沙盒中，然后提供身份验证所需的凭据。

>[!BEGINTABS]

>[!TAB 密钥对身份验证]

若要使用密钥对进行连接，请选择&#x200B;**[!UICONTROL 密钥对身份验证]**，提供您的身份验证凭据，然后选择&#x200B;**[!UICONTROL 连接到源]**。 有关这些凭据的详细信息，请阅读[[!DNL Snowflake] 批次概述](../../../../connectors/databases/snowflake.md#gather-required-credentials)。

![密钥对身份验证的新帐户创建步骤。](../../../../images/tutorials/create/snowflake/key-pair-aws.png)

>[!TAB 基本身份验证]

>[!WARNING]
>
>[!DNL Snowflake]源的基本身份验证（或帐户密钥身份验证）将于2025年11月被弃用。 您必须迁移到基于密钥对的身份验证，才能继续使用源并从数据库中摄取数据到Experience Platform。 有关弃用的详细信息，请阅读关于降低凭据泄露风险的[[!DNL Snowflake] 最佳实践指南](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/)。

若要使用用户名和密码组合进行连接，请选择&#x200B;**[!UICONTROL 基本身份验证]**，提供您的身份验证凭据，然后选择&#x200B;**[!UICONTROL 连接到源]**。 有关这些凭据的详细信息，请阅读[[!DNL Snowflake] 批次概述](../../../../connectors/databases/snowflake.md#gather-required-credentials)。

![源工作流程中的新帐户步骤，可将Snowflake连接到AWS上的Experience Platform。](../../../../images/tutorials/create/snowflake/aws-auth.png)

>[!ENDTABS]

### 跳过样本数据预览 {#skip-preview-of-sample-data}

在数据选择步骤中，摄取大型表或数据文件时可能会遇到超时。 您可以跳过数据预览以规避超时，并且仍可以查看架构，尽管没有示例数据。 要跳过数据预览，请启用&#x200B;**[!UICONTROL 跳过预览样本数据]**&#x200B;切换开关。

工作流的其余部分将保持不变。 唯一需要注意的是，跳过数据预览可能会阻止在映射步骤中自动验证已计算和必填字段，您随后必须在映射期间手动验证这些字段。

## 后续步骤

通过学习本教程，您已建立与Snowflake帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入 [!DNL Experience Platform]](../../dataflow/databases.md)。
