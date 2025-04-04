---
title: 使用API为Azure设置和配置客户管理的密钥
description: 了解如何使用您的Azure租户设置您的CMK应用并将您的加密密钥ID发送到Adobe Experience Platform。
role: Developer
feature: API, Privacy
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 1%

---

# 使用API为Azure设置和配置客户管理的密钥

本文档介绍了有关使用API在Adobe Experience Platform中启用客户管理的密钥(CMK)的Azure特定说明。 有关如何使用Azure托管的Experience Platform实例的UI完成此过程的说明，请参阅[UI CMK设置文档](./ui-set-up.md)。

有关特定于AWS的说明，请参阅[AWS安装指南](../aws/ui-set-up.md)。

## 先决条件

要查看和访问Adobe Experience Platform中的[!UICONTROL 加密]部分，您必须已创建一个角色，并为其分配了[!UICONTROL 管理客户管理的密钥]权限。 任何具有[!UICONTROL 管理客户管理的密钥]权限的用户都可以为其组织启用CMK。

有关在Experience Platform中分配角色和权限的详细信息，请参阅[配置权限文档](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html)。

若要为Azure托管的Experience Platform实例启用CMK，必须使用以下设置配置您的[[!DNL Azure] 密钥保管库](./azure-key-vault-config.md)：

* [启用清除保护](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [启用软删除](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [使用基于 [!DNL Azure] 角色的访问控制配置访问](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [配置 [!DNL Azure] 密钥保管库](./azure-key-vault-config.md)

## 设置CMK应用程序 {#register-app}

配置密钥保管库后，下一步是注册将链接到[!DNL Azure]租户的CMK应用程序。

### 快速入门

注册CMK应用程序需要您调用Experience Platform API。 有关如何收集进行这些调用所需的身份验证标头的详细信息，请参阅[Experience Platform API身份验证指南](../../../api-authentication.md)。

虽然身份验证指南提供了有关如何为所需的`x-api-key`请求标头生成您自己的唯一值的说明，但本指南中的所有API操作都使用静态值`acp_provisioning`。 但是，您仍然必须提供自己的`{ACCESS_TOKEN}`和`{ORG_ID}`值。

在本指南中显示的所有API调用中，`platform.adobe.io`都用作根路径，其默认为VA7区域。 如果贵组织使用其他区域，`platform`后面必须跟有短划线和分配给贵组织的区域代码： NLD2为`nld2`，AUS5为`aus5`（例如：`platform-aus5.adobe.io`）。 如果您不知道您所在的地区，请联系您的系统管理员。

### 获取身份验证URL {#fetch-authentication-url}

要开始注册流程，请向应用程序注册端点发出GET请求，以获取贵组织所需的身份验证URL。

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的响应返回包含身份验证URL的`applicationRedirectUrl`属性。

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

将`applicationRedirectUrl`地址复制并粘贴到浏览器中以打开身份验证对话框。 选择&#x200B;**[!DNL Accept]**&#x200B;以将CMK应用服务主体添加到您的[!DNL Azure]租户。

![突出显示带有[!UICONTROL 接受]的Microsoft权限请求对话框。](../../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### 将CMK应用程序分配给角色 {#assign-to-role}

完成身份验证过程后，导航回您的[!DNL Azure]密钥库，并在左侧导航中选择&#x200B;**[!DNL Access control]**。 从此处依次选择&#x200B;**[!DNL Add]**&#x200B;和&#x200B;**[!DNL Add role assignment]**。

![突出显示了[!DNL Add]和[!DNL Add role assignment]的Microsoft Azure仪表板。](../../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

下一个屏幕提示您为此分配选择一个角色。 选择&#x200B;**[!DNL Key Vault Crypto Service Encryption User]**&#x200B;再选择&#x200B;**[!DNL Next]**&#x200B;以继续。

>[!NOTE]
>
>如果您有[!DNL Managed-HSM Key Vault]层，则必须选择&#x200B;**[!DNL Managed HSM Crypto Service Encryption User]**&#x200B;用户角色。

![突出显示了[!DNL Key Vault Crypto Service Encryption User]的Microsoft Azure仪表板。](../../../images/governance-privacy-security/customer-managed-keys/select-role.png)

在下一个屏幕上，选择&#x200B;**[!DNL Select members]**&#x200B;以在右边栏中打开一个对话框。 使用搜索栏查找CMK应用程序的服务主体，并从列表中选择它。 完成后，选择&#x200B;**[!DNL Save]**。

>[!NOTE]
>
>如果在列表中找不到您的应用程序，则表示您的服务主体尚未被租户接受。 为确保您拥有正确的权限，请与[!DNL Azure]管理员或代表合作。

## 在Experience Platform上启用加密密钥配置 {#send-to-adobe}

在[!DNL Azure]上安装CMK应用后，可以将加密密钥标识符发送到Adobe。 在左侧导航中选择&#x200B;**[!DNL Keys]**，然后选择要发送的密钥的名称。

![突出显示了[!DNL Keys]对象和键名称的Microsoft Azure仪表板。](../../../images/governance-privacy-security/customer-managed-keys/select-key.png)

选择键的最新版本，此时将显示其详细信息页面。 在此处，您可以选择为密钥配置允许的操作。

>[!IMPORTANT]
>
>允许对该键执行的最小所需操作是&#x200B;**[!DNL Wrap Key]**&#x200B;和&#x200B;**[!DNL Unwrap Key]**&#x200B;权限。 您可以根据需要包含[!DNL Encrypt]、[!DNL Decrypt]、[!DNL Sign]和[!DNL Verify]。

**[!UICONTROL 密钥标识符]**&#x200B;字段显示密钥的URI标识符。 复制此URI值以供在下一步中使用。

![Microsoft Azure功能板密钥详细信息中突出显示[!DNL Permitted operations]和复制密钥URL部分。](../../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

获得密钥保管库URI后，可以使用POST请求将其发送到CMK配置端点。

>[!NOTE]
>
>Adobe中只存储密钥保管库和密钥名称，而不存储密钥版本。

**请求**

+++ 将密钥保管库URI发送到CMK配置端点的示例请求。

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
| `name` | 配置的名称。 请确保记住此值，因为在[后续步骤](#check-status)中需要检查配置的状态。 值区分大小写。 |
| `type` | 配置类型。 必须设置为`BYOK_CONFIG`。 |
| `imsOrgId` | 您的组织ID。 此ID的值必须与`x-gw-ims-org-id`标头下提供的值相同。 |
| `configData` | 此属性包含有关配置的以下详细信息：<ul><li>`providerType`：必须设置为`AZURE_KEYVAULT`。</li><li>`keyVaultKeyIdentifier`：您复制了[early](#send-to-adobe)的密钥保管库URI。</li></ul> |

+++

**响应**

+++ 成功的响应将返回配置作业的详细信息。

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
    "imsOrgId": "{ORG_ID}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

+++

作业应在几分钟内完成处理。

## 验证配置的状态 {#check-status}

要检查配置请求的状态，您可以发出GET请求。

**请求**

您必须将要检查的配置的`name`附加到路径（以下示例中为`config1`），并包含设置为`BYOK_CONFIG`的`configType`查询参数。

+++ 检查配置请求状态的示例请求。

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

+++

**响应**

+++ 成功的响应将返回作业的状态。

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
  "imsOrgId": "{ORG_ID}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

+++

`status`属性可以具有以下含义的四个值之一：

1. `RUNNING`：验证Experience Platform是否可以访问密钥和密钥保管库。
1. `UPDATE_EXISTING_RESOURCES`：系统正在将密钥保管库和密钥名称添加到组织中所有沙盒的数据存储中。
1. `COMPLETED`：密钥保管库和密钥名称已成功添加到数据存储。
1. `FAILED`：出现问题，主要与密钥、密钥保管库或多租户应用设置有关。

## 后续步骤

通过完成上述步骤，您已成功为组织启用CMK。 对于Azure托管的Experience Platform实例，现在将使用[!DNL Azure]密钥保管库中的密钥对摄取到主数据存储中的数据加密和解密。

要了解有关Adobe Experience Platform中数据加密的更多信息，请参阅[加密文档](../../encryption.md)。
