---
title: CMK警报解决参考
description: 识别、排除和解决Adobe Experience Platform中由客户管理的密钥(CMK)配置错误触发的常见警报。 使用本指南来遵循清晰的分步说明并恢复安全密钥访问。
exl-id: ffe2eadc-dfb5-418b-a201-2c20dcc9cfe4
source-git-commit: e8cfed9ebd50cf50f03e232755eddef1cb8c0d3b
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# CMK警报解决参考

使用本指南可以排除和解决由Adobe Experience Platform中客户管理的密钥(CMK)设置配置错误触发的警报。 它可帮助系统管理员和实施专家找出原因并应用解决方案来恢复安全访问。

## 警报类别 {#categories}

以下部分概述了Adobe Experience Platform中可能由客户管理的密钥(CMK)问题触发的警报类型：

- [已禁用密钥访问](#key-access-disabled)
- [密钥访问失败](#key-access-failure)
- [警报通知](#alert-notification)

## 已禁用密钥访问 {#key-access-disabled}

此警报表示Adobe Experience Platform无法访问配置的CMK，因为此密钥已禁用或因其配置而无法访问。 在这种情况下，系统将该情况视为有意删除关键访问。

### 发生时间

当Azure Key Vault中的加密密钥处于禁用状态、被删除或配置错误，从而阻止在平台操作期间进行访问时，将触发此警报。

### 可能的原因

出现此警报的常见原因如下：

- 已手动禁用该键。
- 已删除关键操作(wrapKey/unwrapKey)。
- 密钥激活日期是将来的设置。
- 密钥到期日期已过去。
- 已删除键。
- 已删除或更改多租户应用程序权限。
- 已删除多租户应用程序。
- 已更改多租户应用程序属性。
- 密钥库已被删除或无法再访问。

### 解决方法

+++如果键被禁用

1. 导航到包含CMK的[Azure密钥保管库](https://portal.azure.com/)。
2. 选择与Adobe Experience Platform关联的键。
3. 验证密钥的状态是否设置为&#x200B;**已启用**。
4. 如果密钥被禁用，请使用Azure门户或CLI命令`az keyvault key enable`启用它。

>[!NOTE]
>
>为您的Azure环境自定义此命令。

+++

+++如果关键操作已更改

1. 将`wrapKey`和`unwrapKey`权限重新添加到密钥。

>[!NOTE]
>
>密钥的所有设置（包括激活和到期日期）都必须有效，密钥才能正常工作。

+++

+++如果激活或到期日期配置错误

1. 将激活日期设置为过去或现在。
2. 将到期日期设置为将来的日期。

+++

+++如果键已被删除

1. 确保在Azure密钥库中启用了软删除。
2. 在Azure门户或CLI中导航到“管理已删除的密钥”。
3. 从软删除项列表中选择已删除的键。
4. 单击&#x200B;**恢复**&#x200B;以恢复密钥。

+++

+++如果删除或更改了多租户应用程序权限

1. 恢复多租户应用程序的正确权限。
2. 确保已授予以下权限： `Key Vault Crypto Service Encryption User`

+++

+++如果多租户应用程序已删除

这是一个重大变化。 您必须联系Adobe以恢复或重新生成多租户应用程序。

+++

+++如果多租户应用程序设置已更改

1. 还原对与多租户应用程序关联的属性所做的更改。

+++

+++如果密钥库已删除

1. 确认已在Azure中启用软删除。
2. 在门户或CLI中导航到“管理已删除的存储库”。
3. 在保留期（7-90天）内恢复已删除的存储库。
4. 如果禁用了清除保护，您仍可以恢复保险库。

>[!NOTE]
>
>如果未正确配置软删除或清除保护，则可能无法恢复密钥或保险库。

+++

## 密钥访问失败 {#key-access-failure}

此警报表示Adobe Experience Platform由于网络级别或基于配置的拒绝访问而无法访问CMK。

>[!IMPORTANT]
>
>这被视为可恢复的错误。 在这种情况下，数据在SLA下&#x200B;**未**&#x200B;清除。

### 发生时间

此警报通常在未将Key Vault防火墙配置为允许Adobe CMK访问或基于身份的访问失败时触发。

### 可能的原因

- 密钥保管库防火墙正在阻止Adobe的静态IP (`20.88.123.53`)
- 密钥在预期位置不再存在
- Adobe多租户应用程序权限缺失
- 密钥库已删除或配置错误
- 多租户应用程序的对象ID已更改

### 解决方法

+++如果密钥库或密钥不再存在

1. 验证密钥保管库和加密密钥是否仍然存在。
2. 如果密钥被删除，请按照“密钥访问被禁用”下的软删除恢复步骤操作。

+++

+++如果多租户应用程序权限缺失或更改

1. 确认Adobe多租户应用程序具有以下权限：
   - 键上的`get`、`wrapKey`和`unwrapKey`。
2. 检查多租户应用程序的对象ID是否正确。 如果更改，则重新应用权限。

+++

+++如果防火墙阻止Adobe

1. 查看Azure Key Vault中的防火墙规则。
2. 确保它们允许从Adobe的静态IP进行访问： `20.88.123.53`。

>[!NOTE]
>
>即使拥有正确的权限，被阻止的IP也会阻止密钥访问。

+++

## 警报通知 {#alert-notification}

此警报将用作与已知故障类型不匹配的CMK配置或访问异常的常规通知。

>[!NOTE]
>
>此警报可能反映内部错误、新的配置错误或意外情况。

### 发生时间

当Adobe CMK在密钥访问或监视期间检测到未知、不支持或新问题时，将显示此警报。

### 可能的原因

- 意外防火墙/网络状况
- 预定义警报类型未涵盖的密钥或保险库更改
- Adobe内部网络中断
- Adobe配置错误，这在以前是前所未见的

### 解决方法

+++如果原因不明或不明确

1. 查看警报消息以了解任何上下文详细信息。
2. 检查防火墙、保险库和密钥设置以了解最近的更改。
3. 如果未找到明确的原因，请联系Adobe支持人员以获取指导。
4. 监控日志和系统行为以识别模式。

+++

## 后续步骤

若要了解如何触发警报以及如何为[!DNL Azure] CMK配置IP 列入允许列表 列入允许列表，请参阅[为Azure CMK配置警报和IP指南](./azure/alerts-and-ip-access.md)。
