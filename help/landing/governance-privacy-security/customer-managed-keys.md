---
title: Adobe Experience Platform中的客户管理的密钥
description: 了解如何为Adobe Experience Platform中存储的数据设置您自己的加密密钥。
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: 2564c0cc817362536f1a8291e1c733d9efbf5a78
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 1%

---

# Adobe Experience Platform中的客户管理的密钥

存储在Adobe Experience Platform上的数据使用系统级别密钥静态加密。 如果您使用的是基于Platform构建的应用程序，则可以选择使用自己的加密密钥，从而更好地控制数据安全。

>[!NOTE]
>
>Adobe Experience Platform Data Lake和Profile Store中的数据是使用CMK加密的。 这些存储区被视为您的主数据存储。

本文档介绍了在Platform中启用客户管理的密钥(CMK)功能的过程。

## 先决条件

要访问CMK API，您必须分配 [!UICONTROL 管理客户管理的密钥] 与该API凭据关联的新角色或现有角色的权限和在生产沙盒中的访问权限。 如果您希望仅向API凭据提供CMK访问权限，建议您使用前面提到的必要权限创建新的CMK管理员角色。

有关在Experience Platform中分配角色和权限的详细信息，请参阅 [配置权限文档](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

为了启用CMK，您的 [!DNL Azure] 必须使用以下设置配置密钥保管库：

* [启用清除保护](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [启用软删除](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [使用配置访问 [!DNL Azure] 基于角色的访问控制](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

## 流程摘要

CMK包含在Healthcare Shield以及Adobe的Privacy and Security Shield产品中。 贵组织在购买其中一种产品的许可证后，可以开始一次性流程来设置该功能。

>[!WARNING]
>
>设置CMK后，无法还原为系统管理的密钥。 您负责安全地管理您的密钥，并在中提供对您的密钥库、密钥和CMK应用程序的访问权限 [!DNL Azure] 以防止无法访问您的数据。

该过程如下：

1. [配置 [!DNL Azure] 密钥库](#create-key-vault) 根据贵组织的策略，则 [生成加密密钥](#generate-a-key) 最终将与Adobe共享。
1. 使用API调用执行以下操作 [设置CMK应用程序](#register-app) 与您的 [!DNL Azure] 租户。
1. 使用API调用执行以下操作 [将您的加密密钥ID发送到Adobe](#send-to-adobe) 并启动该功能的启用过程。
1. [检查配置的状态](#check-status) 验证是否已启用CMK。

完成设置过程后，所有通过沙盒载入到Platform中的所有数据将使用以下加密： [!DNL Azure] 键设置。 要使用CMK，您将利用 [!DNL Microsoft Azure] 作为其一部分的功能 [公共预览项目](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

## 配置 [!DNL Azure] 密钥库 {#create-key-vault}

CMK仅支持来自的键 [!DNL Microsoft Azure] 密钥库。 要开始使用此功能，您必须使用 [!DNL Azure] 创建新的企业帐户，或使用现有的企业帐户，并按照以下步骤创建密钥保管库。

>[!IMPORTANT]
>
>只有适用于的Premium和Standard服务层 [!DNL Azure] 支持密钥保管库。 [!DNL Azure Managed HSM]， [!DNL Azure Dedicated HSM] 和 [!DNL Azure Payments HSM] 不受支持。 请参阅 [[!DNL Azure] 文档](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) ，以了解有关提供的密钥管理服务的更多信息。

>[!NOTE]
>
>以下文档仅介绍创建密钥存储库的基本步骤。 在本指南之外，您应根据贵组织的策略配置密钥库。

登录到 [!DNL Azure] 门户并使用搜索栏查找 **[!DNL Key vaults]** 在服务列表下。

![搜索并选择密钥电子仓库](../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

此 **[!DNL Key vaults]** 选择服务后，将显示该页。 从此处选择 **[!DNL Create]**.

![创建密钥保管库](../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

使用提供的表单，填写密钥保管库的基本详细信息，包括名称和分配的资源组。

>[!WARNING]
>
>虽然大多数选项可以保留为其默认值， **确保启用软删除和清除保护选项**. 如果不启用这些功能，则在删除密钥库时，您可能会失去对数据的访问权限。
>
>![启用清除保护](../images/governance-privacy-security/customer-managed-keys/basic-config.png)

在此处，继续完成密钥库创建工作流，并根据您组织的策略配置不同的选项。

一旦你到了 **[!DNL Review + create]** 步骤，您可以在验证密钥库时查看其详细信息。 验证通过后，选择 **[!DNL Create]** 以完成该过程。

![密钥库的基本配置](../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

### 配置联网选项

如果将密钥库配置为限制对特定虚拟网络的公共访问或完全禁用公共访问，则必须授予Microsoft防火墙例外。

选择 **[!DNL Networking]** 在左侧导航中。 下 **[!DNL Firewalls and virtual networks]**，选中复选框 **[!DNL Allow trusted Microsoft services to bypass this firewall]**，然后选择 **[!DNL Apply]**.

![密钥库的基本配置](../images/governance-privacy-security/customer-managed-keys/networking.png)

### 生成密钥 {#generate-a-key}

创建密钥库后，即可生成新的密钥。 导航至 **[!DNL Keys]** 选项卡并选择 **[!DNL Generate/Import]**.

![生成密钥](../images/governance-privacy-security/customer-managed-keys/view-keys.png)

使用提供的表单提供键的名称，然后选择 **RSA** 键类型对应的。 至少， **[!DNL RSA key size]** 必须至少为 **3072** 位数，如下所示 [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] 也与RSA 3027兼容。

>[!NOTE]
>
>请记住您为键提供的名称，因为此名称将在后面的步骤中使用： [将密钥发送到Adobe](#send-to-adobe).

使用其余控件来配置要生成或导入的键（如果需要）。 完成后，选择 **[!DNL Create]**.

![Configure键](../images/governance-privacy-security/customer-managed-keys/configure-key.png)

配置的密钥将显示在保险库的密钥列表中。

![密钥已添加](../images/governance-privacy-security/customer-managed-keys/key-added.png)

## 设置CMK应用程序 {#register-app}

配置密钥库后，下一步是注册将链接到您的 [!DNL Azure] 租户。

### 快速入门

注册CMK应用程序需要您调用平台API。 有关如何收集进行这些调用所需的身份验证标头的详细信息，请参阅 [平台API身份验证指南](../../landing/api-authentication.md).

而身份验证指南提供了有关如何为所需的生成您自己的唯一值的说明 `x-api-key` 请求标头，本指南中的所有API操作都使用静态值 `acp_provisioning` 而是。 您仍然必须提供自己的值， `{ACCESS_TOKEN}` 和 `{ORG_ID}`，但是。

在本指南中显示的所有API调用中， `platform.adobe.io` 用作根路径，默认值为VA7区域。 如果贵组织使用其他区域， `platform` 必须后跟一个短划线和分配给您的组织的区域代码： `nld2` 用于NLD2或 `aus5` 对于AUS5(例如： `platform-aus5.adobe.io`)。 如果您不知道您所在的地区，请联系您的系统管理员。

### 获取身份验证URL

要开始注册流程，请向应用程序注册端点发出GET请求，以获取您组织所需的身份验证URL。

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的响应返回 `applicationRedirectUrl` 属性，包含身份验证URL。

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

复制并粘贴 `applicationRedirectUrl` 将地址插入浏览器以打开身份验证对话框。 选择 **[!DNL Accept]** 要将CMK应用程序服务主体添加到您的 [!DNL Azure] 租户。

![接受权限请求](../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### 将CMK应用程序分配给角色 {#assign-to-role}

完成身份验证过程后，导航回 [!DNL Azure] 密钥库和选择 **[!DNL Access control]** 在左侧导航中。 从此处选择 **[!DNL Add]** 后接 **[!DNL Add role assignment]**.

![添加角色分配](../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

下一个屏幕提示您为此分配选择一个角色。 选择 **[!DNL Key Vault Crypto Service Encryption User]** 选择之前 **[!DNL Next]** 以继续。

![选择角色](../images/governance-privacy-security/customer-managed-keys/select-role.png)

在下一个屏幕上，选择 **[!DNL Select members]** 以在右边栏中打开对话框。 使用搜索栏查找CMK应用程序的服务主体，并从列表中选择它。 完成后，选择 **[!DNL Save]**.

>[!NOTE]
>
>如果在列表中找不到您的应用程序，则表示您的服务主体尚未被租户接受。 请与您的 [!DNL Azure] 管理员或代表，以确保您拥有正确的权限。

## 在Experience Platform上启用加密密钥配置 {#send-to-adobe}

在上安装CMK应用程序后 [!DNL Azure]，您可以将加密密钥标识符发送到Adobe。 选择 **[!DNL Keys]** ，后跟要发送的键的名称。

![选择键](../images/governance-privacy-security/customer-managed-keys/select-key.png)

选择键的最新版本，此时将显示其详细信息页面。 在此处，您可以选择为密钥配置允许的操作。 至少必须将该密钥授予 **[!DNL Wrap Key]** 和 **[!DNL Unwrap Key]** 权限。

此 **[!UICONTROL 密钥标识符]** 字段显示键的URI标识符。 复制此URI值以供在下一步中使用。

![复制密钥URL](../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

获取密钥保管库URI后，可以使用POST请求将其发送到CMK配置端点。

>[!NOTE]
>
>只有密钥保管库和密钥名称与Adobe一起存储，而非密钥版本。

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/infrastructure/manager/customer/config \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "name": "Config1",
        "type": "BYOK_CONFIG",
        "imsOrgId": "{ORG_ID}",
        "configData": {
          "providerType": "AZURE_KEYVAULT",
          "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 配置的名称。 确保您记住此值，因为需要在以下位置检查配置状态： [后续步骤](#check-status). 值区分大小写。 |
| `type` | 配置类型。 必须设置为 `BYOK_CONFIG`. |
| `imsOrgId` | 您的组织 ID。该值必须与 `x-gw-ims-org-id` 标题。 |
| `configData` | 包含有关配置的以下详细信息：<ul><li>`providerType`：必须设置为 `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier`：您复制的密钥保管库URI [更早](#send-to-adobe).</li></ul> |

**响应**

成功的响应将返回配置作业的详细信息。

```json
{
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "config": {
    "configData": {
      "keyVaultUri": "https://adobecmkexample.vault.azure.net",
      "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
      "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
      "keyName": "Config1",
      "providerType": "AZURE_KEYVAULT"
    },
    "name": "acpcf978863Aaepcmkmultitenantapp",
    "type": "BYOK_CONFIG",
    "imsOrgId": "{IMS_ORG}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

作业应在几分钟内完成处理。

## 验证配置的状态 {#check-status}

要检查配置请求的状态，您可以发出GET请求。

**请求**

您必须附加 `name` 要检查的配置的路径(`config1` （在下例中）并包括 `configType` 查询参数设置为 `BYOK_CONFIG`.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的响应将返回作业的状态。

```json
{
  "name": "acpcf978863Aaepcmkmultitenantapp",
  "type": "BYOK_CONFIG",
  "status": "COMPLETED",
  "configData": {
    "keyVaultUri": "https://adobecmkexample.vault.azure.net",
    "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
    "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
    "keyName": "Config1",
    "providerType": "AZURE_KEYVAULT"
  },
  "imsOrgId": "{IMS_ORG}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

此 `status` 属性可以具有以下含义的四个值之一：

1. `RUNNING`：验证平台是否能够访问密钥和密钥保管库。
1. `UPDATE_EXISTING_RESOURCES`：系统正在将密钥保管库和密钥名称添加到组织中所有沙盒的数据存储中。
1. `COMPLETED`：密钥保管库和密钥名称已添加到数据存储。
1. `FAILED`：出现问题，主要与密钥、密钥库或多租户应用程序设置有关。

## 撤销访问权限 {#revoke-access}

如果要撤销平台对您的数据的访问权限，可以从的密钥保管库中移除与应用程序关联的用户角色 [!DNL Azure].

>[!WARNING]
>
>禁用密钥保险库、密钥或CMK应用程序可能会导致重大更改。 一旦禁用密钥保管库、密钥或CMK应用程序，并且数据在Platform中不再可访问，则与该数据相关的任何下游操作都将不再可能。 在对配置进行任何更改之前，请确保您了解撤销平台对您密钥的访问权限将会产生的下游影响。

删除密钥访问权限或禁用/删除密钥后 [!DNL Azure] 密钥库中，此配置可能需要几分钟到24小时的时间才能传播到主数据存储。 平台工作流还包括性能和核心应用程序功能所需的缓存和临时数据存储。 通过此类缓存和临时存储传播CMK撤销最多可能需要七天，具体取决于其数据处理工作流。 例如，这意味着“配置文件”仪表板将保留并显示其缓存数据存储中的数据，并且作为刷新周期的一部分，需要七天时间使缓存数据存储中保留的数据过期。 在重新启用对应用程序的访问时，数据再次变为可用同样的时间延迟。

>[!NOTE]
>
>对于非主（缓存/临时）数据的7天数据集到期，存在两个特定于用例的异常。 有关这些功能的更多信息，请参阅各自的文档。<ul><li>[Adobe Journey Optimizer URL Shortener](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=zh-Hans#message-preset-sms)</li><li>[边缘投影](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## 后续步骤

通过完成上述步骤，您已成功为组织启用CMK。 现在，摄取到主数据存储中的数据将使用 [!DNL Azure] 密钥库。

