---
description: 了解如何為使用Destination SDK建置的目的地配置檔案匯出設定。
title: 批次設定
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 4%

---


# 批次設定 {#batch-configuration}

使用Destination SDK中的批配置選項，允許用戶自定義導出的檔案名並根據其首選項配置導出計畫。

透過Destination SDK建立檔案式目的地時，您可以設定預設的檔案命名和匯出排程，或者也可以讓使用者從Platform UI設定這些設定的選項。 例如，您可以設定下列行為：

* 在檔案名稱中包括特定資訊，例如區段ID、目的地ID或自訂資訊。
* 允許使用者從Platform UI自訂檔案命名。
* 將檔案匯出設定為在設定的時間間隔進行。
* 定義使用者可在Platform UI中看到的檔案命名和匯出排程自訂選項。

批次組態設定是檔案式目的地的目的地組態的一部分。

若要了解此元件在透過Destination SDK建立的整合中的插入位置，請參閱 [配置選項](../configuration-options.md) 檔案，或參閱如何 [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

您可以透過 `/authoring/destinations` 端點。 如需詳細API呼叫範例，請參閱下列API參考頁面，您可在其中設定本頁面所示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文說明您可用於目的地的所有支援批次設定選項，並說明客戶在Platform UI中會看到什麼。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 支援的整合類型 {#supported-integration-types}

如需詳細資訊，請參閱下表以了解哪些類型的整合支援本頁面所述的功能。

| 整合類型 | 支援功能 |
|---|---|
| 即時（串流）整合 | 無 |
| 檔案式（批次）整合 | 是 |

## 支援的參數 {#supported-parameters}

您在這裡設定的值會在 [排程區段匯出](../../../ui/activate-batch-profile-destinations.md#scheduling) 檔案式目的地啟動工作流程的步驟。

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
   }
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `allowMandatoryFieldSelection` | 布林值 | 設為 `true` 允許客戶指定哪些設定檔屬性為強制屬性。 預設值為 `false`。請參閱 [強制屬性](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes) 以取得更多資訊。 |
| `allowDedupeKeyFieldSelection` | 布林值 | 設為 `true` 允許客戶指定重複資料刪除金鑰。 預設值為 `false`。請參閱 [重複資料刪除密鑰](../../../ui/activate-batch-profile-destinations.md#deduplication-keys) 以取得更多資訊。 |
| `defaultExportMode` | 列舉 | 定義預設的檔案導出模式。 支援的值：<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> 預設值為 `DAILY_FULL_EXPORT`。請參閱 [批次啟動檔案](../../../ui/activate-batch-profile-destinations.md#scheduling) 以取得檔案匯出排程的詳細資訊。 |
| `allowedExportModes` | 清單 | 定義客戶可用的檔案匯出模式。 支援的值：<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | 清單 | 定義客戶可用的檔案匯出頻率。 支援的值：<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | 列舉 | 定義預設檔案導出頻率。支援的值：<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> 預設值為 `DAILY`。 |
| `defaultStartTime` | 字串 | 定義檔案導出的預設開始時間。 使用24小時檔案格式。 預設值為「00:00」。 |
| `filenameConfig.allowedFilenameAppendOptions` | 字串 | *必填*. 可供用戶選擇的可用檔案名宏清單。 這會決定要將哪些項目附加至匯出的檔案名稱（區段ID、組織名稱、匯出的日期和時間，以及其他）。 設定時 `defaultFilename`，請務必避免重複執行巨集。 <br><br>支援的值： <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>無論您定義巨集的順序為何，Experience PlatformUI都會依此處顯示的順序顯示巨集。 <br><br> 若 `defaultFilename` 空白， `allowedFilenameAppendOptions` 清單必須至少包含一個宏。 |
| `filenameConfig.defaultFilenameAppendOptions` | 字串 | *必填*. 預選的預設檔案名宏，用戶可以取消選中這些宏。<br><br> 此清單中的巨集是 `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | 字串 | *可選*. 定義導出檔案的預設檔案名宏。 使用者無法覆寫這些項目。 <br><br>定義的任何宏 `allowedFilenameAppendOptions` 會附加在 `defaultFilename` 巨集。 <br><br>若 `defaultFilename` 空白，您必須在中定義至少一個巨集 `allowedFilenameAppendOptions`. |

{style="table-layout:auto"}

## 檔案名配置 {#file-name-configuration}

使用檔案名配置宏定義導出的檔案名應包括哪些內容。 下表中的巨集說明在 [檔案名配置](../../../ui/activate-batch-profile-destinations.md#file-names) 螢幕。

>[!TIP]
> 
>作為最佳實務，您應一律包含 `SEGMENT_ID` 宏。 區段ID是唯一的，因此將它們納入檔案名稱是確保檔案名稱也唯一的最佳方式。

| 巨集 | UI標籤 | 說明 | 範例 |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL 目標] | UI中的目的地名稱。 | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL 區段ID] | 不重複、平台產生的區段ID | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL 區段名稱] | 使用者定義的區段名稱 | VIP訂閱者 |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL 目的地ID] | 目的地例項的不重複、平台產生的ID | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL 目的地名稱] | 目標實例的用戶定義名稱。 | 我的2022年廣告目的地 |
| `ORGANIZATION_NAME` | [!UICONTROL 組織名稱] | Adobe Experience Platform中的客戶組織名稱。 | 我的組織名稱 |
| `SANDBOX_NAME` | [!UICONTROL 沙箱名稱] | 客戶使用的沙箱名稱。 | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL 日期和時間] | `DATETIME` 和 `TIMESTAMP` 兩者都會定義檔案的產生時間，但格式不同。 <br><br><ul><li>`DATETIME` 使用下列格式：YYYYMMDD_HHMMSS。</li><li>`TIMESTAMP` 使用10位Unix格式。 </li></ul> `DATETIME` 和 `TIMESTAMP` 互斥，且無法同時使用。 | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL 自訂文字] | 要包含在檔案名稱中的用戶定義自定義文本。 無法用於 `defaultFilename`. | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL 日期和時間] | 10位數的檔案產生時間時間戳記，採用Unix格式。 | 1652131584 |

{style="table-layout:auto"}

### 檔案名配置示例

以下的設定範例顯示API呼叫中使用的設定與UI中顯示的選項之間的對應關係。

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

![顯示檔案名配置螢幕的UI影像以及預先選擇的宏](../../assets/functionality/destination-configuration/file-name-configuration.png)

## 後續步驟 {#next-steps}

閱讀本文後，您應該更清楚了解如何為檔案型目的地設定檔案命名和匯出排程。

若要進一步了解其他目的地元件，請參閱下列文章：

* [客戶驗證配置](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [結構配置](schema-configuration.md)
* [身分命名空間設定](identity-namespace-configuration.md)
* [支援的對應配置](supported-mapping-configurations.md)
* [目的地傳送](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [歷史設定檔資格](historical-profile-qualifications.md)