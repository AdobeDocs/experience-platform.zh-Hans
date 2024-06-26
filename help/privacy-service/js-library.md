---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Adobe隐私JavaScript库概述
description: Adobe隐私JavaScript库允许您检索数据主体身份以用于Privacy Service。
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 6%

---

# Adobe隐私JavaScript库概述

作为数据处理者，Adobe会根据贵公司的权限和说明处理个人数据。 作为“数据控制者”，您可以决定 Adobe 代表您处理和存储的个人数据。根据您选择通过Adobe Experience Cloud解决方案发送的信息，Adobe可以存储适用于隐私法规的隐私信息，例如 [!DNL General Data Protection Regulation] (GDPR)和 [!DNL California Consumer Privacy Act] (CCPA)。 查看文档 [Adobe Experience Cloud中的隐私](https://www.adobe.com/cn/privacy/marketing-cloud.html) ，以了解有关Experience Cloud解决方案如何收集专用数据的更多信息。

此 **Adobe隐私JavaScript库** 允许数据控制者自动检索由生成的所有数据主体身份 [!DNL Experience Cloud] 特定领域的解决方案。 使用提供的API [Adobe Experience Platform Privacy Service](home.md)之后，这些身份可用于为属于这些数据主体的私有数据创建访问和删除请求。

>[!NOTE]
>
>此 [!DNL Privacy JS Library] 通常只需在与隐私相关的页面上安装，无需在网站或域的所有页面上安装。

## 函数

此 [!DNL Privacy JS Library] 提供了多个用于管理中标识的功能 [!DNL Privacy Service]. 这些函数只能用于管理存储在浏览器中以供特定访客使用的标识。 不能使用它们将信息提交到 [!DNL Experience Cloud Central Service] 直接。

下表概述了库提供的各种功能：

| 函数 | 描述 |
| --- | --- |
| `retrieveIdentities` | 返回匹配身份的数组(`validIds`)中检索到的对象 [!DNL Privacy Service]以及未找到的一组标识(`failedIds`)。 |
| `removeIdentities` | 从浏览器中删除每个匹配（有效）的标识。 返回匹配身份的数组(`validIds`)，每个标识都包含 `isDeletedClientSide` 布尔值，指示此ID是否已删除。 |
| `retrieveThenRemoveIdentities` | 检索匹配身份的数组(`validIds`)，然后从浏览器中删除这些标识。 虽然此函数类似于 `removeIdentities`，当您使用的Adobe解决方案要求先访问请求然后才能删除时（例如，在删除请求中提供标识符之前必须检索唯一标识符时），最好使用此标识符。 |

>[!NOTE]
>
>`removeIdentities` 和 `retrieveThenRemoveIdentities` 仅从浏览器中删除支持身份的特定Adobe解决方案的身份。 例如，Adobe Audience Manager不会删除存储在第三方Cookie中的Demdex ID，而Adobe Target会删除存储其ID的所有Cookie。

由于所有三个函数都表示异步进程，因此必须使用回调或承诺来处理任何检索到的身份。


## 安装

要开始使用 [!DNL Privacy JS Library]，您必须使用以下方法之一将其安装到计算机上：

* 通过运行以下命令使用npm安装： `npm install @adobe/adobe-privacy`
* 从下载 [Experience CloudGitHub存储库](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

您还可以通过标记扩展来安装库。 请参见 [Adobe隐私标记扩展](../tags/extensions/client/privacy/overview.md) 了解更多信息。

## 实例化 [!DNL Privacy JS Library]

所有利用 [!DNL Privacy JS Library] 必须实例化新的 `AdobePrivacy` 对象，必须将其配置为特定的Adobe解决方案。 例如，Adobe Analytics的实例化将类似于以下内容：

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{ORG_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

有关各种Adobe解决方案支持的参数的完整列表，请参阅附录中受支持的部分 [Adobe解决方案配置参数](#adobe-solution-configuration-parameters).

## 代码示例 {#samples}

以下代码示例演示了如何使用 [!DNL Privacy JS Library] 对于多种常见场景，前提是您未使用标记。

### Retrieve identities

此示例演示如何从检索标识列表 [!DNL Experience Cloud].

#### JavaScript

以下代码定义了一个函数， `handleRetrievedIDs`，用作回调或promise以处理检索到的身份 `retrieveIdentities`.

```javascript
function handleRetrievedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.retrieveIdentities(handleRetrievedIDs);

// If using promises:
adobePrivacy.retrieveIdentities().then(handleRetrievedIDs);
```

| Variable | 描述 |
| --- | --- |
| `validIds` | 包含已成功检索的所有ID的JSON对象。 |
| `failedIDs` | 包含所有未从中检索的ID的JSON对象 [!DNL Privacy Service]，或者无法找到其他内容。 |

#### 结果

如果代码执行成功， `validIDs` 使用检索到的身份列表填充。

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543"
},
{
    "company": "adobe",
    "namespace": "gsurfer_id",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao"
}
```

### Remove identities

此示例演示了如何从浏览器中删除身份列表。

#### JavaScript

以下代码定义了一个函数， `handleRemovedIDs`，用作回调或promise以处理检索到的身份 `removeIdentities` 从浏览器中删除它们之后。

```javascript
function handleRemovedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.removeIdentities(handleRemovedIDs);

// If using promises:
adobePrivacy.removeIdentities().then(handleRemovedIDs)…
```

| Variable | 描述 |
| --- | --- |
| `validIds` | 包含已成功检索的所有ID的JSON对象。 |
| `failedIDs` | 包含所有未从中检索的ID的JSON对象 [!DNL Privacy Service]，或者无法找到其他内容。 |

#### 结果

如果代码执行成功， `validIDs` 使用检索到的身份列表填充。

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543",
    "isDeletedClientSide": false
},
{
    "company": "adobe",
    "namespace": "AMO",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao",
    "isDeletedClientSide": true
}
```

## 后续步骤

通过阅读本文档，您已经了解了 [!DNL Privacy JS Library]. 使用库检索身份列表后，您可以使用这些身份创建对的数据访问和删除请求 [!DNL Privacy Service] API。 请参阅 [Privacy ServiceAPI指南](api/overview.md) 了解更多信息。

## 附录

本节包含有关使用的补充信息 [!DNL Privacy JS Library].

### Adobe解决方案配置参数 {#config-params}

以下是受支持Adobe解决方案所接受的配置参数列表，这些参数用于 [实例化AdobePrivacy对象](#instantiate-the-privacy-js-library).

**所有解决方案**

| 参数 | 描述 |
| --- | --- |
| `key` | 标识用户或数据主体的唯一ID。 此属性仅用于您自己的内部跟踪，不供Adobe使用。 |

**Adobe Analytics**

| 参数 | 描述 |
| --- | --- |
| `cookieDomainPeriods` | 域中用于Cookie跟踪的句点数(默认为 `2`，例如 `.domain.com`)。 除非在JavaScript Web信标中指定，否则不要在此处定义它。 |
| `dataCenter` | Adobe数据收集数据中心。 仅当在JavaScript Web信标中指定它时，才应包含它。 潜在值包括： <ul><li>`d1`：圣何塞数据中心</li><li>`d2`：达拉斯数据中心</li></ul> |
| `reportSuite` | JavaScript Web信标中指定的报表包ID(例如， `s_code.js` 或 `dtm`)。 |
| `trackingServer` | 非SSL数据收集域。 仅当在JavaScript Web信标中指定它时，才应包含它。 |
| `trackingServerSecure` | SSL数据收集域。 仅当在JavaScript Web信标中指定它时，才应包含它。 |
| `visitorNamespace` | 用于对访客进行分组的命名空间。 仅当在JavaScript Web信标中指定它时，才应包含它。 |

**Adobe Audience Manager**

| 参数 | 描述 |
| --- | --- |
| `aamUUIDCookieName` | 包含从Adobe Audience Manager返回的唯一用户ID的第一方Cookie的名称。 |

**Adobe Experience Cloud Identity服务(ECID)**

| 参数 | 描述 |
| --- | --- |
| `imsOrgID` | 您的组织 ID。 |

**Adobe Target**

| 参数 | 描述 |
| --- | --- |
| `clientCode` | 标识Adobe Target System中客户端的客户端代码。 |
