---
title: 同意策略规则构建参考
description: 了解如何使用XDM数据类型、支持的运算符和高级逻辑在Adobe Experience Platform UI中创建详细的同意策略规则。
source-git-commit: 678220b14cefd4dd31ef7a12355d796575a77a50
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# 同意策略规则构建参考

在高级规则逻辑上使用此引用，以在Adobe Experience Platform中的同意策略生成器的&#x200B;**[!UICONTROL Then]**&#x200B;子句中设置精确、合法有效的规则。

![同意策略生成器界面突出显示用户定义规则条件的[!UICONTROL Then]子句部分。](../images/policies/multiple-rules.png)

了解策略规则如何应用于您的同意数据的结构和类型，以准确强制实施客户同意首选项。

阅读本文档，了解如何通过在XDM架构中导航到容器字段并选择原始字段来根据同意筛选用户档案。 然后，使用相应的运算符来定义用户档案必须匹配的确切值。

## 先决条件

在使用本参考之前，请确保您的同意策略设置已完成，并且您了解Adobe Experience Platform数据架构和治理框架的基本概念。

确保您满足以下先决条件：

* **策略设置完成**：您已在Adobe Experience Platform UI中创建或开始创建同意策略。 有关详细步骤，请参阅[数据使用策略用户指南](user-guide.md#consent-policy)。

* **熟悉数据结构**：此参考需要具备以下核心概念的工作知识：
   * **XDM和联合架构**：了解Experience数据模型结构如何定义数据关系，以及联合架构如何表示统一客户配置文件。 有关详细信息，请参阅[XDM系统概述](../../xdm/home.md)。
   * **数据管理框架**：了解Adobe Experience Platform如何实施数据使用策略和治理规则。 有关详细信息，请参阅[数据管理概述](../home.md)。
   * **客户同意处理**：了解如何在客户体验工作流中收集、存储和应用同意数据。 请参阅[同意处理概述](../../landing/governance-privacy-security/consent/adobe/overview.md)。

## 核心概念：原始和容器字段

阅读此部分以了解同意策略规则如何在XDM架构中使用不同的字段类型。 了解容器和原始字段之间的区别有助于您在定义策略条件时选择正确的字段和运算符。

### 支持的字段类型和规则逻辑

同意策略支持多种字段类型，每种类型都具有用于构建规则条件的特定运算符。 字段类型分组为两个类别：**容器类型**&#x200B;和&#x200B;**基元类型**。

### 容器类型（架构导航）

容器类型用于组织同意数据，但无法直接在策略条件中使用。 它们用作导航路径，以访问包含实际值的原始字段。

| 容器类型 | 描述 |
|----------------|-------------|
| **对象** | 具有固定架构的容器，用于保存多个不同类型的字段。 |
| **数组** | 包含多个相同类型的值的容器。 |
| **地图** | 带有动态键的容器，可以保存对象或其他字段类型。 |

>[!IMPORTANT]
>
>不能直接在同意策略条件中选择容器字段。 您必须导航到容器中以选择用于构建规则的&#x200B;**原始字段**（如字符串、数字或布尔值）。 容器运算符仅用于架构导航，不适用于设置策略条件。

### 原始类型（规则条件）

原始字段包含实际的同意数据值（例如，`true`或`"weekly"`），并且是唯一可用于定义策略条件的字段类型。

下表描述了每个受支持的原始类型和可用的运算符。

| 原始类型 | 支持的运算符 | 描述 |
|----------------|---------------------|-------------|
| **字符串** | `is equal to`、`is not equal to`、`exists`、`does not exist` | 基于文本的同意属性。 |
| **数字** | `is equal to`、`is not equal to`、`is greater than`、`is less than`、`exists`、`does not exist` | 数字同意属性。 |
| **布尔值** | `is equal to`、`is not equal to` | True或False同意值。 |
| **日期** | `is equal to`、`is not equal to`、`exists`、`does not exist` | 基于日期的同意属性。 |


## 使用复杂的数据结构

阅读此部分以了解如何导航同意模式中的嵌套容器以访问原始字段。 它介绍了常见的架构模式，并说明了更深层的结构如何启用更精细的同意逻辑。

### 处理嵌套和复杂的架构结构

复杂的同意架构通常包括嵌套的容器结构，这些结构支持灵活且可伸缩的数据管理。 由于策略规则只能引用原始字段，因此您必须通过容器层次结构导航以访问可在同意策略条件中使用的字段。 更深入的嵌套可实现更细粒度和更具体的规则定位。

常见的嵌套容器模式包括：

* **映射的映射** — 包含其他映射的动态键。
* **对象**&#x200B;的映射 — 包含具有固定架构对象的动态键。
* **映射数组** — 包含带有动态键的映射的数组。
* **对象数组** — 包含具有固定架构对象的数组。
* **具有映射或数组属性的对象** — 包含映射或数组字段的对象。

### 字段结构示例

以下结构用作本指南中规则示例的可视参考。

```
consent.marketing (Object)
├── email (Boolean)
├── sms (Boolean)
├── preferences (Map with dynamic keys)
│   ├── "email_preferences" (Object)
│   │   ├── frequency (String)
│   │   └── channels (Array of Strings)
│   ├── "sms_preferences" (Object)
│   │   ├── frequency (String)
│   │   └── opt_in_time (Date)
│   └── "push_preferences" (Object)
│       ├── frequency (String)
│       └── categories (Array of Strings)
└── lastUpdated (Date)
```

## 按字段类型构建高级规则

请阅读此部分，了解有关基于字段类型创建同意策略规则的详细指导。 您将了解如何为布尔值、映射、对象和数组配置规则逻辑以捕获精确的同意条件。

### 规则构建组件和步骤

构建有效的同意策略规则需要了解如何导航架构并为每个字段类型应用正确的运算符。 每个规则都遵循相同的基本方法：导航到原始字段，选择适当的运算符，并定义必须满足的条件。

请按照以下步骤构建规则：

1. **选择字段** — 浏览容器字段以访问原始字段。
2. **选择运算符** — 选择字段类型支持的运算符。
   ![分层架构导航面板，显示一个用户正在扩展容器以访问基元字段。](../images/policies/consent-policy-map-field.png)
3. **设置值** — 定义要匹配的值或条件。
4. **匹配映射键** — 选择是定位特定键还是匹配映射中的所有键。
5. **添加条件** — 根据需要使用AND或OR逻辑组合多个规则。

### 使用布尔字段（隐式同意逻辑）

布尔字段存储true或false同意值，并代表最常见的同意属性。 `is not equal to`运算符允许您包含未明确选择退出的用户档案，支持隐式同意方案。

**布尔运算符和结果**

| 运算符 | 值 | 结果 |
|----------|-------|--------|
| `is equal to` | `true` | 包含明确同意的配置文件(`true`)。 |
| `is equal to` | `false` | 包含具有显式选择退出(`false`)的配置文件。 |
| `is not equal to` | `true` | 包含未经明确同意的配置文件（`false`或缺少配置文件）。 |
| `is not equal to` | `false` | 包括未显式选择退出的配置文件（`true`或缺少该配置文件）。 |

**示例：隐式电子邮件同意**

```
Field: consent.marketing.email (boolean)
Operator: is not equal to
Value: false
Result: Includes profiles who have not explicitly opted out of email marketing (includes both true and missing/null values).
```

### 使用映射字段（动态首选项）

映射字段使用动态键存储键值对，这与具有固定架构的对象不同。 映射通常用在首选项中心，无需模式更新即可添加新类别。 您可以定位特定键或使用通配符匹配所有键。

**特定键匹配**

使用此方法定位特定的首选项类别。

```
Field: consent.preferences["email_preferences"].frequency (string) - navigated to from the map container
Operator: is equal to
Value: "weekly"
Result: Includes profiles who set the email frequency to weekly (for the "email_preferences" key)
```

**任何键匹配**

使用“**[!UICONTROL find any matching item]**”复选框选项可匹配映射中的所有动态键。

![策略规则生成器显示“映射”字段的“查找任何匹配项”复选框，用于匹配所有动态键的值。](../images/policies/find-any-matching-item.png)

```
Field: consent.preferences.*.frequency (string)
Operator: is equal to
Value: "weekly"
Result: Includes profiles who set frequency to weekly in ANY preference category (for example, email_preferences, sms_preferences, or push_preferences)
```

### 使用对象字段（固定导航）

对象字段充当具有固定架构的容器。 它们仅用于导航，无法在策略条件中直接引用。

**导航示例**

```
consent.marketing (object) → consent.marketing.email (boolean)
```

**示例用例：**

```
Field: consent.marketing.email (Boolean) - navigated to from the object
Operator: is equal to
Value: true
Result: Include profiles who have explicitly consented to marketing emails
```


### 使用数组字段（多个值）

数组字段包含多个相同类型的值，并且需要根据它们存储的是基元还是对象进行不同的处理。 导航和运算符选项因阵列类型而异。

**基元数组示例**

使用`contains`运算符根据数组中的特定值标识配置文件。

```
Field: consent.communication_channels (array of strings)
Operator: contains
Value: "email"
Result: Include profiles who have consented to email communication
```

**对象数组示例**

导航到数组以访问嵌套对象中的原始字段。

```
Field: consent.preferences["email_preferences"].categories[].type - navigated to from the array
Operator: is equal to
Value: "promotional"
Result: Include profiles where any email category is "promotional"
```

## 将规则与复杂逻辑相结合

本节介绍如何使用AND或OR逻辑组合多个规则条件。 您将了解逻辑运算符如何协作以定义高级、多条件同意策略。

### 组合多个条件（AND或OR逻辑）

您可以使用AND或OR逻辑组合多个规则条件，以构建针对特定配置文件区段的更复杂的同意策略。\
**AND逻辑**&#x200B;要求所有条件都为true，从而生成更小的受众匹配。\
**OR逻辑**&#x200B;允许任何条件为true，从而扩大受众范围。

在同意策略界面中，使用在规则条件之间显示的逻辑选择器，在AND和OR逻辑之间切换。

### 一般复杂规则示例

以下示例将基本同意状态与偏好设置频率相结合，以创建目标区段。

```
Field: consent.marketing.email
Operator: is equal to true
AND
Field: consent.preferences.frequency
Operator: is not equal to "daily"
Result: Include profiles who consent to email marketing but not to a daily frequency
```

### 对象数组的高级逻辑

在对象数组中组合条件时，行为取决于在条件之间使用AND还是OR逻辑。

**示例：具有AND条件的对象数组**

当所有条件都必须应用于&#x200B;*same*&#x200B;数组元素时，请使用AND逻辑。

```
Field: consent.preferences["email_preferences"].categories[].enabled (boolean)
Operator: is equal to
Value: true
AND
Field: consent.preferences["email_preferences"].categories[].type (string)
Operator: is equal to
Value: "promotional"
Result: Includes profiles where the same category entry has both enabled=true and type="promotional".
Note: AND conditions apply to the same array entry. Using OR logic would include profiles if any array entry matches any of the conditions.
```

>[!TIP]
>
>适用于AND逻辑的&#x200B;**最佳实践**
>
>在构建基于AND的数组条件时，请牢记以下关键行为：
>
>* 当所有条件都必须应用于&#x200B;**同一数组元素**&#x200B;时，请使用AND逻辑。
>* 请记住，AND会创建限制性的定位（匹配的配置文件较少）。
>* 不要期望多个数组条目中的AND逻辑匹配；它适用于每个条目。
>* 当需要跨条目灵活匹配时，请避免使用AND逻辑。

>[!IMPORTANT]
>
>使用AND逻辑时，每个数组条目必须同时满足所有指定的条件。 当您需要匹配组合属性（例如已启用且促销的类别）时，这是最理想的选择。

>[!NOTE]
>
>AND逻辑仅适用于对象数组的相同数组项&#x200B;**。**\
>对于基元数组，将在整个数组的字段级别评估AND逻辑。

**示例：具有OR条件的对象数组**

使用OR逻辑，通过允许数组条目中的任何条件为true来创建包含受众匹配。

```
Field: consent.preferences["email_preferences"].categories[].enabled (boolean)
Operator: is equal to
Value: true
OR
Field: consent.preferences["email_preferences"].categories[].type (string)
Operator: is equal to
Value: "newsletter"
Result: Includes profiles where any category entry has enabled=true or any entry has type="newsletter".
Note: OR logic allows matching across different array entries. One entry can meet the first condition while another meets the second.
```

### 后续步骤

构建和优化同意策略规则后，请使用以下资源完成配置、验证策略实施并查看基础数据模型。

* **策略创建工作流**：使用[同意策略UI指南](user-guide.md#consent-policy.md)实施您在策略生成器UI中定义的规则
* **同意策略评估和实施**：验证启用的策略对受众激活和配置文件数据使用有何影响。 有关详细信息，请参阅[自动策略实施指南](../enforcement/auto-enforcement.md)
* **XDM同意数据类型**：引用策略规则中使用的同意属性的特定架构结构和字段定义。 请参阅[XDM同意和偏好设置数据类型](../../xdm/data-types/consents.md)指南。
