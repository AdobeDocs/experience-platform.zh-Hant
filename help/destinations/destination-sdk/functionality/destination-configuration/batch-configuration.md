---
description: 瞭解如何為使用Destination SDK建立的目的地設定檔案匯出設定。
title: 批次設定
exl-id: 0ffbd558-a83c-4c3d-b4fc-b6f7a23a163a
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 2%

---

# 批次設定 {#batch-configuration}

使用Destination SDK中的批次組態選項可讓使用者自訂匯出的檔案名稱，並根據其偏好設定匯出排程。

當您透過Destination SDK建立以檔案為基礎的目的地時，可以設定預設的檔案命名和匯出排程，也可以讓使用者選擇從Platform UI中設定這些設定。 例如，您可以設定行為指令，例如：

* 在檔案名稱中包含特定資訊，例如對象ID、目的地ID或自訂資訊。
* 允許使用者從Platform UI自訂檔案命名。
* 設定檔案匯出，使其以設定的時間間隔進行。
* 定義使用者可在平台UI中看到的檔案命名和匯出排程自訂選項。

批次組態設定是以檔案為基礎的目的地目的地組態的一部分。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱[設定選項](../configuration-options.md)檔案中的圖表，或參閱如何[使用Destination SDK設定檔案型目的地](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)的指南。

您可以透過`/authoring/destinations`端點設定檔案命名和匯出排程設定。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面中顯示的元件。

* [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文會說明您可用於目的地的所有支援批次設定選項，並顯示客戶在Platform UI中會看到的內容。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都區分大小寫&#x200B;****。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

如需瞭解哪些型別的整合支援本頁面所述功能的詳細資訊，請參閱下表。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 無 |
| 檔案式（批次）整合 | 是 |

## 支援的引數 {#supported-parameters}

您在此處設定的值出現在檔案型目的地啟用工作流程的[排程對象匯出](../../../ui/activate-batch-profile-destinations.md#scheduling)步驟中。

```json
"batchConfig":{
   "allowMandatoryFieldSelection":true,
   "allowDedupeKeyFieldSelection":true,
   "defaultExportMode":"DAILY_FULL_EXPORT",
   "allowedExportMode":[
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
   ],
   "allowedScheduleFrequency":[
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
   ],
   "defaultFrequency":"DAILY",
   "defaultStartTime":"00:00",
   "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
   "segmentGroupingEnabled": true
   }
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `allowMandatoryFieldSelection` | 布林值 | 設定為`true`以允許客戶指定哪些設定檔屬性是強制性的。 預設值為`false`。 如需詳細資訊，請參閱[必要屬性](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes)。 |
| `allowDedupeKeyFieldSelection` | 布林值 | 設定為`true`以允許客戶指定重複資料刪除索引鍵。 預設值為`false`。  如需詳細資訊，請參閱[重複資料刪除索引鍵](../../../ui/activate-batch-profile-destinations.md#deduplication-keys)。 |
| `defaultExportMode` | 列舉 | 定義預設檔案匯出模式。 支援的值：<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> 預設值為`DAILY_FULL_EXPORT`。 如需檔案匯出排程的詳細資訊，請參閱[批次啟用檔案](../../../ui/activate-batch-profile-destinations.md#scheduling)。 |
| `allowedExportModes` | 清單 | 定義客戶可用的檔案匯出模式。 支援的值：<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | 清單 | 定義客戶可用的檔案匯出頻率。 支援的值：<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | 列舉 | 定義預設檔案匯出頻率。支援的值：<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> 預設值為 `DAILY`。 |
| `defaultStartTime` | 字串 | 定義檔案匯出的預設開始時間。 使用24小時檔案格式。 預設值為「00:00」。 |
| `filenameConfig.allowedFilenameAppendOptions` | 字串 | *必要*。 可供使用者選擇的可用檔案名稱巨集清單。 這會決定要將哪些專案附加至匯出的檔案名稱（對象ID、組織名稱、匯出的日期和時間等）。 設定`defaultFilename`時，請務必避免重複巨集。 <br><br>支援的值： <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>無論定義巨集的順序為何，Experience PlatformUI一律會依此處呈現的順序顯示巨集。 <br><br>如果`defaultFilename`是空的，則`allowedFilenameAppendOptions`清單必須至少包含一個巨集。 |
| `filenameConfig.defaultFilenameAppendOptions` | 字串 | *必要*。 預先選取的預設檔案名稱巨集，使用者可取消核取。<br><br>此清單中的巨集是`allowedFilenameAppendOptions`中定義的巨集子集。 |
| `filenameConfig.defaultFilename` | 字串 | *選擇性*。 定義匯出檔案的預設檔案名稱巨集。 使用者無法覆寫這些專案。 <br><br> `allowedFilenameAppendOptions`所定義的任何巨集都會附加到`defaultFilename`巨集之後。 <br><br>如果`defaultFilename`是空的，您必須在`allowedFilenameAppendOptions`中至少定義一個巨集。 |
| `segmentGroupingEnabled` | 布林值 | 根據對象[合併原則](../../../../profile/merge-policies/overview.md)，定義啟用的對象應匯出為單一檔案還是多個檔案。 支援的值： <ul><li>`true`：每個合併原則匯出一個檔案。</li><li>`false`：無論合併原則為何，都會為每個對象匯出單一檔案。 這是預設行為。 完全忽略此引數也能達到相同的結果。</li></ul> |

{style="table-layout:auto"}

## 檔案名稱組態 {#file-name-configuration}

使用檔案名稱組態巨集來定義匯出的檔案名稱應包含的內容。 下表中的巨集說明在[檔案名稱組態](../../../ui/activate-batch-profile-destinations.md#file-names)畫面的UI中找到的元素。

>[!TIP]
> 
>您最好在匯出的檔案名稱中一律包含`SEGMENT_ID`巨集。 區段ID是唯一的，因此將其納入檔案名稱中，也是確保檔案名稱唯一的最佳方式。

| 巨集 | UI標籤 | 說明 | 範例 |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL 目標] | ui中的目的地名稱。 | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL 區段識別碼] | 平台產生的唯一受眾ID | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL 區段名稱] | 使用者定義的對象名稱 | VIP訂閱者 |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL 目的地識別碼] | 目的地執行個體的唯一Platform產生ID | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL 目的地名稱] | 目的地執行個體的使用者定義名稱。 | 我的2022 Advertising目的地 |
| `ORGANIZATION_NAME` | [!UICONTROL 組織名稱] | Adobe Experience Platform中的客戶組織名稱。 | 我的組織名稱 |
| `SANDBOX_NAME` | [!UICONTROL 沙箱名稱] | 客戶使用的沙箱名稱。 | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL 日期和時間] | `DATETIME`和`TIMESTAMP`都定義產生檔案的時間，但格式不同。<br><br><ul><li>`DATETIME`使用以下格式： YYYYMMDD_HHMMSS。</li><li>`TIMESTAMP`使用10位數Unix格式。 </li></ul> `DATETIME`與`TIMESTAMP`互斥，不能同時使用。 | <ul><li>`DATETIME`： 20220509_210543</li><li>`TIMESTAMP`： 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL 自訂文字] | 要包含在檔案名稱中的使用者定義自訂文字。 無法在`defaultFilename`中使用。 | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL 日期和時間] | 檔案產生時間的10位數時間戳記，以Unix格式顯示。 | 1652131584 |
| `MERGE_POLICY_ID` | [!UICONTROL 合併原則ID] | 用來產生匯出對象的[合併原則](../../../../profile/merge-policies/overview.md)識別碼。 當您根據合併原則將匯出的對象分組到檔案中時，請使用此巨集。 使用此巨集與`segmentGroupingEnabled:true`。 | e8591fdb-2873-4b12-b63e-15275b1c1439 |
| `MERGE_POLICY_NAME` | [!UICONTROL 合併原則名稱] | 用來產生匯出對象的[合併原則](../../../../profile/merge-policies/overview.md)的名稱。 當您根據合併原則將匯出的對象分組到檔案中時，請使用此巨集。 使用此巨集與`segmentGroupingEnabled:true`。 | 我的自訂合併原則 |

{style="table-layout:auto"}

### 檔案名稱設定範例

以下設定範例顯示API呼叫中使用的設定與UI中顯示的選項之間的對應。

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```

![顯示檔案名稱組態畫面的UI影像，其中包含預先選取的巨集](../../assets/functionality/destination-configuration/file-name-configuration.png)

## 後續步驟 {#next-steps}

閱讀本文後，您應該更瞭解如何為檔案型目的地設定檔案命名和匯出排程。

若要深入瞭解其他目的地元件，請參閱下列文章：

* [客戶驗證設定](customer-authentication.md)
* [OAuth2授權](oauth2-authorization.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [綱要設定](schema-configuration.md)
* [身分名稱空間設定](identity-namespace-configuration.md)
* [支援的對應設定](supported-mapping-configurations.md)
* [目的地傳遞](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [彙總原則](aggregation-policy.md)
* [歷史設定檔資格](historical-profile-qualifications.md)
