---
title: Snowflake流源连接器概述
description: 了解如何创建源连接和数据流，以将流数据从Snowflake实例摄取到Adobe Experience Platform
badgeBeta: label="Beta 版" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: c80535cbb5dda55f1cf145f9f40bbcd40c78e63e
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 1%

---

# [!DNL Snowflake] 流源

>[!IMPORTANT]
>
>* 此 [!DNL Snowflake] 流源为测试版。 请阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记源代码的更多信息。
>* 此 [!DNL Snowflake] API中的流源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从流式传输数据 [!DNL Snowflake] 数据库。

## 了解 [!DNL Snowflake] 流源

此 [!DNL Snowflake] 流源的工作方式是：通过定期执行SQL查询来加载数据，并为结果集中的每一行创建输出记录。

通过使用 [!DNL Kafka Connect]， [!DNL Snowflake] 流源会跟踪它从每个表收到的最新记录，以便它可以在正确的位置开始下一次迭代。 源使用此功能来筛选数据，并且只从每个迭代上的表中获取更新的行。

## 先决条件

以下部分概述了从以下位置流式传输数据之前需要完成的先决步骤： [!DNL Snowflake] 要Experience Platform的数据库：

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL Snowflake]中，您必须提供以下连接属性：

| 凭据 | 描述 |
| --- | --- |
| `account` | 与您的帐户关联的完整帐户名称 [!DNL Snowflake] 帐户。 完全合格的 [!DNL Snowflake] 帐户名称包括您的帐户名称、地区和云平台。 例如：`cj12345.east-us-2.azure`。有关帐户名称的更多信息，请参阅此 [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | 此 [!DNL Snowflake] warehouse管理应用程序的查询执行过程。 每个 [!DNL Snowflake] 数据仓库相互独立，在将数据传送到Platform时必须单独进行访问。 |
| `database` | 此 [!DNL Snowflake] 数据库包含您要带入Platform的数据。 |
| `username` | 的用户名 [!DNL Snowflake] 帐户。 |
| `password` | 的密码 [!DNL Snowflake] 用户帐户。 |
| `role` | （可选）可以为给定连接的用户提供自定义角色。 如果未提供，则此值默认为 `public`. |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL Snowflake] 是 `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |


### 配置角色设置 {#configure-role-settings}

即使分配了默认公共角色，您也必须配置角色的权限，以允许源连接访问相关 [!DNL Snowflake] 数据库、模式和表。 不同的各种权限 [!DNL Snowflake] 实体之详情如下：

| [!DNL Snowflake] 实体 | 需要角色权限 |
| --- | --- |
| 仓库 | 操作、使用 |
| 数据库 | 使用情况 |
| 架构 | 使用情况 |
| 表格 | 选择 |

>[!NOTE]
>
>必须在仓库的高级设置配置中启用自动恢复和自动暂停。

有关角色和权限管理的详细信息，请参阅 [[!DNL Snowflake] API参考](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## 限制和常见问题解答 {#limitations-and-frequently-asked-questions}

* 的数据吞吐量 [!DNL Snowflake] 源是每秒2000条记录。
* 根据仓库的活动时间和仓库的大小，定价可能会有所不同。 对于 [!DNL Snowflake] 源集成，最小尺寸，x小仓库就足够了。 建议启用自动暂停，以便仓库在不使用时能够自行暂停。
* 此 [!DNL Snowflake] 源每10秒轮询数据库一次新数据。
* 配置选项：
   * 您可以启用 `backfill` 布尔标记 [!DNL Snowflake] 创建源连接时的源。
      * 如果回填设置为true ，则timestamp.initial的值将设置为0。 这意味着获取时间戳列大于0纪元时间的数据。
      * 如果回填设置为false，则timestamp.initial的值将设置为–1。 这意味着获取时间戳列大于当前时间（源开始摄取的时间）的数据。
   * 时间戳列的格式应如下所示： `TIMESTAMP_LTZ` 或 `TIMESTAMP_NTZ`. 如果时间戳列设置为 `TIMESTAMP_NTZ`，则存储这些值的相应时区应该通过 `timezoneValue` 参数。 如果未提供，该值将默认为UTC。
      * `TIMESTAMP_TZ` 不能用于时间戳列或映射。

## 后续步骤

以下教程提供了有关如何连接 [!DNL Snowflake] 要使用APIExperience Platform的流源：

* [从流式传输数据 [!DNL Snowflake] 要使用流服务APIExperience Platform的数据库](../../tutorials/api/create/databases/snowflake-streaming.md)
* [从流式传输数据 [!DNL Snowflake] 要在Experience Platform用户界面中使用源工作区进行Experience Platform的数据库](../../tutorials/ui/create/databases/snowflake-streaming.md)
