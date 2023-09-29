---
title: 配置Azure密钥库
description: 了解如何使用Azure创建新的企业帐户，或使用现有企业帐户并创建密钥保管库。
source-git-commit: a0df05cde19e97d4abdad7abd19eafea8efe1096
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# 配置 [!DNL Azure] 密钥库

客户管理的密钥(CMK)仅支持来自 [!DNL Microsoft Azure] 密钥库。 要开始使用此功能，您必须使用 [!DNL Azure] 创建新的企业帐户，或使用现有的企业帐户，并按照以下步骤创建密钥保管库。

>[!IMPORTANT]
>
>只有适用于的Premium和Standard服务层 [!DNL Azure] 支持密钥保管库。 [!DNL Azure Managed HSM]， [!DNL Azure Dedicated HSM] 和 [!DNL Azure Payments HSM] 不受支持。 请参阅 [[!DNL Azure] 文档](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) ，以了解有关提供的密钥管理服务的更多信息。

>[!NOTE]
>
>以下文档仅介绍创建密钥存储库的基本步骤。 在本指南之外，您应根据贵组织的策略配置密钥库。

登录到 [!DNL Azure] 门户并使用搜索栏查找 **[!DNL Key vaults]** 在服务列表下。

![中的搜索功能 [!DNL Microsoft Azure] 替换为 [!DNL Key vaults] 在搜索结果中突出显示。](../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

此 **[!DNL Key vaults]** 选择服务后，将显示该页。 从此处选择 **[!DNL Create]**.

![此 [!DNL Key vaults] 中的仪表板 [!DNL Microsoft Azure] 替换为 [!DNL Create] 突出显示。](../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

使用提供的表单，填写密钥库的基本详细信息，包括名称和分配的资源组。

>[!WARNING]
>
>虽然大多数选项可以保留为其默认值， **确保启用软删除和清除保护选项**. 如果不启用这些功能，则在删除密钥库时，您可能会失去对数据的访问权限。
>
>![此 [!DNL Microsoft Azure] [!DNL Create a Key Vault] 突出显示软删除和清除保护的工作流。](../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

在此处，继续完成Key Vault创建工作流，并根据您组织的策略配置不同的选项。

一旦你到了 **[!DNL Review + create]** 步骤，您可以在验证过程中查看密钥库的详细信息。 验证通过后，选择 **[!DNL Create]** 以完成该过程。

![Microsoft Azure Key电子仓库“查看和创建”页面中突出显示了创建内容。](../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## 配置联网选项 {#configure-network-options}

如果将密钥库配置为限制对特定虚拟网络的公共访问或完全禁用公共访问，则必须授予 [!DNL Microsoft] 防火墙例外。

选择 **[!DNL Networking]** 在左侧导航中。 下 **[!DNL Firewalls and virtual networks]**，选中复选框 **[!DNL Allow trusted Microsoft services to bypass this firewall]**，然后选择 **[!DNL Apply]**.

![此 [!DNL Networking] 选项卡/ [!DNL Microsoft Azure] 替换为 [!DNL Networking] 和 [!DNL Allow trusted Microsoft surfaces to bypass this firewall] 突出显示异常。](../../images/governance-privacy-security/customer-managed-keys/networking.png)

### 生成密钥 {#generate-a-key}

创建密钥存储库后，即可生成新密钥。 导航至 **[!DNL Keys]** 选项卡并选择 **[!DNL Generate/Import]**.

![此 [!DNL Keys] 选项卡/ [!DNL Azure] 替换为 [!DNL Generate import] 突出显示。](../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

使用提供的表单提供键的名称，然后选择 **RSA** 键类型对应的。 至少， **[!DNL RSA key size]** 必须至少为 **3072** 位数，如下所示 [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] 也与RSA 3027兼容。

>[!NOTE]
>
>请记住您为键提供的名称，因为将键发送到Adobe时需要使用该名称。

使用其余控件来配置要生成或导入的键（如果需要）。 完成后，选择 **[!DNL Create]**.

![创建键仪表板，使用 [!DNL 3072] 位突出显示。](../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

配置的密钥将显示在保险库的密钥列表中。

![此 [!DNL Keys] 突出显示了键名称的工作区。](../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## 后续步骤

要继续设置客户管理的密钥功能的一次性过程，请继续 [API](./api-set-up.md) 或 [UI](./ui-set-up.md) 客户管理的密钥设置指南。
