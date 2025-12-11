---
title: 核心事件转发扩展概述
description: 了解Adobe Experience Platform中的核心事件转发扩展。
feature: Event Forwarding
exl-id: b5ee4ccf-6fa5-4472-be04-782930f07e20
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 93%

---

# 核心事件转发扩展概述

核心事件转发扩展为Adobe Experience Platform中的事件转发提供默认事件、条件和数据类型。

使用本参考可了解有关使用此扩展构建规则时可用的选项的信息。

## 核心扩展条件类型

此部分介绍核心扩展中可用的条件类型。这些条件类型可以与常规或例外逻辑类型一起使用。

### 自定义代码

指定必须作为事件条件存在的任何自定义代码。使用内置代码编辑器输入自定义代码。Adobe Experience Platform中的事件转发支持ES13。

1. 选择 **[!UICONTROL Open Editor]**。
1. 键入自定义代码。
1. 选择 **[!UICONTROL Save]**。

要访问自定义代码中数据元素的值，请使用 `getDataElementValue` 方法。例如，要检索名为 `productName` 的数据元素的值，请编写以下代码： 

```javascript
getDataElementValue('productName') 
```

#### ruleStash 对象

在自定义代码中，您还可以使用 `ruleStash` 对象。

```javascript
utils.logger.log(context.arc.ruleStash);
```

`ruleStash` 是一个对象，可从操作模块中收集所有结果。

每个扩展都有自己的命名空间。例如，如果您将扩展命名为 `send-beacon`，则来自 `send-beacon` 操作的所有结果都将存储在 `ruleStash['send-beacon']` 命名空间中。

```javascript
utils.logger.log(context.arc.ruleStash['adobe-cloud-connector']);
```

每个扩展的命名空间都是唯一的，并且开头的值为 `undefined`。

从每个操作中返回的结果将会覆盖命名空间。命名空间不会发生奇迹。例如，如果 `transform` 扩展中包含两个操作：`generate-fullname` 和 `generate-fulladdress`，则将这两个操作添加到同一条规则中。

如果 `generate-fullname` 操作的结果为 `Firstname Lastname`，则完成该操作后的规则存储将如下所示：

```js
{
  transform: 'Firstname Lastname`
}
```

如果 `generate-address` 操作的结果为 `3900 Adobe Way`，则完成该操作后的规则存储将如下所示：

```js
{
  transform: '3900 Adobe Way`
}
```

请注意，规则存储中不再存在 `Firstname Lastname`。这是由于 `generate-address` 操作用地址将其覆盖。

如果要将这两项操作的结果存储到 `ruleStash` 的 `transform` 命名空间中，您可以编写类似于以下示例的操作模块：

```javascript
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;
  if (!transformRuleStash) {
    transformRuleStash = {};
  }
  transformRuleStash.fullName = 'Firstname Lastname';
  return transformRuleStash;
}
```

首次执行此操作时，由于 `ruleStash` 作为 `undefined`，因此将其初始化为一个空对象。下次执行该操作时，该操作将会返回先前调用的 `ruleStash`。通过将对象用作 `ruleStash`，您可以添加新数据，而不会丢失先前由扩展中的其他操作设置的数据。

在这种情况下，需要注意总是返回完整的扩展规则存储。如果您只返回一个值（例如，5），则规则存储将如下所示：

```js
{
  transform: 5
}
```

### Value Comparison {#value-comparison}

比较两个值以确定此条件是否返回 true。

假设您有一个包含多个条件的规则，此条件可能会返回 true，但是由于其他条件评估为 false 或其中一个例外评估为 true，因此该规则仍不会触发。

1. 提供一个值。
1. 选择运算符。有关更多详细信息，请参阅下面的值比较运算符列表。
1. 提供另一个要比较的值。

可以使用以下值比较运算符：

**Equal：**&#x200B;如果使用非严格比较后认为两个值相等，则该条件会返回 true（在 JavaScript 中，运算符为 ==）。值可以是任何类型。在值字段中输入 _true_、_false_、_null_ 或 _undefined_ 之类的词时，该词将作为字符串进行比较，而不会转换为其 JavaScript 等效字符。

**Does Not Equal：**&#x200B;如果使用非严格比较后认为两个值不相等，则该条件会返回 true（在 JavaScript 中，运算符为 !=）。值可以是任何类型。在值字段中输入 _true_、_false_、_null_ 或 _undefined_ 之类的词时，该词将作为字符串进行比较，而不会转换为其 JavaScript 等效字符。

**Contains：**&#x200B;如果第一个值包含第二个值，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 false。

**Does Not Contain：**&#x200B;如果第一个值不包含第二个值，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 true。

**Starts With：**&#x200B;如果第一个值以第二个值开头，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 false。

**Does Not Start With：**&#x200B;如果第一个值不以第二个值开头，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 true。

**Ends With：**&#x200B;如果第一个值以第二个值结尾，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 false。

**Does Not End With：**&#x200B;如果第一个值不以第二个值结尾，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 true。

**Matches Regex：**&#x200B;如果第一个值匹配正则表达式，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 false。

**Does Not Match Regex：**&#x200B;如果第一个值不匹配正则表达式，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 true。

**Is Less Than：**&#x200B;如果第一个值小于第二个值，则该条件会返回 true。表示数字的字符串将转换为数字。除数字或可转换字符串之外的任何其他值都会导致该条件返回 false。

**Is Less Than Or Equal To：**&#x200B;如果第一个值小于或等于第二个值，则该条件会返回 true。表示数字的字符串将转换为数字。除数字或可转换字符串之外的任何其他值都会导致该条件返回 false。

**Is Greater Than：**&#x200B;如果第一个值大于第二个值，则该条件会返回 true。表示数字的字符串将转换为数字。除数字或可转换字符串之外的任何其他值都会导致该条件返回 false。

**Is Greater Than Or Equal To：**&#x200B;如果第一个值大于或等于第二个值，则该条件会返回 true。表示数字的字符串将转换为数字。除数字或可转换字符串之外的任何其他值都会导致该条件返回 false。

**Is True：**&#x200B;如果提供的值是值为 true 的布尔值，则该条件会返回 true。如果您提供的值是任何其他类型，则不会将该值转换为布尔值。除值为 true 的布尔值之外的任何其他值都会导致该条件返回 false。

**Is Truthy：**&#x200B;如果提供的值在转换为布尔值后为 true，则该条件会返回 true。有关 truthy 值的示例，请参阅 [MDN 的 Truthy 文档](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy)。

**Is False：**&#x200B;如果提供的值是值为 false 的布尔值，则该条件会返回 true。如果您提供的值是任何其他类型，则不会将该值转换为布尔值。除值为 false 的布尔值之外的任何其他值都会导致该条件返回 false。

**Is Falsy：**&#x200B;如果提供的值在转换为布尔值后为 false，则该条件会返回 true。有关 falsy 值的示例，请参阅 [MDN 的 Falsy 文档](https://developer.mozilla.org/zh-CN/docs/Glossary/Falsy)。



## 核心扩展操作类型

此部分介绍核心扩展中可用的操作类型。

### 自定义代码

提供在触发事件并评估条件后运行的代码。Adobe Experience Platform中的事件转发支持ES13。

1. 命名操作代码。
1. 选择 **[!UICONTROL Open Editor]**。
1. 编辑代码，然后选择 **[!UICONTROL Save]**。

要访问自定义代码中数据元素的值，请使用 `getDataElementValue` 方法。例如，要检索名为 `productName` 的数据元素的值，请编写以下代码： 

```javascript
getDataElementValue('productName') 
```

事件转发操作按顺序执行。 对于某项操作中的自定义代码而言，也有可能会返回一个可用于后续操作的值。返回的值可能来自该操作中的代码，也可能来自对外部源发起调用的响应正文。要在使用核心扩展的单个规则中，引用先前执行的操作中的数据，请创建一个 `Path` 类型的数据元素，并使用以下路径引用名为 `productCategory` 的变量的值（该变量在核心扩展内的自定义代码中定义）：

```javascript
arc.ruleStash.[Extension-Name].[key-as-defined-by-action] 

arc.ruleStash.core.productCategory  
```

## 核心扩展数据元素类型

数据元素类型由扩展决定。对于可创建的类型，没有任何限制。

以下部分介绍核心扩展中可用的数据元素类型。其他扩展则使用其他数据元素类型。

### 自定义代码

通过选择 **[!UICONTROL Open Editor]** 并将代码插入编辑器窗口，可以将自定义 JavaScript 输入到用户界面中。

编辑器窗口中需要一个返回语句，以指示应该将什么值用作数据元素值。如果不包括返回语句或返回了值`null`或`undefined`，则数据元素的默认值反映为`null`或`undefined`。

要访问自定义代码中数据元素的值，请使用 `getDataElementValue` 方法。例如，要检索名为 `productName` 的数据元素的值，请编写以下代码： 

```javascript
getDataElementValue('productName') 
```

**示例：**

```javascript
return getDataElementValue('section').concat(getDataElementValue('pName')); 
```

#### 路径

发送到 Adobe Experience Platform Edge Network 的事件上的键值对的路径，该路径可通过“路径”数据元素类型进行引用。

要引用事件的整个对象，请输入 `arc` 作为路径。`arc` 表示 Adobe Resource Context 的缩写，是发送到 Adobe Experience Platform Edge Network 的事件的顶级路径。

例如，假定从客户端到 Edge Network 实现了 `interact` 调用，则从浏览器控制台中会看到以下请求：

```javascript
"events": [ 
        { 
             "xdm": { 
                    "page": { 
                            "btnHover": false, 
                            "pageName": "We Travel Home Page", 
                            "siteSection": "Landing Page" 
                     }] 
```

要输入引用 `pageName` 的路径，请在路径字段中输入以下内容：

```javascript
arc.event.xdm.page.pageName 
```

>[!NOTE]
>
>来自客户端的`interact`调用具有`events`，但是对于事件转发，您需要`event`。 这是因为事件转发会单独检查每个事件，而不是像客户端上所示的一批检查多个事件。
