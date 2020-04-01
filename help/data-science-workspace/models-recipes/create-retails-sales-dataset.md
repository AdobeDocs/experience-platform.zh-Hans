---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 创建零售模式和数据集
topic: Tutorial
translation-type: tm+mt
source-git-commit: 91c7b7e285a4745da20ea146f2334510ca11b994

---


# 创建零售模式和数据集

本教程为您提供了所有其他Adobe Experience Platform Data Science Workspace教程所需的入门项目和资源。 完成后，您和您的IMS组织的Experience Platform成员将获得零售模式和数据集。

## 入门指南

在开始本教程之前，您必须具备以下先决条件：
- 访问Adobe Experience Platform。 如果您无权访问Experience Platform中的IMS组织，请在继续操作之前与系统管理员联系。
- 授权进行Experience Platform API调用。 完成 [身份验证并访问Adobe Experience Platform API](../../tutorials/authentication.md) ，获取以下值以成功完成本教程：
   - 授权： `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - 客户机密码： `{CLIENT_SECRET}`
   - 客户端证书： `{PRIVATE_KEY}`
- 零售销售菜谱的示例数据 [和源文件](../pre-built-recipes/retail-sales.md)。 从 [Adobe公共Git存储库下载本教程和其他数据科学工作区教程所需的资源](https://github.com/adobe/experience-platform-dsw-reference/)。
- [Python >= 2.7](https://www.python.org/downloads/) ，以及以下Python包：
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [字典](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 对本教程中使用的以下概念的有效理解：
   - [体验数据模型(XDM)](../../xdm/home.md)
   - [模式合成基础](../../xdm/schema/field-dictionary.md)

## 创建零售销售模式和数据集

零售销售模式和数据集是使用提供的引导脚本自动创建的。 按照以下步骤操作：

### 配置文件

1. 在Experience Platform教程资源包中，导航到该目录，然 `bootstrap`后使用相应的文 `config.yaml` 本编辑器打开。
2. 在该部 `Enterprise` 分下，输入以下值：

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. 编辑在下面示例的部 `Platform` 分下找到的值：

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
   - `ingest_data` :在本教程中，请将此值设置为，以 `"True"` 便创建零售模式和数据集。 值将仅 `"False"` 创建模式。
   - `build_recipe_artifacts` :为了在本教程中，请将此值设置为，以 `"False"` 防止脚本生成Recipe对象。
   - `kernel_type` :Recipe对象的执行类型。 将此值保留 `Python` 为 `build_recipe_artifacts` 设置，否则 `"False"`请指定正确的执行类型。

4. 在该部 `Titles` 分下，为零售销售示例数据提供相应的以下信息，在进行编辑后保存并关闭文件。 示例如下：

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

1. 打开您的终端应用程序，然后导航到Experience Platform教程资源目录。
2. 将目 `bootstrap` 录设置为当前工作路径，并输入以 `bootstrap.py` 下命令运行python脚本：

   ```bash
   python bootstrap.py
   ```

   > [!NOTE] 完成脚本可能需要几分钟。

## 后续步骤

成功完成引导脚本后，可在Experience Platform上查看零售销售的输入和输出模式以及数据集。 有关详细 [信息，请参阅预览](./preview-schema-data.md)模式数据教程。

您还使用提供的引导脚本成功地将零售销售示例数据引入Experience Platform。

要继续使用摄取的数据，请执行以下操作：
- [使用Jupyter笔记本分析数据](../jupyterlab/analyze-your-data.md)
   - 使用Data Science Workspace中的Jupyter笔记本电脑访问、探索、可视化和了解您的数据。
- [将源文件打包到菜谱中](./package-source-files-recipe.md)
   - 按照本教程学习如何通过将源文件打包到可导入的Recipe文件中，将您自己的模型引入数据科学工作区。