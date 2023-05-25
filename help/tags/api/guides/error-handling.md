---
title: 错误处理
description: 了解如何在Reactor API中处理错误。
exl-id: 336c0ced-1067-4519-94e1-85aea700fce6
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# 错误处理

调用Reactor API时出现问题时，可能会通过以下方式之一返回错误：

* **立即错误**：执行导致立即错误的请求时，API会返回错误响应，其中HTTP状态反映所发生的错误的一般类型。
* **延迟的错误**：执行导致延迟错误（例如异步活动）的API请求时，中的API可能会返回错误 `meta.status_details` 相关资源的ID。

## 错误格式

错误响应旨在符合 [JSON：API错误规范](http://jsonapi.org/format/#errors)，通常遵循以下结构：

```json
{
  "errors": [
    {
      "id": "8a5526da-ab12-4be9-b084-2efe537f388c",
      "status": "404",
      "code": "not-found",
      "title": "Record Not Found",
      "meta": {
        "request_id": "jfb0dQ2e0XVTkQ6AOfEJFfTDjguw9x3d"
      },
      "source": {
        "pointer": "/data"
      }
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 此特定问题发生的唯一标识符。 |
| `status` | 适用于此问题的HTTP状态代码，以字符串值表示。 |
| `code` | 应用程序特定的错误代码，以字符串值表示。 |
| `title` | 简短、易于用户阅读的问题摘要 **不应更改** 从发生到发生，但用于本地化的目的除外。 |
| `detail` | 特定于此问题发生的可读说明。 点赞 `title`中，此字段值可以本地化。 |
| `source` | 一个对象，其中包含对错误源的引用，可以选择包括以下任意成员：<ul><li>`pointer`： a [JSON指针(RFC6901)](https://datatracker.ietf.org/doc/html/rfc6901) 引用请求文档中的关联实体的字符串(例如 `/data` 主数据对象，或 `/data/attributes/title` （对于特定属性）。</li></ul> |
| `meta` | 包含有关错误的非标准元数据的对象。 |

{style="table-layout:auto"}

## 错误引用

下表列出了API可以返回的不同错误。

| 错误标题 | 描述 |
| --- | --- |
| `authentication-failure` | 您的IMS访问令牌无效。 您可以通过再次登录来获取新的访问令牌。 或者，对于技术帐户，生成新的JWT并替换IMS访问令牌。 |
| `connection-refused` | 无法建立与服务器的连接。 |
| `decrypt-bad-passphrase` | 无法使用提供的密码解密数据。 |
| `decrypt-failed` | 无法使用提供的私钥解密数据。 确保密钥在本地有效，并且空格已修剪。 |
| `decrypt-no-data` | 如果没有私钥，数据将无法解密。 请提供加密的私钥。 |
| `delegate-descriptor-unresolved` | 扩展未提供此委托描述符的预期定义。 可能需要更新扩展。 |
| `deleted-resources` | 您尝试添加到库的资源已被删除。 |
| `environment-in-use` | 一个环境一次只能分配给一个库。 选项1是选择其他环境。 选项2是通过将库移动到其他环境或删除库来释放此环境。 |
| `environment-required` | 在创建内部版本之前，必须为库分配一个环境。 |
| `extension-not-found` | 定义数据元素或规则组件的扩展未包含在库中。 确保已将所有必需的扩展添加到库中。 |
| `extension-package-path-error` | extension.json中定义的路径构造不正确。 |
| `extension-package-transform-definition-error` | 您为对象属性定义了无效的转换。 每个对象属性都可以定义一个转换，并且它必须是文件转换或函数转换。 |
| `extension-package-zip-error` | 解压缩ExtensionPackage或压缩文件进行分发时出错。 |
| `host-in-use` | 如果一个或多个环境正在使用某个主机，则无法删除该主机。 |
| `host-required` | 分配给此库的环境没有有效的主机。 检查为库分配的环境。 然后，为该环境分配一个有效主机。 |
| `host-type-error` | 只有SFTP主机需要先验证凭据才能使用，因此预测试仅适用于该主机类型。 |
| `illegal-custom-code-transform` | 不允许使用customCode转换。 请指定函数或文件转换。 |
| `ims-not-authorized` | 授权您的帐户时发生未知错误。 请稍后重试。 |
| `ims-session-error` | 登录会话出现问题。 请注销并重新登录。 |
| `internal-error` | 发生内部错误。 请等待几分钟，然后重试。 如果问题仍然存在，请联系客户关怀团队。 |
| `invalid-data_element` | 无法将无效的数据元素添加到库中。 |
| `invalid-embed_code` | 这不是有效的嵌入代码，或者您尝试将其链接到开发或暂存环境。 动态Tag Management (DTM)嵌入代码只能链接到生产环境。 |
| `invalid-extension` | 无法将无效的扩展添加到库中。 |
| `invalid-extension_package_id` | 您只能修改扩展包的某些对象属性。 您试图修改其中一个不允许的项。 |
| `invalid-new-owner-org-id` | 您尝试分配的组织ID不是有效的组织ID。 |
| `invalid-org` | 您的活动组织无权访问API。 检查您使用的组织是否正确。 |
| `invalid-rule` | 无法将无效的规则添加到库。 |
| `invalid-settings-syntax` | 分析设置JSON时遇到语法错误。 |
| `library-file-not-found` | 在zip包中找不到extension.json中定义的所需文件。 |
| `minification-error` | 由于代码无效，无法编译代码。 |
| `multiple-revisions` | 库中只能包含每个资源的一个修订版。 |
| `no-available-orgs` | 此用户帐户不属于有权访问标记的产品配置文件。 使用Admin Console可将此用户添加到具有标记权限的产品配置文件中。 |
| `not-authorized` | 此用户帐户没有执行此操作所需的权限。 |
| `not-found` | 找不到记录。 验证您尝试检索的对象的ID。 |
| `not-unique` | 您尝试使用的名称已被使用。 对于此资源，“name”属性必须是唯一的。 |
| `public-release-not-authorized` | 扩展的公开发行由以下协调方进行 `launch-ext-dev@adobe.com`. 查看文档 [释放扩展](../../extension-dev/submit/release.md) 了解更多信息。 |
| `read-only` | 此资源为只读资源，无法修改。 |
| `session-timeout` | 用户会话已过期。 请注销并重新登录。 |
| `sftp-authentication-failed` | SFTP连接的身份验证失败。 |
| `sftp-connection-timeout` | SFTP连接已超时。 |
| `sftp-exception` | 使用SFTP连接到服务器时遇到异常。 |
| `sftp-status-exception` | 尝试与服务器通信时遇到SFTP异常。 |
| `socket-error` | 尝试与服务器通信时遇到套接字错误。 |
| `ssh-disconnect` | SSH会话已断开连接。 |
| `timeout-error` | 与服务器的连接超时。 |
| `unknown-error` | 发生意外错误。 您可以稍后重试或致电客户关怀部门，并解释发生问题时您正在做什么。 |
| `unsupported-custom-code-language` | 提供的自定义代码语言不受支持。 |
| `upgraded-extension-required` | 安装扩展升级后，必须将其包含在所有库中，直到升级进入生产环境。 唯一的例外是尚未发布扩展。 |
| `upstream-build-required` | 必须先为上游库成功构建，然后才能构建此库。 |

{style="table-layout:auto"}
