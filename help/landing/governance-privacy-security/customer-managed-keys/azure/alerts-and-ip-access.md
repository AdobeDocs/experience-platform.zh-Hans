---
title: 列入允许列表为Azure CMK配置警报和IP
description: 了解如何在Azure Key Vault中允许列表Adobe的静态IP地址，并了解Experience Platform警报如何帮助检测和解决客户管理的密钥访问问题。
source-git-commit: 719273798954b70460c77711ef5eda5f9d22cdb0
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# 列入允许列表为[!DNL Azure] CMK配置警报和IP

为了提高透明度，Adobe提供了一个[监控服务](../../../../observability/alerts/ui.md){target="_blank"}，用于检查您的密钥保管库的访问状态，并在发生问题时触发警报。 这些警报可帮助您快速响应并避免服务中断。 要启用此服务，请允许列表Adobe的静态IP地址。

>[!IMPORTANT]
>
>如果您已禁用公共网络访问或将[!DNL Azure]密钥库配置为仅允许选定的网络，则必须将Adobe列入允许列表的静态IP地址添加到中。 如果没有该工具，您可能无法收到有关可能会影响Experience Platform实例的访问问题的通知。

## 在[!DNL Azure]密钥库中允许列表Adobe的静态IP {#add-adobe-static-ip}

要启用这些警报并保持网络限制，请导航到您的&#x200B;**[!DNL Azure Key Vault]** > **[!DNL Networking settings]**。 在&#x200B;**[!DNL Firewalls and virtual networks]**&#x200B;选项卡中，选择&#x200B;**[!DNL Allow public access from specific virtual networks and IP addresses]**。

![[!DNL Azure] Key Vault Networking设置屏幕，其中显示添加Adobe静态IP地址的位置并突出显示允许从以下位置访问的选项。](../../../images/governance-privacy-security/customer-managed-keys/key-vault-networking-settings.png)

### Adobe的静态IP地址

>[!IMPORTANT]
>
>Adobe提供的静态IP地址为： `20.88.123.53`。

接下来，在&#x200B;**[!DNL Firewall]**&#x200B;部分中，选择&#x200B;**[!DNL Add your current IP address]**&#x200B;并将其替换为Adobe的静态IP地址。 所有出站连接都被视为生产环境，因此必须列入允许列表此静态IP地址，以确保在受限网络配置中不间断地访问您的密钥保管库。

>[!NOTE]
>
>在[!DNL Azure]密钥库设置中添加或更新静态IP地址后，最多允许10分钟以使更改生效。 添加IP后，CMK应用程序会访问密钥库以验证权限。

在列入允许列表Adobe的静态IP后，Experience Platform可以监控对您的密钥库的访问并在出现问题时触发警报。 这些警报会提供早期警告，这样您可以在服务受到影响之前采取行动。 下一部分详细介绍可以接收的警报类型以及如何响应。

## 监测警报 {#monitor-alerts}

平台警报通知您可能会中断密钥访问的问题，例如&#x200B;**[!UICONTROL 密钥访问失败]**&#x200B;或&#x200B;**[!UICONTROL 密钥禁用]**。 这些警报可帮助您快速识别已删除的静态IP或错误配置的防火墙等问题。 要恢复访问，请检查[!DNL Azure]防火墙设置并重新添加所需的IP地址。

<!-- For a complete list of alert types and recommended resolutions, see the [CMK alert resolution reference](../alert-resolution-reference.md). -->

订阅Adobe I/O事件通知，以便在监控工具中接收实时警报。 有关设置说明，请参阅[订阅Adobe I/O事件通知](../../../../observability/alerts/subscribe.md)。 您还可以参阅[警报UI指南](../../../../observability/alerts/ui.md)，了解如何在Experience Platform中查看和管理警报。

## 后续步骤

您现在已为[!DNL Azure]密钥库配置了IP列入允许列表和警报监视。 要在[!DNL Azure]中完成客户托管密钥的设置，请遵循这些配置指南。

- [配置 [!DNL Azure] 密钥保管库](./azure-key-vault-config.md)
- [使用API设置CMK](./api-set-up.md)
- [使用用户界面设置CMK](./ui-set-up.md)
