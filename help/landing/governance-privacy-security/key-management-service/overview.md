---
title: 如何使用Amazon Web Services密钥管理服务进行Adobe Experience Platform数据加密
description: 了解如何使用Amazon Web Services密钥管理服务为Adobe Experience Platform中存储的数据设置加密密钥。
role: Developer, Admin, User
hide: true
hidefromtoc: true
source-git-commit: 7c37ce72eecbcbc9e49aa4135a21ef4649d9bfa5
workflow-type: tm+mt
source-wordcount: '2663'
ht-degree: 0%

---

# 如何使用Amazon Web Services密钥管理服务进行Adobe Experience Platform数据加密

>[!AVAILABILITY]
>
>本文档适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform多云概述](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud)。
>
>AWS上的[客户管理的密钥](../customer-managed-keys/overview.md) (CMK)支持Privacy and Security Shield，但不适用于Healthcare Shield。 Privacy和Security Shield以及Healthcare Shield均支持Azure上的CMK。

使用本指南，通过创建、管理和控制Amazon Web Services (AWS)的加密密钥，使用Adobe Experience Platform (KMS)密钥管理服务(KMS)保护您的数据。 此集成简化了法规遵从性，通过自动化简化了操作，并且消除了维护您自己的关键管理基础架构的需要。

有关特定于Customer Journey Analytics的说明，请参阅[Customer Journey AnalyticsCMK文档](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-privacy/cmk)

>[!IMPORTANT]
>
>默认情况下，Adobe Experience Platform使用系统管理的密钥加密静态数据。 通过启用客户管理的密钥(CMK)，您可以完全控制数据安全。 但是，此更改是不可逆的，一旦启用CMK，您就无法还原到系统管理的密钥。 您有责任安全地管理您的密钥，以确保对数据的访问不会出现中断，并防止潜在的不可访问性。

本指南详细介绍了在AWS KMS中创建和管理加密密钥以保护Experience Platform中数据的过程。

## 先决条件 {#prerequisites}

在继续阅读本文档之前，您应该充分了解以下关键概念和功能：

- **AWS密钥管理服务(KMS)**：了解AWS KMS的基础知识，包括如何创建、管理和轮换加密密钥。 有关详细信息，请参阅[KMS官方文档](https://docs.aws.amazon.com/kms/)。
- AWS中的&#x200B;**身份和访问管理(IAM)策略**： IAM是一项允许您安全管理对AWS服务和资源的访问权限的服务。 使用IAM可以：
   - 定义哪些用户、组和角色有权访问特定资源。
   - 指定允许或拒绝用户执行的操作。
   - 通过使用IAM策略分配权限来实施细粒度访问控制。
有关详细信息，请参阅[适用于AWS KMS的IAM策略官方文档](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html)。
- **Experience Platform中的数据安全**：了解Platform如何确保数据安全并与AWS KMS等外部服务集成以进行加密。 Platform使用HTTPS TLS v1.2保护数据以便传输、云提供商静态加密、隔离存储以及可自定义的身份验证和加密选项。 有关如何保持数据安全的更多信息，请参阅[治理、隐私和安全概述](../overview.md)或有关Platform中[数据加密](../encryption.md)的文档。
- **AWS管理控制台**：一个中心中心，您可以从基于Web的应用程序访问和管理所有AWS服务。 使用搜索栏快速查找工具、检查通知、管理您的帐户和账单，以及自定义您的设置。 有关详细信息，请参阅[官方的AWS管理控制台文档](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/what-is.html)。

## 快速入门 {#get-started}

本指南要求您已经拥有Amazon Web Services帐户的访问权限和管理控制台的访问权限。 请按照以下步骤开始：

1. **验证权限**：确保您拥有必要的AWS Identity and Access Management (IAM)权限，以便在KMS中创建、管理和使用加密密钥。 要验证您的权限，请执行以下操作：
   1. 访问[IAM策略模拟器](https://policysim.aws.amazon.com/)。
   1. 选择您的用户帐户或角色。
   1. 模拟KMS操作，如`kms:CreateKey`或`kms:Encrypt`。
如果模拟返回错误或您不确定自己的权限，请联系AWS管理员以获取帮助。

1. **检查您的AWS帐户配置**：确认您的AWS帐户已启用使用AWS KMS服务。 大多数帐户默认启用KMS访问权限，但您可以通过访问[AWS管理控制台](https://aws.amazon.com/console/)来查看帐户设置。 有关详细信息，请参阅[AWS Key Management Service开发人员指南](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)。

1. **选择支持的区域**：AWS KMS在特定区域可用。 确保您在支持KMS的区域中运行。 您可以在[AWS KMS端点和配额列表](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)中查看受支持地区的完整列表。

### 导航到AWS KMS以开始设置键

>[!IMPORTANT]
>
>确保加密密钥的安全存储、访问和可用性。 您负责管理密钥并防止对Platform操作造成中断。

要开始设置和管理加密密钥，请登录到您的AWS帐户，然后导航到AWS密钥管理服务(KMS)。 从AWS Management Console中，从服务菜单中选择&#x200B;**密钥管理服务(KMS)**。

![突出显示密钥管理服务的AWS Management Console的“搜索”下拉菜单。](../../images/governance-privacy-security/key-management-service/navigate-to-kms.png)

## 创建新密钥 {#create-a-key}

出现[!DNL Key Management Service (KMS)]工作区。 选择 **[!DNL Create a key]**。

![Create a key的密钥管理服务工作区突出显示。](../../images/governance-privacy-security/key-management-service/create-a-key.png)

## 配置密钥设置 {#configure-key}

出现[!DNL Configure Key]工作流。 默认情况下，密钥类型设置为&#x200B;**[!DNL Symmetric]**，密钥用法设置为&#x200B;**[!DNL Encrypt and Decrypt]**。 在继续之前，请确保已选择这些选项。

![突出显示了“对称”和“加密和解密”基本选项的“配置密钥”工作流的第一步。](../../images/governance-privacy-security/key-management-service/configure-key-basic-options.png)

展开&#x200B;**[!DNL Advanced options]**&#x200B;下拉菜单。 建议您使用&#x200B;**[!DNL KMS]**&#x200B;选项，该选项允许AWS创建和管理密钥资料。 默认情况下已选中&#x200B;**[!DNL KMS]**&#x200B;选项。

>[!NOTE]
>
>如果您已经拥有现有的密钥，则可以导入外部密钥资料或使用AWS [!DNL CloudHSM]密钥库。 这些选项不在本文档的范围之内。

接下来，选择[!DNL Regionality]设置，该设置指定键的区域范围。 选择&#x200B;**[!DNL Single-Region key]**，然后选择&#x200B;**[!DNL Next]**&#x200B;以继续执行步骤2。

>[!IMPORTANT]
>
>AWS对KMS密钥实施区域限制。 此区域限制意味着密钥必须位于与您的Adobe帐户相同的区域中。 Adobe只能访问位于您帐户所在地区的KMS密钥。 确保您选择的地区与Adobe单租户帐户的地区匹配。

![Configure key工作流的第一步，其中突出显示AWS区域、KMS和单区域键高级选项。](../../images/governance-privacy-security/key-management-service/configure-key-advanced-options.png)

## 为密钥添加标签和标记 {#add-labels-and-tags-to-key}

此时将显示工作流的第二个[!DNL Add labels]阶段。 在此，您可以配置[!DNL Alias]和[!DNL Tags]字段以帮助您从AWS KMS控制台管理和查找加密密钥。

在&#x200B;**[!DNL Alias]**&#x200B;输入字段中输入键的描述性标签。 别名充当用户友好标识符，以使用AWS KMS控制台中的搜索栏快速找到密钥。 为避免混淆，请选择一个能反映密钥目的的有意义的名称，如“Adobe — 平台 — 密钥”或“客户 — 加密 — 密钥”。 如果键别名不足以描述其用途，您还可以包含键的说明。

最后，通过在[!DNL Tags]部分中添加键值对来为键分配元数据。 此步骤是可选的，但您应该添加标记以对AWS资源进行分类和筛选，从而更便于管理。 例如，如果贵组织使用多个与Adobe相关的资源，则可以使用“Adobe”或“Experience-Platform”来标记它们。 通过这个额外的步骤，可以轻松地在AWS Management Console中搜索和管理所有关联的资源。 选择&#x200B;**[!DNL Add tag]**&#x200B;开始该进程。

<!-- I do not have an AWS account with which to document the Add tag process as yet. -->

如果您对设置感到满意，请选择&#x200B;**[!DNL Next]**&#x200B;以继续工作流。

![Configure key工作流的第二步，突出显示“别名”、“描述”、“标记”和“下一步”。](../../images/governance-privacy-security/key-management-service/add-labels.png)

## 定义关键管理权限 {#define-key-admins}

此时会显示密钥创建工作流的步骤3。 为确保访问安全和受控，您可以选择哪些IAM用户和角色可以管理密钥。 此阶段有两个选项，[!DNL Key administrators]和[!DNL Key deletion]。 在&#x200B;**[!DNL Key administrators]**&#x200B;部分中，选中您要授予此密钥的管理员权限的任何用户或角色名称旁边的一个或多个复选框。

>[!NOTE]
>
>您无法在此工作流阶段创建管理员。

在&#x200B;**[!DNL Key deletion]**&#x200B;部分中，启用该复选框以允许密钥管理员删除此密钥。 如果不选中该复选框，则不允许管理用户执行该操作。

选择&#x200B;**[!DNL Next]**&#x200B;以继续工作流。

![工作流的“定义关键管理权限”阶段，带有复选框和下一个突出显示。](../../images/governance-privacy-security/key-management-service/define-key-admins.png)

## 向关键用户授予访问权限 {#assign-key-users}

在工作流的第四步，您可以[!DNL Define key usage permissions]。 从&#x200B;**[!DNL Key users]**&#x200B;列表中，选中要拥有使用此密钥的权限的所有IAM用户和角色的复选框。

从这种观点来看，您也可以[!DNL Add another AWS account]；但是，强烈建议不要添加其他AWS帐户。 添加另一个帐户可能会带来风险，并使加密和解密操作的权限管理复杂化。 通过保持与单个AWS帐户关联的密钥，Adobe可确保与AWS KMS的安全集成，从而最大程度地降低风险并确保可靠的操作。

选择&#x200B;**[!DNL Next]**&#x200B;以继续工作流。

![工作流的“定义密钥使用权限”阶段，带有复选框和下一个突出显示。](../../images/governance-privacy-security/key-management-service/define-key-users.png)

## 查看关键配置 {#review}

此时将显示关键配置的审核阶段。 验证[!DNL Key configuration]和[!DNL Alias and description]部分中的键详细信息。

>[!NOTE]
>
>确保关键区域与AWS帐户相同。

![工作流的“审阅”阶段，其中重点介绍了“键配置”和“别名”及描述部分。](../../images/governance-privacy-security/key-management-service/review-key-configuration-details.png)

### 更新密钥策略以将密钥与Experience Platform集成

接下来，编辑&#x200B;**[!DNL Key Policy]**&#x200B;部分中的JSON以将该键与Experience Platform相集成。 默认密钥策略类似于下面的JSON。

<!-- The AWS ID below is fake. Q) Can I refer to it simply as AWS_ACCOUNT_ID ? Is that suitable? -->

```JSON
{
  "Id": "key-consolepolicy-3",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Enable IAM User Permissions",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123464903283:root" // this is a mock AWS Principal ID, your ID will differ
      },
      "Action": "kms:*",
      "Resource": "*"
    }
  ]
}
```

在上述示例中，同一帐户(`Principal.AWS`)中的所有资源(`"Resource": "*"`)都可以访问此密钥。 该策略允许同一帐户中的其他服务使用该密钥进行加密和解密。 服务仅具有此帐户的权限。

接下来，通过向此策略添加新语句，授予您的Platform单个租户帐户访问此密钥的权限。 您可以从Platform UI获取JSON策略，并将其应用于AWS KMS密钥，以便安全地将其链接到平台。

导航到Platform UI。 在左侧导航边栏的&#x200B;**[!UICONTROL 管理]**&#x200B;部分中，选择&#x200B;**[!UICONTROL 加密]**。 出现[!UICONTROL 加密配置]工作区。 然后在[!UICONTROL 客户管理的密钥]卡中选择&#x200B;**[!UICONTROL 配置]**。

![客户管理的密钥卡中突出显示的配置平台加密配置工作区。](../../images/governance-privacy-security/key-management-service/encryption-configuration.png)

出现[!UICONTROL 客户托管密钥配置]。 选择复制图标(![复制图标。](../../../images/icons/copy.png))以将CMK KMS策略复制到剪贴板。 绿色弹出通知确认策略已复制。

![显示CMK KMS策略并突出显示复制图标的客户托管密钥配置。](../../images/governance-privacy-security/key-management-service/copy-cmk-policy.png)

<!-- This part of the workflow was in contention at the time of the demo.  -->

接下来，返回到AWS KMS工作区并更新下面显示的密钥策略。

![工作流的“审阅”阶段中更新了策略并突出显示了“完成”。](../../images/governance-privacy-security/key-management-service/updated-cmk-policy.png)

将[!UICONTROL 平台加密配置]工作区中的四个语句添加到默认策略中，如下所示： `Enable IAM User Permissions`、`CJA Flow IAM User Permissions`、`CJA Integrity IAM User Permissions`、`CJA Oberon IAM User Permissions`。

```json
{
    "Version": "2012-10-17",
    "Id": "key-consolepolicy",
    "Statement": [
        {
            "Sid": "Enable IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::975049898882:root" // this is a mock AWS Principal ID, your ID will differ
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "975049898882" // this is a mock AWS Principal ID, your ID will differ
                }
            }
        },
        {
            "Sid": "CJA Flow IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::767397686373:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "767397686373"
                }
            }
        },
        {
            "Sid": "CJA Integrity IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::730335345392:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "730335345392"
                }
            }
        },
        {
            "Sid": "CJA Oberon IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::891377157113:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "891377157113"
                }
            }
        }
    ]
}
```



选择&#x200B;**[!DNL Finish]**&#x200B;以使用更新后的策略确认您的密钥详细信息并创建密钥。 密钥和策略现在已配置为总共五项语句，以允许您的AWS帐户与您的Experience Platform帐户通信。 效果是瞬时的。

将显示AWS [!DNL Key Management Service]的已更新[!DNL Customer managed keys]工作区。

### 将AWS加密密钥详细信息添加到平台

接下来，要启用加密，请将密钥的Amazon资源名称(ARN)添加到平台[!UICONTROL 客户托管密钥配置]。 在AWS的[!DNL Customer Managed Keys]部分中，从[!DNL Key Management Service]的列表中选择新密钥的别名。

![高亮显示新密钥别名的AWS KMS客户托管密钥工作区。](../../images/governance-privacy-security/key-management-service/customer-managed-keys-on-aws.png)

此时将显示键的详细信息。 AWS中的所有内容都有一个Amazon资源名称(ARN)，该名称包含
是用于跨AWS服务指定资源的唯一标识符。 它遵循标准化格式： `arn:partition:service:region:account-id:resource`。

选择复制图标以复制您的ARN。 将显示确认对话框。

![突出显示了ARN的AWS KMS客户管理的密钥的密钥详细信息。](../../images/governance-privacy-security/key-management-service/keys-details-arn.png)

现在，导航回平台[!UICONTROL 客户托管密钥配置] UI。 在&#x200B;**[!UICONTROL 添加AWS加密密钥详细信息]**&#x200B;部分中，添加从AWS UI复制的&#x200B;**[!UICONTROL 配置名称]**&#x200B;和&#x200B;**[!UICONTROL KMS密钥ARN]**。

![在“添加AWS加密密钥详细信息”部分中突出显示的具有配置名称和KMS密钥ARN的平台加密配置工作区。](../../images/governance-privacy-security/key-management-service/add-encryption-key-details.png)

接下来，选择&#x200B;**[!UICONTROL SAVE]**&#x200B;以提交配置名称、KMS密钥ARN，并开始验证密钥。

![已高亮显示保存的Platform Encryption Configuration工作区。](../../images/governance-privacy-security/key-management-service/save.png)

返回[!UICONTROL 加密配置]工作区。 加密配置的状态显示在&#x200B;**[!UICONTROL 客户管理的密钥]**&#x200B;卡的底部。

![客户管理的密钥卡上突出显示的带处理功能的平台UI中的加密配置工作区。](../../images/governance-privacy-security/key-management-service/configuration-status.png)

验证密钥后，密钥保管库标识符将添加到所有沙盒的数据湖和配置文件数据存储中。

>[!NOTE]
>
>该过程的持续时间取决于您的数据大小。 通常，该过程在24小时内完成。 每个沙盒通常在2到3分钟内更新。

## 密钥撤销 {#key-revocation}

>[!IMPORTANT]
>
>在撤销任何访问之前，请了解密钥撤销对下游应用程序的影响。

以下是密钥撤销的关键注意事项：

- 撤销或禁用密钥将导致无法访问您的Platform数据。 此操作不可逆，应谨慎执行。
- 在撤销对加密密钥的访问时，请考虑传播时间线。 在几分钟到24小时内无法访问主数据存储。 缓存或临时数据存储在7天内变得不可访问。

要撤销密钥，请导航到AWS KMS工作区。 **[!DNL Customer managed keys]**&#x200B;部分显示您的AWS帐户的所有可用密钥。 从列表中选择密钥的别名。

![高亮显示新密钥别名的AWS KMS客户托管密钥工作区。](../../images/governance-privacy-security/key-management-service/customer-managed-keys-on-aws.png)

此时将显示键的详细信息。 要禁用该键，请从下拉菜单中选择&#x200B;**[!DNL Key actions]**，然后选择&#x200B;**[!DNL Disable]**。

![AWS KMS UI中AWS键的详细信息，其中突出显示了键操作和禁用。](../../images/governance-privacy-security/key-management-service/disable-key.png)

将显示确认对话框。 选择&#x200B;**[!DNL Disable key]**&#x200B;以确认您的选择。 禁用键的影响应在大约五分钟内反映在Platform应用程序和UI中。

>[!NOTE]
>
>禁用密钥后，如果需要，可以使用上述相同方法再次启用密钥。 此选项可从&#x200B;**[!DNL Key actions]**&#x200B;下拉菜单中获取。

![突出显示了“禁用键”的“禁用键”对话框。](../../images/governance-privacy-security/key-management-service/disable-key-dialog.png)

或者，如果您的密钥跨其他服务使用，则可以直接从密钥策略中删除Experience Platform的访问权限。 在&#x200B;**[!DNL Key Policy]**&#x200B;部分中选择&#x200B;**[!UICONTROL 编辑]**。

![在“键策略”部分中突出显示了“编辑的AWS键的详细信息部分。](../../images/governance-privacy-security/key-management-service/edit-key-policy.png)

此时会显示&#x200B;**[!DNL Edit key policy]**&#x200B;页面。 突出显示并删除从Platform UI复制的策略语句，以删除客户管理的密钥应用程序的权限。 然后，选择&#x200B;**[!DNL Save changes]**&#x200B;以完成该过程。

![AWS上的Edit key policy工作区中突出显示了语句JSON对象和Save更改。](../../images/governance-privacy-security/key-management-service/delete-statement-and-save-changes.png)

## 密钥轮替 {#key-rotation}

AWS提供自动和按需密钥轮替。 为了降低密钥泄露的风险或满足安全合规性要求，您可以根据需要或定期自动生成新的加密密钥。 计划自动密钥轮换以限制密钥的生命周期，并确保如果密钥受损，其在轮换后不可用。 虽然现代加密算法高度安全，但密钥轮换是一项重要的安全合规性措施，并表明遵守了安全最佳实践。

### 自动密钥轮替 {#automatic-key-rotation}

默认情况下禁用自动密钥轮替。 要从KMS工作区计划自动密钥轮替，请选择&#x200B;**[!DNL Key rotation]**&#x200B;选项卡，然后在&#x200B;**[!DNL Automatic key rotation section]**&#x200B;中选择&#x200B;**[!DNL Edit]**。

![突出显示了AWS键的详细信息部分（包含键轮换和编辑）。](../../images/governance-privacy-security/key-management-service/key-rotation.png)

出现&#x200B;**[!DNL Edit automatic key rotation]**&#x200B;工作区。 在此处，选择单选按钮以启用或禁用自动密钥轮替。 然后，使用文本输入字段或下拉菜单为键旋转选择时间段。 选择&#x200B;**[!DNL Save]**&#x200B;以确认您的设置并返回密钥详细信息工作区。

>[!NOTE]
>
>密钥轮换的最小周期为90天，最大周期为2560天。

![编辑自动密钥轮换工作区，其中轮换时段和保存突出显示。](../../images/governance-privacy-security/key-management-service/automatic-key-rotation.png)

### 按需密钥轮换 {#on-demand-key-rotation}

如果当前密钥受损，请选择&#x200B;**[!DNL Rotate Now]**&#x200B;以立即轮换它。 AWS仅允许10次按需轮换。 除非安全性已受损，否则请使用计划的密钥轮换。

![带有“立即旋转”的AWS键的详细信息部分突出显示。](../../images/governance-privacy-security/key-management-service/on-demand-key-rotation.png)

## 后续步骤

阅读本文档后，您已了解如何在AWS KMS中创建、配置和管理加密密钥以用于Adobe Experience Platform。 接下来，请考虑审查您组织的安全性和法规遵从性策略，以确保适当的密钥管理做法，如计划的密钥轮换和安全密钥存储。
