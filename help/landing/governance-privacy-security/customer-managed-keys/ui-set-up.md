---
title: 使用Platform UI设置和配置客户管理的密钥
description: 了解如何使用您的Azure租户设置您的CMK应用并将您的加密密钥ID发送到Adobe Experience Platform。
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 1%

---

# 使用Platform UI设置和配置客户管理的密钥

本文档介绍了使用UI在Platform中启用客户管理的密钥(CMK)功能的过程。 有关如何使用API完成此过程的说明，请参阅 [API CMK设置文档](./api-set-up.md).

## 先决条件

要查看和访问 [!UICONTROL 加密] Adobe Experience Platform部分，您必须已创建一个角色并分配 [!UICONTROL 管理客户管理的密钥] 该角色的权限。 任何具有 [!UICONTROL 管理客户管理的密钥] 权限可以为他们的组织启用CMK。

有关在Experience Platform中分配角色和权限的详细信息，请参阅 [配置权限文档](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

要启用CMK，您的 [[!DNL Azure] 必须配置密钥保管库](./azure-key-vault-config.md) 设置：

* [启用清除保护](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [启用软删除](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [使用配置访问 [!DNL Azure] 基于角色的访问控制](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [配置 [!DNL Azure] 密钥库](./azure-key-vault-config.md)

## 设置CMK应用程序 {#register-app}

配置密钥库后，下一步是注册将链接到您的 [!DNL Azure] 租户。

### 快速入门

要查看 [!UICONTROL 加密配置] 仪表板，选择 **[!UICONTROL 加密]** 在 [!UICONTROL 管理] 左侧导航侧栏的标题。

![加密配置仪表板（带加密）和客户管理的密钥卡突出显示。](../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

选择 **[!UICONTROL 配置]** 以打开 [!UICONTROL 客户管理的密钥配置] 视图。 此工作区包含完成下述步骤并执行与Azure Key保管库集成所需的所有值。

### 复制身份验证URL {#copy-authentication-url}

要开始注册过程，请从复制贵组织的应用程序身份验证URL [!UICONTROL 客户管理的密钥配置] 查看并将其粘贴到您的 [!DNL Azure] 环境 **[!DNL Key Vault Crypto Service Encryption User]**. 操作方法详细信息 [分配角色](#assign-to-role) 将在下一节中提供。

选择复制图标(![复制图标。](../../images/governance-privacy-security/customer-managed-keys/copy-icon.png))通过 [!UICONTROL 应用程序身份验证URL].

![此 [!UICONTROL 客户管理的密钥配置] 视图中的应用程序身份验证URL部分突出显示。](../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

复制并粘贴 [!UICONTROL 应用程序身份验证URL] ，打开身份验证对话框。 选择 **[!DNL Accept]** 要将CMK应用程序服务主体添加到您的 [!DNL Azure] 租户。 确认身份验证会将您重定向到Experience Cloud登录页面。

![Microsoft权限请求对话框 [!UICONTROL Accept] 突出显示。](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>如果您有多个 [!DNL Microsoft Azure] 订阅后，您可能会将您的Platform实例连接到错误的密钥库。 在这种情况下，您必须将 `common` 部分。<br>从的门户设置、目录和订阅页面复制CMK目录ID [!DNL Microsoft Azure] 应用程序<br>![此 [!DNL Microsoft Azure] Application Portal settings， Directories and Subscriptions页，其中突出显示了目录ID。](../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>接下来，将其粘贴到浏览器地址栏中。<br>![突出显示应用程序身份验证URL的“common”部分的Google浏览器页面。](../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### 将CMK应用程序分配给角色 {#assign-to-role}

完成身份验证过程后，导航回 [!DNL Azure] 密钥库和选择 **[!DNL Access control]** 在左侧导航中。 从此处选择 **[!DNL Add]** 后接 **[!DNL Add role assignment]**.

![此 [!DNL Microsoft Azure] 仪表板 [!DNL Add] 和 [!DNL Add role assignment] 突出显示。](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

下一个屏幕提示您为此分配选择一个角色。 选择 **[!DNL Key Vault Crypto Service Encryption User]** 选择之前 **[!DNL Next]** 以继续。

![此 [!DNL Microsoft Azure] 仪表板，带有 [!DNL Key Vault Crypto Service Encryption User] 突出显示。](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

在下一个屏幕上，选择 **[!DNL Select members]** 以在右边栏中打开对话框。 使用搜索栏查找CMK应用程序的服务主体，并从列表中选择它。 完成后，选择 **[!DNL Save]**.

>[!NOTE]
>
>如果在列表中找不到您的应用程序，则表示您的服务主体尚未被租户接受。 为确保您拥有正确的权限，请与 [!DNL Azure] 管理员或代表。

您可以通过比较 [!UICONTROL 应用程序Id] 提供于 [!UICONTROL 客户管理的密钥配置] 使用查看 [!DNL Application ID] 提供于 [!DNL Microsoft Azure] 应用程序概述。

![此 [!UICONTROL 客户管理的密钥配置] 使用查看 [!UICONTROL 应用程序Id] 突出显示。](../../images/governance-privacy-security/customer-managed-keys/application-id.png)

验证Azure工具所需的所有详细信息都包含在Platform UI中。 提供了此级别的粒度，因为许多用户希望使用其他Azure工具来增强其监视和记录这些应用程序对其密钥保管库的访问的能力。 了解这些标识符对于实现此目标以及帮助Adobe服务访问密钥至关重要。

## 在Experience Platform上启用加密密钥配置 {#send-to-adobe}

在上安装CMK应用程序后 [!DNL Azure]，您可以将加密密钥标识符发送到Adobe。 选择 **[!DNL Keys]** ，后跟要发送的键的名称。

![Microsoft Azure功能板具有 [!DNL Keys] 对象和突出显示的键名。](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

选择键的最新版本，此时将显示其详细信息页面。 在此处，您可以选择为密钥配置允许的操作。

>[!IMPORTANT]
>
>该密钥允许的最低要求操作为 **[!DNL Wrap Key]** 和 **[!DNL Unwrap Key]** 权限。 您可以包括 [!DNL Encrypt]， [!DNL Decrypt]， [!DNL Sign]、和 [!DNL Verify] 你愿意的话。

此 **[!UICONTROL 密钥标识符]** 字段显示键的URI标识符。 复制此URI值以供在下一步中使用。

![Microsoft Azure功能板密钥详细信息和 [!DNL Permitted operations] 和高亮显示的复制密钥URL部分。](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

获得 [!DNL Key vault URI]，返回到 [!UICONTROL 客户管理的密钥配置] 查看并输入描述性 **[!UICONTROL 配置名称]**. 接下来，添加 [!DNL Key Identifier] 从Azure Key详细信息页面摄取到 **[!UICONTROL 密钥保管库密钥标识符]** 并选择 **[!UICONTROL 保存]**.

![此 [!UICONTROL 客户管理的密钥配置] 使用查看 [!UICONTROL 配置名称] 和 [!UICONTROL 密钥保管库密钥标识符] 高亮显示的部分。](../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

您将返回 [!UICONTROL 加密配置仪表板]. 的状态 [!UICONTROL 客户管理的密钥] 配置显示为 [!UICONTROL 正在处理].

![此 [!UICONTROL 加密配置] 仪表板 [!UICONTROL 正在处理] 突出显示于 [!UICONTROL 客户管理的密钥] 卡片。](../../images/governance-privacy-security/customer-managed-keys/processing.png)

## 验证配置的状态 {#check-status}

留出大量的处理时间。 要检查配置的状态，请返回至 [!UICONTROL 客户管理的密钥配置] 查看并向下滚动到 [!UICONTROL 配置状态]. 进度条已前进到第三步的第一步，并说明了系统正在验证Platform是否有权访问密钥和密钥保管库。

CMK配置有四种潜在状态。 具体如下：

* 步骤1：验证平台是否能够访问密钥和密钥保管库。
* 步骤2：正在将密钥保管库和密钥名称添加到组织中的所有数据存储中。
* 步骤3：已成功将密钥保管库和密钥名称添加到数据存储。
* `FAILED`：出现问题，主要与密钥、密钥库或多租户应用程序设置有关。

## 后续步骤

通过完成上述步骤，您已成功为组织启用CMK。 现在，摄取到主数据存储中的数据将使用 [!DNL Azure] 密钥库。
