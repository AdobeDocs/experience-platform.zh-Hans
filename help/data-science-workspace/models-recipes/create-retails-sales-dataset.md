---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics;recipes
solution: Experience Platform
title: 创建零售销售模式和数据集
topic: tutorial
type: Tutorial
description: 本教程为您提供了所有其他Adobe Experience Platform数据科学工作区教程所需的先决条件和资源。 完成后，您和您的IMS组织成员将可以在Experience Platform上获得零售模式和数据集。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# 创建零售销售模式和数据集

本教程为您提供所有其他教程所需的入门项目和 [!DNL Adobe Experience Platform] 资 [!DNL Data Science Workspace] 源。 完成后，您和您的IMS组织成员将获得零售销售模式和数据集 [!DNL Experience Platform]。

## 入门指南

在开始本教程之前，您必须具有以下先决条件：
- 访问 [!DNL Adobe Experience Platform]。 如果您无权访问中的IMS组织，请在继 [!DNL Experience Platform]续操作之前与系统管理员联系。
- 进行API调 [!DNL Experience Platform] 用的授权。 请完成 [身份验证和访问Adobe Experience PlatformAPI](../../tutorials/authentication.md) (Authenticate and access Methonic API)教程，获取以下值以成功完成本教程：
   - 授权： `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - 客户机密码： `{CLIENT_SECRET}`
   - 客户端证书： `{PRIVATE_KEY}`
- 零售销售处方的示例数 [据和源文件](../pre-built-recipes/retail-sales.md)。 从Adobe公共Git存储库下载本教程 [!DNL Data Science Workspace] 和其他教程 [所需的资源](https://github.com/adobe/experience-platform-dsw-reference/)。
- [Python >= 2.7](https://www.python.org/downloads/) 和以下 [!DNL Python] 包：
   - [画](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [字典](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 对本教程中使用的以下概念的有效理解：
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [模式合成基础](../../xdm/schema/field-dictionary.md)

## 创建零售销售模式和数据集

零售销售模式和数据集是使用提供的引导脚本自动创建的。 按照以下步骤操作：

### 配置文件

1. 在教程 [!DNL Experience Platform] 资源包中，导航到目录，然 `bootstrap`后使用相 `config.yaml` 应的文本编辑器打开。
2. 在该部 `Enterprise` 分下输入以下值：

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. 编辑在“示例”部分下 `Platform` 找到的值，如下所示：

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` :API调用的基本路径。 请勿修改此值。
   - `ims_token` :你 `{ACCESS_TOKEN}` 来这。
   - `ingest_data` :在本教程中，请将此值设 `"True"` 置为创建零售销售模式和数据集。 值将仅 `"False"` 创建模式。
   - `build_recipe_artifacts` :为在本教程中起作用，请将此值设 `"False"` 置为阻止脚本生成Recipe项目。
   - `kernel_type` :Recipe对象的执行类型。 将此值保留 `Python` 为 `build_recipe_artifacts` ，否则 `"False"`请指定正确的执行类型。

4. 在部分 `Titles` 下，为零售销售示例数据提供相应的以下信息，在编辑到位后保存并关闭文件。 示例如下：

   ```yaml
   Titles:
       input_class_title: retail_sales_input_class
       input_mixin_title: retail_sales_input_mixin
       input_mixin_definition_title: retail_sales_input_mixin_definition
       input_schema_title: retail_sales_input_schema
       input_dataset_title: retail_sales_input_dataset
       file_replace_tenant_id: DSWRetailSalesForXDM0.9.9.9.json
       file_with_tenant_id: DSWRetailSales_with_tenant_id.json
       is_output_schema_different: "True"
       output_mixin_title: retail_sales_output_mixin
       output_mixin_definition_title: retail_sales_output_mixin_definition
       output_schema_title: retail_sales_output_title
       output_dataset_title: retail_sales_output_dataset
   ```

### 运行引导脚本

1. 打开您的终端应用程序并导航到 [!DNL Experience Platform] 教程资源目录。
2. 将目 `bootstrap` 录设置为当前工作路径，并输入以 `bootstrap.py` 下命 [!DNL Python] 令运行脚本：

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >完成脚本可能需要几分钟。

## 后续步骤

成功完成引导脚本后，可以在上查看零售销售的输入和输出模式和数据集 [!DNL Experience Platform]。 有关详细 [信息，请参](./preview-schema-data.md)阅预览模式数据教程。

您还使用提供的引导脚本成功将零售 [!DNL Experience Platform] 销售示例数据引入。

要继续处理所摄取的数据：
- [使用Jupyter笔记本分析数据](../jupyterlab/analyze-your-data.md)
   - 在数据科学工作区中使用Jupyter笔记本，访问、探索、可视化和了解您的数据。
- [将源文件打包到菜谱中](./package-source-files-recipe.md)
   - 请按照本教程学习如何通过将源文件打包到可 [!DNL Data Science Workspace] 导入的Recipe文件中，将自己的Model引入其中。