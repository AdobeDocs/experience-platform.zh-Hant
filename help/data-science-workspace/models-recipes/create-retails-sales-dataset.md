---
keywords: Experience Platform；零售銷售配方；資料科學工作區；熱門主題；配方
solution: Experience Platform
title: 建立零售銷售結構和資料集
topic-legacy: tutorial
type: Tutorial
description: 本教學課程提供您其他Adobe Experience Platform資料科學工作區教學課程的必要條件和必要資產。 完成後，您和您的IMS組織成員將可使用零售銷售方案和資料集進行Experience Platform。
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# 建立零售銷售結構和資料集

本教學課程提供所有其他[!DNL Adobe Experience Platform] [!DNL Data Science Workspace]教學課程的必要條件和資產。 完成後，您和[!DNL Experience Platform]上的IMS組織成員將可使用零售銷售方案和資料集。

## 快速入門

開始本教學課程之前，您必須具備下列必要條件：
- 存取[!DNL Adobe Experience Platform]。 如果您沒有[!DNL Experience Platform]中IMS組織的存取權，請在繼續之前先與系統管理員聯絡。
- 進行[!DNL Experience Platform] API呼叫的授權。 完成[驗證並訪問Adobe Experience PlatformAPI](https://www.adobe.com/go/platform-api-authentication-en)教程，以獲取以下值，以成功完成本教程：
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key:`{API_KEY}`
   - x-gw-ims-org-id:`{IMS_ORG}`
   - 用戶端密碼：`{CLIENT_SECRET}`
   - 用戶端憑證：`{PRIVATE_KEY}`
- [零售銷售方式](../pre-built-recipes/retail-sales.md)的示例資料和源檔案。 從[Adobe公用Git儲存庫](https://github.com/adobe/experience-platform-dsw-reference/)下載此教學課程和其他[!DNL Data Science Workspace]教學課程所需的資產。
- [Python >= 2.7](https://www.python.org/downloads/) 和以下軟 [!DNL Python] 件包：
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 對本教學課程中使用的下列概念有正確認識：
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [架構構成基礎](../../xdm/schema/field-dictionary.md)

## 建立零售銷售結構和資料集

零售銷售方案和資料集是使用提供的引導指令碼自動建立的。 請依下列步驟進行：

### 設定檔案

1. 在[!DNL Experience Platform]教程資源包中，導航到`bootstrap`目錄，然後使用適當的文本編輯器開啟`config.yaml`。
2. 在`Enterprise`節下輸入以下值：

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. 編輯`Platform`節下找到的值，如下所示：

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` :API呼叫的基本路徑。請勿修改此值。
   - `ims_token` :你 `{ACCESS_TOKEN}` 來這。
   - `ingest_data` :在本教程中，請將此值設定為，以 `"True"` 便建立零售銷售方案和資料集。值`"False"`將僅建立方案。
   - `build_recipe_artifacts` :在本教學課程中，請將此值設 `"False"` 定為防止指令碼產生Recipe對象。
   - `kernel_type` :處方對象的執行類型。如果`build_recipe_artifacts`設為`"False"`，請將此值保留為`Python`，否則請指定正確的執行類型。

4. 在`Titles`區段下，為零售銷售示例資料提供下列適當資訊，在編輯完成後儲存並關閉檔案。 範例如下：

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

1. 開啟終端應用程式並導航到[!DNL Experience Platform]教程資源目錄。
2. 將`bootstrap`目錄設定為當前工作路徑，然後輸入以下命令運行`bootstrap.py` [!DNL Python]指令碼：

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >完成指令碼可能需要幾分鐘的時間。

## 後續步驟

成功完成引導指令碼後，可在[!DNL Experience Platform]上查看零售銷售部門的輸入和輸出方案和資料集。 請參閱[預覽架構資料教學課程](./preview-schema-data.md)
的上界。

您也使用提供的引導指令碼成功將零售銷售示例資料導入[!DNL Experience Platform]。

要繼續使用收錄的資料：
- [使用Jupyter Notebooks分析資料](../jupyterlab/analyze-your-data.md)
   - 使用Data Science Workspace中的Jupyter Notebooks來存取、探索、視覺化和瞭解您的資料。
- [將來源檔案封裝至配方](./package-source-files-recipe.md)
   - 請依照本教學課程，瞭解如何將來源檔案封裝在可匯入的方式檔案中，將您自己的模型帶入[!DNL Data Science Workspace]。
