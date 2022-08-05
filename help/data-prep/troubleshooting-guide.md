---
keywords: Experience Platform；主页；热门主题；
title: 数据准备疑难解答指南
topic-legacy: troubleshooting
description: 本文档提供了有关Adobe Experience Platform数据准备的常见问题解答。
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: d0f5d1f55101ce15934289d4fcfd1f70c1b63fc7
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# [!DNL Data Prep] 疑难解答指南

本文档提供了有关Adobe Experience Platform的常见问题解答 [!DNL Data Prep]，以及常见错误的疑难解答指南。 有关Platform API的一般问题和故障诊断信息，请参阅 [Adobe Experience Platform API疑难解答指南](../landing/troubleshooting.md).

## 常见问题解答

以下是有关 [!DNL Data Prep] 和他们的答案。

### 如何解决转换错误？

[!DNL Data Prep] 将所有转换错误定位到发生这些错误的列。 因此，该列将无效，并且将继续处理该行的其余部分。 这些转换问题将记录为 **警告**. 建议您定期查看警告并调整转换逻辑以解决转换问题。 这将提高摄取到Experience Platform的数据质量。

如果列被标记为 **必需** 将因转换问题而失效，则不会摄取该行。 启用部分数据摄取后，您可以在整个流程失败之前设置此类拒绝的阈值。 如果无效属性未影响任何架构级别验证，则将继续摄取该行。

即使没有任何转换错误，任何无效的行也将被拒绝。 例如，数据摄取流可能具有到必填字段的传递映射（无转换逻辑），并且该属性没有传入值。 该行将被拒绝。

### 如何转义字段中的特殊字符？

您可以使用 `${...}`. 但是，包含带有句点(`.`)不受此机制支持。 在与层级进行交互时，如果子属性具有句点(`.`)，则必须使用反斜杠(`\`)以转义特殊字符。 例如， `address` 是包含属性的对象 `street.name`，这可称为 `address.street\.name` 而不是 `address.street.name`.

### 计算字段的最大长度是多少？

计算字段的最大长度为4096个字符。