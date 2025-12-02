---
title: _container
description: 在一个对象中查看整个标记容器。
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---

# `_container`

`_satellite._container`对象包含页面上加载的标记属性的完整配置和运行时上下文。 所有信息（如规则、数据元素、扩展和环境）都在此对象中可用。 其主要用途是协助调试实施，以便您能够准确地查看公开或发布的逻辑。

```ts
readonly _satellite._container: {
  buildInfo: BuildInfo;
  company: Company;
  dataElements: { [name: string]: DataElement };
  environment: Environment;
  extensions: { [name: string]: Extension };
  property: Property;
  rules: Rule[];
}
```

>[!IMPORTANT]
>
>此对象仅用于调试目的。 请勿将生产逻辑与此对象绑定、在实施中引用此对象或编辑此对象中的值。 Adobe可随时更改此对象中属性或名称的可用性。

## 可用字段

以下对象可供参考：

```json
{
  "buildInfo": {
    "minified": true,
    "buildDate": "YYYY-06-13T01:22:12Z"
  },
  "company": {
    "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
    "dynamicCdnEnabled": true,
    "cdnAllowList": [ "assets.adobedtm.com" ]
  },
  "dataElements": { ... },
  "environment": {
    "id": "EN6b2...d6ff2",
    "stage": "production"
  },
  "extensions": {
    "adobe-alloy": { ... },
    "core": { ... },
    "common-web-sdk-plugins": { ... }
  },
  "property": {
    "name": "Example tag property",
    "settings": {
      "domains": [ "example.com" ],
      "undefinedVarsReturnEmpty": false,
      "ruleComponentSequencingEnabled": true
    },
    "id": "PR845...6cf92"
  },
  "rules": [ { ... } ]
}
```

## `buildInfo`

`_satellite._container.buildInfo`对象包含[`_satellite.buildInfo`](buildinfo.md)的副本。

```ts
readonly _satellite._container.buildInfo: {
  minified: boolean;
  buildDate: string;
  turbineBuildDate: string;
  turbineVersion: string;
}
```

## `company`

`_satellite._container.company`对象包含[`_satellite.company`](company.md)的副本。

```ts
readonly _satellite._container.company: {
  orgId: string;
  dynamicCdnEnabled: boolean;
  cdnAllowList: string[];
}
```

## `dataElements`

`_satellite._container.dataElements`对象提供了标记属性中所有数据元素的引用。

```ts
readonly _satellite._container.dataElements: {
  [name: string]: {
    modulePath: string;
    settings: Settings; // Varies by data element type
  }
}
```

每个数据元素都包含以下属性：

| 名称 | 类型 | 描述 |
|---|---|---|
| **`modulePath`** | `string` | JavaScript文件的路径，可确定该数据元素类型的逻辑。 |
| **`settings`** | `Settings` | 数据元素的设置。 此对象中的属性取决于数据元素类型。 |

## `environment`

`_satellite._container.environment`对象包含[`_satellite.environment`](environment.md)的副本。

```ts
readonly _satellite._container.environment: {
  id: string;
  stage: string;
}
```

## `extensions`

`_satellite._container.extensions`对象列出了发布到标记属性的所有扩展。

```ts
readonly _satellite._container.extensions: {
  [name: string]: {
    displayName: string;
    hostedLibFilesUrl: string;
    modules: Modules; // Extension-specific module definitions
  }
}
```

每个扩展都包含以下属性：

| 名称 | 类型 | 描述 |
|---|---|---|
| **`displayName`** | `string` | 扩展的友好名称。 |
| **`hostedLibFilesUrl`** | `string` | CDN上扩展所在的位置。 |
| **`modules`** | `Modules` | 该扩展使用的所有事件、操作、条件和数据元素的JavaScript逻辑。 每个扩展中此对象的内容均不同。 |

## `property`

`_satellite._container.property`对象提供了有关标记属性本身的信息。

```ts
readonly _satellite._container.property: {
  id: string;
  name: string;
  settings: {
    domains: string[];
    ruleComponentSequencingEnabled: boolean;
    undefinedVarsReturnEmpty: boolean;
  };
}
```

| 名称 | 类型 | 描述 |
|---|---|---|
| **`id`** | `string` | 标记属性的唯一标识符。 |
| **`name`** | `string` | 标记属性的易记名称。 |
| **`settings`** | `PropertySettings` | 此属性的设置。 请参阅下表。 |

| 设置名称 | 类型 | 描述 |
|---|---|---|
| **`domains`** | `string[]` | 属性的已配置域，在[配置标记属性](/help/tags/ui/administration/companies-and-properties.md)时设置。 |
| **`ruleComponentSequencingEnabled`** | `boolean` | 确定配置标记属性时是否启用复选框&#x200B;**[!UICONTROL Run rule components in sequence]**。 |
| **`undefinedVarsReturnEmpty`** | `boolean` | 确定配置标记属性时是否启用复选框&#x200B;**[!UICONTROL Return an empty string for undefined data elements]**。 |

## `_container.rules`

`rules`对象数组提供了标记属性中所有规则的引用。

```ts
readonly _satellite._container.rules: {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}[]
```

每个规则都包含以下字段：

| 名称 | 类型 | 描述 |
|---|---|---|
| **`id`** | `string` | 规则的唯一标识符。 |
| **`name`** | `string` | 规则的友好名称。 |
| **`events`** | `Event[]` | 一个事件数组，您已将其配置为触发规则。 |
| **`conditions`** | `Condition[]` | 您已配置为触发规则的条件数组。 |
| **`actions`** | `Action[]` | 配置为在触发规则时执行的一系列操作。 |
