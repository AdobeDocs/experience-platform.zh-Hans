---
title: Snowflake Source Connector概述
description: 了解如何使用API或用户界面将Snowflake连接到Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# [!DNL Snowflake]源

>[!IMPORTANT]
>
>* [!DNL Snowflake]源在源目录中可供已购买Real-Time Customer Data Platform Ultimate的用户使用。
>* 默认情况下，[!DNL Snowflake]源将`null`解释为空字符串。 请联系您的Adobe代表，以确保在Adobe Experience Platform中将您的`null`值正确写入`null`。
>* 要让Experience Platform摄取数据，必须将所有基于表的批处理源的时区配置为UTC时区。 [!DNL Snowflake]源支持的唯一时间戳是带有UTC时间的TIMESTAMP_NTZ。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从第三方数据库引入数据。 Experience Platform可以连接到各种类型的数据库，例如关系数据库、NoSQL数据库或数据仓库数据库。 对数据库提供程序的支持包括[!DNL Snowflake]。

## 先决条件 {#prerequisites}

本节概述在将[!DNL Snowflake]源连接到Experience Platform之前需要完成的设置任务。

### 检索帐户标识符 {#retrieve-your-account-identifier}

您必须从[!DNL Snowflake] UI仪表板中检索帐户标识符，因为您将使用该帐户标识符在Experience Platform上验证您的[!DNL Snowflake]实例。

要检索您的帐户标识符，请执行以下操作：

* 在[[!DNL Snowflake] 应用程序UI仪表板](https://app.snowflake.com/)上导航到您的帐户。
* 在左侧导航中，选择&#x200B;**[!DNL Accounts]**，然后从标题中选择&#x200B;**[!DNL Active Accounts]**。
* 接下来，选择信息图标，然后选择并复制当前URL的域名。

![选定域名的Snowflake UI仪表板。](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### 检索您的私钥 {#retrieve-your-private-key}

如果您正在对[!DNL Snowflake]连接使用密钥对身份验证，则您还必须在连接到Experience Platform之前生成私钥。

>[!BEGINTABS]

>[!TAB 创建加密的私钥]

要生成加密的[!DNL Snowflake]私钥，请在终端上运行以下命令：

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

如果成功，您应会收到PEM格式的私钥。

```shell
-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB 创建未加密的私钥]

要生成未加密的[!DNL Snowflake]私钥，请在终端上运行以下命令：

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

如果成功，您应会收到PEM格式的私钥。

```shell
-----BEGIN PRIVATE KEY-----
MIIE6T...
-----END PRIVATE KEY-----
```

>[!ENDTABS]

接下来，获取您的私钥并在[!DNL Base64]中进行编码。 请确保您未对[!DNL Snowflake]私钥进行任何转换或格式转换。 此外，您必须确保私钥的末尾没有尾随新行字符，然后才能在[!DNL Base64]中对其进行编码。

### 验证配置

在为[!DNL Snowflake]数据创建源连接之前，还必须确保满足以下配置：

* 分配给给定用户的默认仓库必须与在向Experience Platform进行身份验证时输入的仓库相同。
* 分配给给定用户的默认角色必须有权访问在对Experience Platform进行身份验证时输入的同一数据库。

要验证您的角色和仓库，请执行以下操作：

* 在左侧导航中选择&#x200B;**[!DNL Admin]**，然后选择&#x200B;**[!DNL Users & Roles]**。
* 选择相应的用户，然后选择右上角的省略号(`...`)。
* 在出现的[!DNL Edit user]窗口中，导航到[!DNL Default Role]以查看与给定用户关联的角色。
* 在同一窗口中，导航到[!DNL Default Warehouse]以查看与给定用户关联的仓库。

![可在其中验证您的角色和仓库的Snowflake UI。](../../images/tutorials/create/snowflake/snowflake-configs.png)

成功编码后，您可以在Experience Platform上使用该已编码的[!DNL Base64]私钥来验证您的[!DNL Snowflake]帐户。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

以下文档提供了有关如何使用API或用户界面将[!DNL Snowflake]连接到Experience Platform的信息：

## 使用API将[!DNL Snowflake]连接到Experience Platform

* [使用流服务API创建Snowflake基本连接](../../tutorials/api/create/databases/snowflake.md)
* [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

## 使用UI将[!DNL Snowflake]连接到Experience Platform

* [在UI中创建Snowflake源连接](../../tutorials/ui/create/databases/snowflake.md)
* [在用户界面中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)
