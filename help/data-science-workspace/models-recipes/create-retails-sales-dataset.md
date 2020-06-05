---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 建立零售銷售結構和資料集
topic: Tutorial
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# 建立零售銷售結構和資料集

本教學課程提供所有其他資料科學工作區教學課程的必 [!DNL Adobe Experience Platform] 要條件和資產。 完成後，您和您的IMS組織Experience Platform成員將可使用零售銷售架構和資料集。

## 快速入門

開始本教學課程之前，您必須具備下列必要條件：
- 存取權 [!DNL Adobe Experience Platform]。 如果您無法存取Experience Platform中的IMS組織，請在繼續前先與系統管理員聯絡。
- 授權進行Experience Platform API呼叫。 完成「 [驗證並存取Adobe Experience Platform API](../../tutorials/authentication.md) 」教學課程，以取得下列值，以順利完成本教學課程：
   - 授權： `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - 用戶端密碼： `{CLIENT_SECRET}`
   - 用戶端憑證： `{PRIVATE_KEY}`
- 零售銷售方式的資料和來 [源檔案範例](../pre-built-recipes/retail-sales.md)。 從 [Adobe公用Git存放庫下載本課程和其他資料科學工作區教學課程所需的資產](https://github.com/adobe/experience-platform-dsw-reference/)。
- [Python >= 2.7](https://www.python.org/downloads/) ，以及下列Python套件：
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 對本教學課程中使用的下列概念有正確認識：
   - [體驗資料模型(XDM)](../../xdm/home.md)
   - [架構構成基礎](../../xdm/schema/field-dictionary.md)

## 建立零售銷售結構和資料集

零售銷售方案和資料集是使用提供的引導指令碼自動建立的。 請依下列步驟進行：

### 設定檔案

1. 在Experience Platform教學課程資源套件中，導覽至目錄，然 `bootstrap`後使用適 `config.yaml` 當的文字編輯器開啟。
2. 在區段 `Enterprise` 下輸入下列值：

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. 編輯在區段下找到的 `Platform` 值，範例如下：

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` : API呼叫的基本路徑。 請勿修改此值。
   - `ims_token` : 你 `{ACCESS_TOKEN}` 來這。
   - `ingest_data` : 在本教程中，請將此值設定為，以 `"True"` 便建立零售銷售方案和資料集。 值將僅 `"False"` 建立結構。
   - `build_recipe_artifacts` : 在本教學課程中，請將此值設 `"False"` 定為防止指令碼產生Recipe對象。
   - `kernel_type` : 處方對象的執行類型。 將此值保留為 `Python` 設 `build_recipe_artifacts` 為，否則 `"False"`請指定正確的執行類型。

4. 在「零 `Titles` 售銷售」範例資料中，請適當提供下列資訊，在編輯完成後儲存並關閉檔案。 範例如下：

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

### 運行引導指令碼

1. 開啟您的終端應用程式，並導覽至Experience Platform教學課程資源目錄。
2. 將目 `bootstrap` 錄設定為當前工作路徑，並輸入以 `bootstrap.py` 下命令運行Python指令碼：

   ```bash
   python bootstrap.py
   ```

   > [!NOTE] 完成指令碼可能需要幾分鐘的時間。

## 後續步驟

成功完成引導指令碼後，您就可在Experience Platform上檢視零售銷售的輸入和輸出結構描述和資料集。 如需詳細 [資訊，請參閱預覽](./preview-schema-data.md)架構資料教學課程。

您也已使用提供的引導指令碼，成功將零售銷售範例資料納入Experience Platform。

要繼續使用收錄的資料：
- [使用Jupyter筆記型電腦分析資料](../jupyterlab/analyze-your-data.md)
   - 使用Data Science Workspace中的Jupyter筆記型電腦存取、探索、視覺化和瞭解您的資料。
- [將來源檔案封裝至配方](./package-source-files-recipe.md)
   - 請依照本教學課程學習如何將來源檔案封裝在可匯入的方式檔案中，將您自己的模型帶入資料科學工作區。