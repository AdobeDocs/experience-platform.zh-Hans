---
title: Snowflake流Source连接器概述
description: 了解如何创建源连接和数据流，以将流数据从Snowflake实例摄取到Adobe Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-09-24T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 1%

---

# [!DNL Snowflake]流源

>[!IMPORTANT]
>
>* [!DNL Snowflake]流源在API中可供已购买Real-Time CDP Ultimate的用户使用。
>
>* 在Amazon Web Services (AWS)上运行Adobe Experience Platform时，您现在可以使用[!DNL Snowflake]流源。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../landing/multi-cloud.md)。


Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从[!DNL Snowflake]数据库流式传输数据。

## 了解[!DNL Snowflake]流源

[!DNL Snowflake]流源通过定期执行SQL查询并为结果集中的每一行创建输出记录来加载数据。

通过使用[!DNL Kafka Connect]，[!DNL Snowflake]流源将跟踪它从每个表中收到的最新记录，以便它可以在下一个迭代的正确位置开始。 源使用此功能来筛选数据，并且只从每个迭代上的表中获取更新的行。

## 先决条件

以下部分概述了在将数据从[!DNL Snowflake]数据库流式传输到Experience Platform之前需要完成的先决步骤：

### 更新IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md#ip-address-allow-list-for-streaming-sources)页。

以下文档提供了有关如何使用API或用户界面将[!DNL Amazon Redshift]连接到Experience Platform的信息：

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL Snowflake]连接，您必须提供以下连接属性：

| 凭据 | 描述 |
| --- | --- |
| `account` | [!DNL Snowflake]帐户的完整帐户标识符（帐户名称或帐户定位器）附加了后缀`snowflakecomputing.com`。 帐户标识符可以具有不同的格式： <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com （如`acme-abc12345.snowflakecomputing.com`）</li><li>{ACCOUNT_LOCATOR}。{CLOUD_REGION_ID}.snowflakecomputing.com （如`acme12345.ap-southeast-1.snowflakecomputing.com`）</li><li>{ACCOUNT_LOCATOR}。{CLOUD_REGION_ID}。{CLOUD}.snowflakecomputing.com （如`acme12345.east-us-2.azure.snowflakecomputing.com`）</li></ul> 有关详细信息，请阅读[[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>)。 |
| `warehouse` | [!DNL Snowflake]仓库管理应用程序的查询执行过程。 每个[!DNL Snowflake]仓库彼此独立，在将数据传送到Experience Platform时必须单独访问。 |
| `database` | [!DNL Snowflake]数据库包含要带Experience Platform的数据。 |
| `username` | [!DNL Snowflake]帐户的用户名。 |
| `password` | [!DNL Snowflake]用户帐户的密码。 |
| `role` | （可选）可以为给定连接的用户提供自定义角色。 如果未提供，此值默认为`public`。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Snowflake]的连接规范ID为`51ae16c2-bdad-42fd-9fce-8d5dfddaf140`。 |

{style="table-layout:auto"}

### 配置角色设置 {#configure-role-settings}

即使分配了默认公共角色，也必须配置角色的权限，以允许源连接访问相关[!DNL Snowflake]数据库、架构和表。 不同[!DNL Snowflake]实体的各种权限如下所示：

| [!DNL Snowflake]实体 | 需要角色权限 |
| --- | --- |
| 仓库 | 操作、使用 |
| 数据库 | 使用情况 |
| 架构 | 使用情况 |
| 表 | 选择 |

>[!NOTE]
>
>必须在仓库的高级设置配置中启用自动恢复和自动暂停。

有关角色和权限管理的详细信息，请参阅[[!DNL Snowflake] API参考](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>)。

## 限制和常见问题解答 {#limitations-and-frequently-asked-questions}

* [!DNL Snowflake]源的数据吞吐量为每秒2000条记录。
* 根据仓库的活动时间和仓库的大小，定价可能会有所不同。 对于[!DNL Snowflake]源集成，最小大小x小仓库就足够了。 建议启用自动暂停，以便仓库在不使用时能够自行暂停。
* [!DNL Snowflake]源每10秒轮询数据库一次新数据。
* 配置选项：
   * 创建源连接时，您可以为[!DNL Snowflake]源启用`backfill`布尔标记。
      * 如果回填设置为true ，则timestamp.initial的值将设置为0。 这意味着获取时间戳列大于0纪元时间的数据。
      * 如果回填设置为false，则timestamp.initial的值将设置为–1。 这意味着获取时间戳列大于当前时间（源开始摄取的时间）的数据。
   * 时间戳列的格式应该是： `TIMESTAMP_LTZ`或`TIMESTAMP_NTZ`。 如果时间戳列设置为`TIMESTAMP_NTZ`，则应通过`timezoneValue`参数传递存储值的相应时区。 如果未提供，该值将默认为UTC。
      * `TIMESTAMP_TZ`不能用于时间戳列或映射。

## 后续步骤

以下教程提供了有关如何使用API将[!DNL Snowflake]流源连接到Experience Platform的步骤：

* [使用流服务API将数据从 [!DNL Snowflake] 数据库流入Experience Platform](../../tutorials/api/create/databases/snowflake-streaming.md)
* [使用Experience Platform用户界面中的源工作区将数据从 [!DNL Snowflake] 数据库流式传输到Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
