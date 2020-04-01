---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 验证和访问Experience Platform API
topic: tutorial
translation-type: tm+mt
source-git-commit: fca15ebf87559b08dd09e63b5df5655b57ef5977

---


# 验证和访问Experience Platform API

本文档提供了一个分步教程，用于获取对Adobe Experience Platform开发人员帐户的访问权限，以便调用Experience Platform API。

## 通过身份验证进行API调用

为了维护应用程序和用户的安全性，对Adobe I/O API的所有请求都必须使用OAuth和JSON Web令牌(JWT)等标准进行身份验证和授权。 然后，JWT与客户特定信息一起使用，以生成您的个人访问令牌。

本教程介绍了通过创建以下流程图中概述的访问令牌进行身份验证的步骤：
![](images/authentication/authentication-flowchart.png)

## 先决条件

为了成功调用Experience Platform API，您需要：

* 可访问Adobe Experience Platform的IMS组织
* 注册的Adobe ID帐户
* Admin Console管理员，可将您添加为 **开发人** 员 **和产品用户** 。

以下各节将介绍创建Adobe ID并成为组织的开发人员和用户的步骤。

### 创建Adobe ID

如果您没有Adobe ID，则可以使用以下步骤创建一个：

1. 转到 [Adobe I/O控制台](https://console.adobe.io)
2. 单击 **创建新帐户**
3. 完成注册过程


### 成为组织的Experience Platform开发人员和用户

在Adobe I/O上创建集成之前，您的帐户必须对IMS组织中的某个产品具有开发人员权限。 有关Admin Console上的开发人员帐户的详细信息，请参阅管理开发 [人员的支持文档](https://helpx.adobe.com/enterprise/using/manage-developers.html) 。

**获得开发人员访问权限**

联系您组织中的Admin Console管理员，以使用 [Admin Console将您添加为您组织的某个产品的开发人员](https://adminconsole.adobe.com/)。

![](images/authentication/assign-developer.png)

管理员必须将您指定为开发人员，以至少分配一个产品用户档案才能继续。

![](images/authentication/add-developer.png)

一旦您被分配为开发人员，您将拥有在 [Adobe I/O上创建集成的访问权限](https://console.adobe.io/)。 这些集成是从外部应用程序和服务到Adobe API的管道。

**获取用户访问权限**

您的Admin Console管理员还必须以用户身份将您添加到产品中。

![](images/authentication/assign-users.png)

与添加开发人员的过程类似，管理员必须将您分配给至少一个产品用户档案才能继续。

![](images/authentication/assign-user-details.png)


## 一次性设置

以下步骤只需执行一次：

* 登录到Adobe I/O控制台
* 创建集成
* 向下复制访问值

一旦您拥有了集成和访问值，您将能够在将来重复使用这些值进行身份验证。 下面详细介绍了每个步骤。

### 登录到Adobe I/O控制台

转到 [Adobe I/O控制台](https://console.adobe.io/) ，使用您的Adobe ID登录。

登录后，单击屏幕顶 **部的** “集成”选项卡。 集成是为所选IMS组织创建的服务帐户。 您只能调用创建集成的IMS组织。

>[!NOTE]
>如果您的帐户与多个组织关联，则屏幕右上角的下拉菜单允许您在它们之间轻松切换。

### 创建集成

在“集 **成** ”页面中，单 **击“新建集成** ”以开始该过程。 该过程包含三个步骤：
* 选择集成类型
* 选择要与哪些Adobe服务集成
* 添加集成详细信息、公钥和产品用户档案

![](images/authentication/integrations.png)

#### 选择集成类型

下一个屏幕询问您是要访问API还是接收近实时事件。 选择 **访问API** ，然后 **继续**。

![](images/authentication/create-new-integration.png)

#### 选择要与哪些Adobe服务集成

如果您的帐户与多个IMS组织关联，则可以使用右上方的下拉菜单在它们之间切换。 在 **** Adobe Experience Platform **下选择** Workshop **和Experience Platform API** ，以访问这些API。

![](images/authentication/integration-select-service.png)

单击 **继续** ，移至下一节。

#### 添加集成详细信息、公钥和产品用户档案

下一个屏幕会提示您填写集成详细信息，输入公钥证书，然后选择产品用户档案。

![](images/authentication/integration-details.png)

首先，输入您的集成详细信息。 接下来，选择产品用户档案。 产品用户档案授予您对属于您在前面的步骤中选择的服务的一组功能的精细访问权限。

对于证书部分，必须生成证书：

**对于MacOS和Linux平台：**

打开命令行并执行以下命令：

`openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`


**对于Windows平台：**

1. 下载openssl客户端以生成公共证书(例如， [Openssl windows客户端](https://bintray.com/vszakats/generic/download_file?file_path=openssl-1.1.1-win64-mingw.zip))

1. 解压该文件夹并将其复制到C:/libs/位置。

1. 打开命令行提示并执行以下命令：

   `set OPENSSL_CONF=C:/libs/openssl-1.1.1-win64-mingw/openssl.cnf`

   `cd C:/libs/openssl-1.1.1-win64-mingw/`

   `openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`

您将收到类似于以下内容的响应，提示您输入一些有关自己的信息：

```
Generating a 2048 bit RSA private key
.................+++
.......................................+++
writing new private key to 'private.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) []:
State or Province Name (full name) []:
Locality Name (eg, city) []:
Organization Name (eg, company) []:
Organizational Unit Name (eg, section) []:
Common Name (eg, fully qualified host name) []:
Email Address []:
```

输入信息后，将生成两个文件： `certificate_pub.crt` 和 `private.key`。

>[!NOTE]
>`certificate_pub.crt` 将于365天后过期。 您可以通过更改上述命令中的值来延长 `days` 时间，但定 `openssl` 期旋转凭据是一个不错的安全实践。

将 `private.key` 在后一节中用于生成JWT。

用 `certificate_pub.crt` 于创建API密钥。 返回Adobe I/O控制台，单击“选 **择文件** ”以上传 `certificate_pub.crt` 文件。

单击 **创建集成** ，以完成该过程。

### 向下复制访问值

创建集成后，您可以视图其详细信息。 单击 **“检索客户端机密** ”，您的屏幕将类似于：

![](images/authentication/access-values.png)

向下复制 `{API KEY}`组 `{IMS ORG}` 织ID的值，如 `{CLIENT SECRET}` 果这些值将在下一步中使用。

## 每个会话的身份验证

最后一步是生成您的 `{ACCESS_TOKEN}` API调用，该调用将用于验证您的API调用。 该访问令牌必须包含在您对Adobe Experience Platform进行的每个API调用的“授权”头中。 访问令牌在24小时后过期，之后必须生成新令牌才能继续使用API。

### 创建JWT

在Adobe I/O控制台中的集成详细信息页面中，导航到 **JWT** 选项卡：

![](images/authentication/generate-jwt.png)

该页面会提示您输入在上 `private.key` 一部分中创建的内容。 打开命令行以视图文件的内 `private.key` 容：

```shell
cat private.key
```

您的输出将类似于：

```shell
-----BEGIN PRIVATE KEY-----
MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCYjPj18NrVlmrc
H+YUTuwWrlHTiPfkBGM0P1HbIOdwrlSTCmPhmaNNG5+mEiULJLWlrhQpx/7uQVNW
......
xbWgBWatJ2hUhU5/K2iFlNJBVXyNy7rN0XzOagLRJ1uS2CM6Hn3vBOqLbHRG4Pen
J1LvEocGunT12UJekLdEaQR4AKodIyjv5opvewrzxUZhVvUIIgeU5vUpg9smCXai
wPW5MQjmygodzCh7+eGLrg==
-----END PRIVATE KEY-----
```

复制整个输出并将其粘贴到文本字段中，然后单击“ **生成JWT”**。 复制生成的JWT以执行下一步。

![](images/authentication/generated-jwt.png)

### 生成访问令牌

您可以通过cURL命令生成访问令牌。 如果未安装cURL，则可以使用安装 `npm install curl`。 您可以在此处阅读有关cURL的更多 [信息](https://curl.haxx.se/)

安装cURL后，您需要将以下命令中的字段与您自己的、和 `{API_KEY}`交换 `{CLIENT_SECRET}`到一起 `{JWT_TOKEN}`:

```SHELL
curl -X POST "https://ims-na1.adobelogin.com/ims/exchange/jwt/" \
  -F "client_id={API_KEY}" \
  -F "client_secret={CLIENT_SECRET}" \
  -F "jwt_token={JWT_TOKEN}"
```

如果输出成功，则输出将类似于：

```JSON
{
  "token_type":"bearer",
  "access_token":"eyJ4NXUiOiJpbXNfbmExLXN0ZzEta2V5LT2VyIiwiYWxnIjoiUlMyNTYifQ.eyJpZCI6IjE1MjAzMDU0ODY5MDhfYzMwM2JkODMtMWE1My00YmRiLThhNjctMWDhhNDJiNTE1X3VlMSIsImNsaWVudF9pZCI6ImYwNjY2Y2M4ZGVhNzQ1MWNiYzQ2ZmI2MTVkMzY1YzU0IiwidXNlcl9pZCI6IjA0ODUzMkMwNUE5ODg2QUQwQTQ5NDEzOUB0ZWNoYWNjdC5hZG9iZS5jb20iLCJzdGF0ZSI6IntcInNlc3Npb25cIjpcImh0dHBzOi8vaW1zLW5hMS1zdGcxLmFkb2JlbG9naW4uY29tL2ltcy9zZXNzaW9uL3YxL05UZzJZemM1TVdFdFlXWTNaUzAwT1RWaUxUZ3lPVFl0WkdWbU5EUTVOelprT0dFeUxTMHdORGcxTXpKRPVGc0TmtGRU1FRTBPVFF4TXpsQWRHVmphR0ZqWTNRdVlXUnZZbVV1WTI5dFwifSIsInR5cGUiOiJhY2Nlc3NfdG9rZW4iLCJhcyI6Imltcy1uYTEtc3RnMSIsImZnIjoiU0hRUlJUQ0ZTWFJJTjdSQjVVQ09NQ0lBWVU9PT09PT0iLCJtb2kiOiJhNTYwOWQ5ZiIsImMiOiJMeksySTBuZ2F2M1BhWWIxV0J3d3FRPT0iLCJleHBpcmVzX2luIjoiODY0MDAwMDAiLCJzY29wZSI6Im9wZW5pZCxzZXNzaW9uLEFkb2JlSUQscmVhZF9vcmdhbml6YXRpb25zLGFkZGl0aW9uYWxfaW5mby5wcm9qZWN0ZWRQcm9kdWN0Q29udGV4dCIsImNyZWF0ZWRfYXQiOiIxNTIwMzA1NDg2OTA4In0.EBgpw0JyKVzbjIBmH6fHDZUvJpvNG8xf8HUHNCK2l-dnVJqXxdi0seOk_kjVodkIa3evC54V560N60vi_mzt7gef-g954VH6l3gFh6XQ7yqRJD2LMW7G1lhQGhga4hrQCnJlfSQoztvIp9hkar9Zcu-MYgyEB5UlwK3KtB3elu7vJGk35F3T9OnqVL4PFj0Ix6zcuN_4gikgQgmtoUjuXULinbtu9Bkmdf7so9FvhapUd5ZTUTTMrAfJ36gEOQPqsuzlu9oUQaYTAn8v4B9TgoS0Paslo6WIksc4f_rSVWsbO6_TSUqIOi0e_RyL6GkMBA1ELA-Dkgbs-jUdkw",
  "expires_in":86399947
}
```

您的访问令牌是键下的 `access_token` 值。 此访问令牌 `expires_in` 86399947毫秒（24小时）。 之后，您必须按照上述步骤生成新访问令牌。

您现在已准备好在Adobe Experience Platform中发出API请求！

### 测试访问代码

要测试访问令牌是否有效，可尝试进行以下API调用。 此调用将列表容器中的所有类 `global` :

>[!NOTE]
>`{API_KEY}` 并参 `{IMS_ORG}` 考您在上面生成的值。

**请求**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```


如果您的响应与下面所示的响应类似，则表明您的 `access_token` 响应有效且有效。 （此响应已被截断，用于空间。）

**响应**

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## 使用Postman进行JWT身份验证和API调用

[Postman](https://www.getpostman.com/) 是一款使用RESTful API的常用工具。 本 [中篇文章介绍](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) ，如何设置邮递员以自动执行JWT身份验证，并使用它使用Adobe Experience Platform API。