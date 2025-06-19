---
title: 为客户管理的密钥配置Azure密钥保管库
description: 了解如何使用Azure创建新的企业帐户，或使用现有企业帐户并创建密钥保管库。
role: Developer
feature: Privacy
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: c920f78363ee5f040964dbd3a0d0815474094b07
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# 为客户管理的密钥配置[!DNL Azure]密钥保管库

客户管理的密钥(CMK)支持来自[!DNL Microsoft Azure]密钥库和AWS [!DNL Key Management Service (KMS)]的密钥。 如果您的实施托管在[!DNL Azure]上，请按照以下步骤创建密钥保管库。 对于AWS托管的实施，请参阅[AWS KMS配置指南](../aws/configure-kms.md)。

>[!IMPORTANT]
>
>仅支持[!DNL Azure]密钥保管库的标准、高级和托管HSM层。 不支持[!DNL Azure Dedicated HSM]和[!DNL Azure Payments HSM]。 有关提供的密钥管理服务的详细信息，请参阅[[!DNL Azure] 文档](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services)。

>[!NOTE]
>
>以下文档仅介绍创建密钥存储库的基本步骤。 在本指南之外，您应根据贵组织的策略配置密钥库。

登录到[!DNL Azure]门户并使用搜索栏在服务列表下找到&#x200B;**[!DNL Key vaults]**。

![搜索结果中突出显示了[!DNL Microsoft Azure]中具有[!DNL Key vaults]的搜索功能。](../../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

选择服务后将显示&#x200B;**[!DNL Key vaults]**&#x200B;页。 从此处选择&#x200B;**[!DNL Create]**。

![在[!DNL Microsoft Azure]中突出显示[!DNL Create]的[!DNL Key vaults]仪表板。](../../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

使用提供的表单，填写密钥库的基本详细信息，包括名称和分配的资源组。

>[!WARNING]
>
>虽然大多数选项可以保留为其默认值，但&#x200B;**请确保启用软删除和清除保护选项**。 如果不启用这些功能，则在删除密钥库时，您可能会失去对数据的访问权限。
>
>![已突出显示具有软删除和清除保护的[!DNL Microsoft Azure] [!DNL Create a Key Vault]工作流。](../../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

在此处，继续完成Key Vault创建工作流，并根据您组织的策略配置不同的选项。

一旦您进入&#x200B;**[!DNL Review + create]**&#x200B;步骤，您可以在密钥库验证过程中查看其详细信息。 验证通过后，选择&#x200B;**[!DNL Create]**&#x200B;以完成该过程。

![Microsoft Azure Key电子仓库审阅和创建页面时突出显示。](../../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## 配置访问权限 {#configure-access}

接下来，为您的密钥库启用基于Azure角色的访问控制。 在左侧导航的[!DNL Settings]部分中选择&#x200B;**[!DNL Access configuration]**，然后选择&#x200B;**[!DNL Azure role-based access control]**&#x200B;以启用设置。 此步骤至关重要，因为以后必须将CMK应用程序与Azure角色关联。 [API](./api-set-up.md#assign-to-role)和[UI](./ui-set-up.md#assign-to-role)工作流中均记录分配角色。

![突出显示了[!DNL Access configuration]和[!DNL Azure role-based access control]的[!DNL Microsoft Azure]仪表板。](../../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## 配置联网选项 {#configure-network-options}

如果您的密钥库配置为限制对特定虚拟网络的公共访问或完全禁用公共访问，则必须授予[!DNL Microsoft]防火墙例外。

在左侧导航中选择&#x200B;**[!DNL Networking]**。 在&#x200B;**[!DNL Firewalls and virtual networks]**&#x200B;下，选中复选框&#x200B;**[!DNL Allow trusted Microsoft services to bypass this firewall]**，然后选择&#x200B;**[!DNL Apply]**。

>[!NOTE]
>
>如果您的密钥库使用受限网络访问，Adobe建议您添加以下静态IP地址： `20.88.123.53`。 通过添加此IP地址，Adobe服务可以更有效地监控连接，并在检测到访问问题时提供平台内警报。
>
>要了解有关何时允许列表Adobe的IP地址、警报的工作方式以及如何响应密钥访问失败通知的更多信息，请参阅[为Azure CMK配置警报和IP访问](./alerts-and-ip-access.md)。
>
>如果您的密钥库已配置为允许公共网络访问，则无需执行进一步操作。

![突出显示了[!DNL Microsoft Azure]的[!DNL Networking]选项卡，其中包含[!DNL Networking]和[!DNL Allow trusted Microsoft surfaces to bypass this firewall]异常。](../../../images/governance-privacy-security/customer-managed-keys/networking.png)

### 生成密钥 {#generate-a-key}

创建密钥存储库后，即可生成新密钥。 导航到&#x200B;**[!DNL Keys]**&#x200B;选项卡并选择&#x200B;**[!DNL Generate/Import]**。

![高亮显示了[!DNL Azure]的[!DNL Keys]选项卡（包含[!DNL Generate import]）。](../../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

使用提供的表单提供密钥的名称，并为密钥类型选择&#x200B;**RSA**&#x200B;或&#x200B;**RSA-HSM**。 对于[!DNL Azure]托管的实施，**[!DNL RSA key size]**&#x200B;必须是[!DNL Azure Cosmos DB]所需的至少&#x200B;**3072**&#x200B;位。 [!DNL Azure Data Lake Storage]还与RSA 3027兼容。

>[!NOTE]
>
>请记住您为密钥提供的名称，因为将密钥发送到Adobe时需要使用该名称。

使用其余控件来配置要生成或导入的键（如果需要）。 完成后，选择&#x200B;**[!DNL Create]**。

![突出显示了[!DNL 3072]位的[!DNL Create a key]仪表板。](../../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

配置的密钥将显示在保险库的密钥列表中。

![键名称高亮显示的[!DNL Keys]工作区。](../../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## 后续步骤

要继续设置客户管理的密钥功能的一次性流程，请按照平台托管环境的设置指南进行操作：

- 对于[!DNL Azure]，请使用[API](./api-set-up.md)或[UI](./ui-set-up.md)安装指南。
- 对于AWS，请参阅[AWS配置KMS指南](../aws/configure-kms.md)和[UI设置指南](../aws/ui-set-up.md)。
