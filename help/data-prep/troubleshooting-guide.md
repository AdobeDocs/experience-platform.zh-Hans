---
keywords: Experience Platform；主页；热门主题；
title: 数据准备疑难解答指南
description: 本文档提供了有关Adobe Experience Platform数据准备的常见问题解答。
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# [!DNL Data Prep] 疑难解答指南

本文档提供了有关Adobe Experience Platform的常见问题解答 [!DNL Data Prep]以及常见错误的疑难解答指南。 有关一般平台API的问题和疑难解答信息，请参阅 [Adobe Experience Platform API疑难解答指南](../landing/troubleshooting.md).

## 常见问题解答

以下是关于以下内容的常见问题解答列表 [!DNL Data Prep] 以及他们的答案。

### 如何解决转换错误？

[!DNL Data Prep] 将所有转换错误本地化为发生错误的列。 因此，该列将无效，并将继续处理行的其余部分。 这些转换问题将记录为 **警告**. 建议您定期查看警告，并调整转换逻辑以解决转换问题。 这将提高引入Experience Platform的数据的质量。

如果列标记为 **必需** 由于转换问题而失效，则不会摄取该行。 启用部分数据摄取后，您可以设置此类拒绝的阈值，以免整个流失败。 如果取消的属性未影响任何架构级别验证，则将继续摄取该行。

即使没有任何转换错误，任何无效行也将被拒绝。 例如，数据摄取流可能具有到必填字段的直通映射（无转换逻辑），并且该属性没有传入值。 此行将被拒绝。

### 如何转义字段中的特殊字符？

您可以使用对字段中的特殊字符进行转义 `${...}`. 但是，包含字段和句点(`.`)不受此机制支持。 与层次结构交互时，如果子属性具有句点(`.`)，则必须使用反斜杠(`\`)以转义特殊字符。 例如， `address` 是包含属性的对象 `street.name`，然后可以将其称为 `address.street\.name` 而不是 `address.street.name`.

### 计算字段的最大长度是多少？

计算字段的最大长度为4096个字符。