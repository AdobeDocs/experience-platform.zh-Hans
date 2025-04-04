---
keywords: Experience Platform；home；popular topics；
title: 数据准备疑难解答指南
description: 本文档提供了有关Adobe Experience Platform数据准备的常见问题解答。
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 0%

---

# [!DNL Data Prep]疑难解答指南

本文档提供了有关Adobe Experience Platform [!DNL Data Prep]的常见问题解答以及常见错误的疑难解答指南。 有关Experience Platform API的一般问题和疑难解答信息，请参阅[Adobe Experience Platform API疑难解答指南](../landing/troubleshooting.md)。

## 常见问题解答

以下是有关[!DNL Data Prep]的常见问题及其答案的列表。

### 如何解决转换错误？

[!DNL Data Prep]将所有转换错误本地化为发生这些错误的列。 因此，该列无效，行的其余部分将继续进行处理。 这些转换问题记录为&#x200B;**警告**。 建议您定期查看警告，并调整转换逻辑以解决转换问题。 这将提高Experience Platform中所摄取数据的质量。

如果标记为&#x200B;**必需**&#x200B;的列由于转换问题而无效，则不会摄取该行。 启用部分数据摄取后，您可以设置此类拒绝的阈值，以免整个流失败。 如果取消的属性未影响任何架构级别验证，则将继续摄取该行。

即使没有任何转换错误，任何无效行也将被拒绝。 例如，数据摄取流可能具有到必填字段的直通映射（无转换逻辑），并且该属性没有传入值。 此行将被拒绝。

### 如何转义字段中的特殊字符？

您可以使用`${...}`对字段中的特殊字符进行转义。 但是，此机制不支持包含具有句点(`.`)的字段的JSON文件。 与层次结构交互时，如果子属性具有句点(`.`)，则必须使用反斜杠(`\`)对特殊字符进行转义。 例如，`address`是包含属性`street.name`的对象，然后可以将其称为`address.street\.name`而不是`address.street.name`。

### 计算字段的最大长度是多少？

计算字段的最大长度为4096个字符。

### 由于对属性进行了验证，我的摄取失败，但我在文件中正确地具有该属性。 到底怎么了？

确保每个字段的数据类型与架构中定义的类型匹配。 此外，必须遵守“Required”、“enum”和“format”等约束。

所摄取的数据必须符合Experience Platform中定义的体验数据模型(XDM)架构。 如果属性与架构中指定的预期类型或格式不匹配，摄取将失败。

如果正在使用数据准备函数，请确保转换产生正确的属性。 您可以在源工作流的设置过程中查看属性。 在映射步骤中，选择&#x200B;**[!UICONTROL 新字段类型]**，然后选择&#x200B;**[!UICONTROL 添加计算字段]**。 接下来，使用计算字段界面预览每个函数。

### 如何从流或批量摄取记录中删除错误的数据值？

您可以使用数据准备映射接口通过仅映射具有所需数据的列来执行列级筛选。 您还可以使用计算字段通过支持函数转换数据。

行级筛选当前仅适用于[Adobe Analytics源连接器](../sources/tutorials/ui/create/adobe-applications/analytics.md#row-level-filtering)。

在摄取之后，可以使用Data Distiller使用SQL清理、塑造和处理数据。 但是，此过程将要求删除包含错误记录的批次，并重新引入根据SQL结果创建的新批次。

>[!IMPORTANT]
>
>* 数据湖：您只能通过删除和重新引入记录所在的批来移除已引入的记录。
>
>* 实时客户配置文件：您可以通过引入新记录来覆盖基于属性的记录，但无法删除体验事件记录。
>
>* Identity Service：不能完全删除Identity Service中的记录。 您将必须删除整个配置文件，然后使用配置文件删除API重新上传包含正确记录的配置文件。

### 在GIF数据中使用计算字段的最佳实践是什么？

您可以在源数据到XDM架构的映射步骤中使用数据准备映射函数来创建新的计算字段。

### 在将Adobe Analytics数据作为源引入时，是否为配置文件自动启用创建的架构？

不会为配置文件自动配置Analytics数据。 配置源连接器后，您必须进入数据集和架构并为配置文件摄取启用它们。

在生产沙盒中创建Analytics源数据流时，将创建两个数据流：

* 一个数据流，将历史报表包数据回填到13个月的数据湖。 此数据流在回填完成后结束。
* 将实时数据发送到数据湖和配置文件的数据流。 此数据流持续运行。

### 如何使用数据准备函数将映射对象中的一个值变为小写？

您可以使用`map_get_values`函数检索该值，然后使用较低级别的函数将其变为小写：

```shell
lower(map_get_values(mapObject, 'keyName'))
```

您可以使用相同的函数将映射对象转换为小写。 但是，不能循环遍历整个映射并将每个项目变为小写。

### 我能否以嵌套方式使用数据准备函数？

可以，您可以在另一个函数中使用一个数据准备功能，以解决在数据摄取期间复杂的数据准备功能。

例如，如果要根据特定条件将字段定义为null ，则可以使用“iif”函数检查该字段。 如果函数返回`true`，则您可以使用“nullify()”；如果函数返回`false`，则可以使用相应的字段。

如果“marketing_type”为字段，则可以使用“.equals”检查“marketing_type”字段中的值，该值可以嵌套在“iif”函数中。 如果返回`true`，则可以使用“nullify()”函数，如下所示：

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

下面概述了使用iif、equals和nullify嵌套数据准备函数的示例：

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
| --- | --- | --- | --- | --- | --- |
| iif | 计算给定的布尔表达式并根据结果返回指定的值。 | <ul><li>表达式： **必需**&#x200B;正在计算的布尔表达式。</li><li>TRUE_VALUE： **必需**&#x200B;如果表达式的计算结果为true，则返回的值。</li><li>FALSE_VALUE： **必需**&#x200B;表达式计算结果为false时返回的值。</li></ul> | iif（表达式， TRUE_VALUE， FALSE_VALUE） | iif(&quot;s&quot;。equalsIgnoreCase(&quot;S&quot;)， &quot;True&quot;， &quot;False&quot;) | &quot;True&quot; |
| 等于 | 比较两个字符串以确认它们是否相等。 此函数区分大小写。 | <ul><li>STRING1： **必需**&#x200B;要比较的第一个字符串。</li><li>STRING2： **必需**&#x200B;要比较的第二个字符串。 | STRING1. &#x200B;equals(&#x200B;STRING2) | “string1”。&#x200B;equals&#x200B;(&quot;STRING1&quot;) | 错的 |
| 无效 | 将属性的值设置为null。 当您不想将字段复制到目标架构时，应使用此字段。 | | nullify() | nullify() | null |

{style="table-layout:auto"}

以下是如何嵌套函数的示例，假定正在评估的字段为“marketing_type”。

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

接下来，假定您具有以下三个字段：

* marketing_type： （电子邮件、phyMail、推送、短信、电话）
* total_consents：数字范围从4000到5500
* 日期：2024年2月至3月

您可以使用和嵌套上面列出的三个函数来操作三个字段：

* iif(marketing_type.equals(&quot;email&quot;)， nullify()， iif(marketing_type.equals(&quot;push&quot;)， &quot;push-notification&quot;， marketing_type))
* iif(marketing_type.equals(&quot;phyMail&quot;)， nullify()， iif(marketing_type.equals(&quot;sms&quot;)， &quot;text-message&quot;， marketing_type))
* iif(total_consents > 5000， iif(marketing_type.equals(&quot;phone&quot;)， nullify()， marketing_type)， &quot;insuffected-consents&quot;)
* iif(date.equals(&quot;3/21/24&quot;)， iif(marketing_type.equals(&quot;push&quot;)， nullify()， marketing_type)， &quot;not-March&quot;)
* iif(total_consents &lt; 4500， iif(marketing_type.equals(&quot;sms&quot;)， &quot;low-consent-sms&quot;， marketing_type)， &quot;high-consents&quot;)
* iif(marketing_type.equals(&quot;email&quot;)， iif(total_consents > 5000， nullify()， &quot;email-low-consents&quot;)， marketing_type)
* iif(marketing_type.equals(&quot;push&quot;)， iif(total_consents &lt; 4500， &quot;low-consent-push&quot;， nullify())， marketing_type)
* iif(total_consents >= 5500， iif(marketing_type.equals(&quot;phyMail&quot;)， nullify()， &quot;high-consents&quot;)， marketing_type)