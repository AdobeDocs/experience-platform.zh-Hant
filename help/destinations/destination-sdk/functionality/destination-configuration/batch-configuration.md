---
description: 瞭解如何為使用Destination SDK構建的目標配置檔案導出設定。
title: 批配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 4%

---


# 批配置 {#batch-configuration}

使用Destination SDK中的批配置選項，允許用戶自定義導出的檔案名，並根據其首選項配置導出計畫。

通過Destination SDK建立基於檔案的目標時，可以配置預設的檔案命名和導出計畫，也可以為用戶提供從平台UI配置這些設定的選項。 例如，可以配置以下行為：

* 包括檔案名中的特定資訊，如段ID、目標ID或自定義資訊。
* 允許用戶從平台UI自定義檔案命名。
* 將檔案導出配置為按設定的時間間隔進行。
* 定義用戶可以在平台UI中看到的檔案命名和導出計畫自定義選項。

批處理配置設定是基於檔案的目標的目標配置的一部分。

要瞭解此元件在與Destination SDK建立的整合中的位置，請參閱 [配置選項](../configuration-options.md) 文檔，或參閱有關如何 [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)。

您可以通過 `/authoring/destinations` 端點。 有關詳細的API調用示例，請參閱以下API參考頁，在這些示例中可以配置此頁中顯示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介紹可用於目標的所有支援的批處理配置選項，並顯示客戶將在平台UI中看到的內容。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 支援的整合類型 {#supported-integration-types}

有關哪些類型的整合支援本頁所述功能的詳細資訊，請參閱下表。

| 整合類型 | 支援功能 |
|---|---|
| 即時（流）整合 | 無 |
| 基於檔案（批處理）的整合 | 是 |

## 支援的參數 {#supported-parameters}

此處設定的值在 [計畫段導出](../../../ui/activate-batch-profile-destinations.md#scheduling) 基於檔案的目標激活工作流的步驟。

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
| `allowMandatoryFieldSelection` | 布林值 | 設定為 `true` 允許客戶指定哪些配置檔案屬性是必需的。 預設值為 `false`。請參閱 [必需屬性](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes) 的子菜單。 |
| `allowDedupeKeyFieldSelection` | 布林值 | 設定為 `true` 允許客戶指定重複資料消除密鑰。 預設值為 `false`。請參閱 [重複資料消除密鑰](../../../ui/activate-batch-profile-destinations.md#deduplication-keys) 的子菜單。 |
| `defaultExportMode` | 枚舉 | 定義預設檔案導出模式。 支援的值：<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> 預設值為 `DAILY_FULL_EXPORT`。查看 [批量激活文檔](../../../ui/activate-batch-profile-destinations.md#scheduling) 的子菜單。 |
| `allowedExportModes` | 清單 | 定義客戶可用的檔案導出模式。 支援的值：<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | 清單 | 定義客戶可用的檔案導出頻率。 支援的值：<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | 枚舉 | 定義預設檔案導出頻率。支援的值：<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> 預設值為 `DAILY`。 |
| `defaultStartTime` | 字串 | 定義檔案導出的預設開始時間。 使用24小時檔案格式。 預設值為「00:00」。 |
| `filenameConfig.allowedFilenameAppendOptions` | 字串 | *必填*. 可供用戶選擇的可用檔案名宏清單。 這確定將哪些項附加到導出的檔案名（段ID、組織名稱、導出日期和時間等）。 設定時 `defaultFilename`，確保避免複製宏。 <br><br>支援的值： <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>無論宏的定義順序如何，Experience PlatformUI始終按此處顯示的順序顯示宏。 <br><br> 如果 `defaultFilename` 是空的， `allowedFilenameAppendOptions` 清單必須至少包含一個宏。 |
| `filenameConfig.defaultFilenameAppendOptions` | 字串 | *必填*. 用戶可以取消選中的預選預設檔案名宏。<br><br> 此清單中的宏是中定義的宏的子集 `allowedFilenameAppendOptions`。 |
| `filenameConfig.defaultFilename` | 字串 | *可選*. 定義導出檔案的預設檔案名宏。 用戶無法覆蓋這些內容。 <br><br>由定義的任何宏 `allowedFilenameAppendOptions` 將在 `defaultFilename` 宏。 <br><br>如果 `defaultFilename` 為空，您必須在 `allowedFilenameAppendOptions`。 |

{style="table-layout:auto"}

## 檔案名配置 {#file-name-configuration}

使用檔案名配置宏定義導出的檔案名應包括的內容。 下表中的宏描述了在UI中找到的元素 [檔案名配置](../../../ui/activate-batch-profile-destinations.md#file-names) 的上界。

>[!TIP]
> 
>作為最佳做法，您應始終包括 `SEGMENT_ID` 宏。 段ID是唯一的，因此將它們包括在檔案名中是確保檔案名也唯一的最佳方法。

| 宏 | UI標籤 | 說明 | 範例 |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL 目標] | UI中的目標名稱。 | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL 段ID] | 唯一、平台生成的段ID | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL 段名稱] | 用戶定義的段名稱 | VIP訂戶 |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL 目標ID] | 目標實例的唯一、平台生成的ID | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL 目標名稱] | 目標實例的用戶定義的名稱。 | 我2022年的廣告目的地 |
| `ORGANIZATION_NAME` | [!UICONTROL 組織名稱] | 客戶組織在Adobe Experience Platform的名稱。 | 我的組織名稱 |
| `SANDBOX_NAME` | [!UICONTROL 沙箱名稱] | 客戶使用的沙盒的名稱。 | 收縮 |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL 日期和時間] | `DATETIME` 和 `TIMESTAMP` 兩者都定義生成檔案的時間，但格式不同。 <br><br><ul><li>`DATETIME` 使用以下格式：YYYYMMDD_HHMMSS。</li><li>`TIMESTAMP` 使用10位Unix格式。 </li></ul> `DATETIME` 和 `TIMESTAMP` 互斥，不能同時使用。 | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL 自定義文本] | 要包含在檔案名中的用戶定義的自定義文本。 不能用於 `defaultFilename`。 | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL 日期和時間] | 以Unix格式生成檔案的時間的10位時間戳。 | 1652131584 |

{style="table-layout:auto"}

### 檔案名配置示例

下面的配置示例顯示了API調用中使用的配置與UI中顯示的選項之間的對應關係。

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

![顯示帶有預選宏的檔案名配置螢幕的UI影像](../../assets/functionality/destination-configuration/file-name-configuration.png)

## 後續步驟 {#next-steps}

閱讀本文後，您應更好地瞭解如何為基於檔案的目標配置檔案命名和導出計畫。

要瞭解有關其他目標元件的詳細資訊，請參閱以下文章：

* [客戶身份驗證配置](customer-authentication.md)
* [OAuth2身份驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [架構配置](schema-configuration.md)
* [標識命名空間配置](identity-namespace-configuration.md)
* [支援的映射配置](supported-mapping-configurations.md)
* [目標傳遞](destination-delivery.md)
* [受眾元資料配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [歷史配置檔案資格](historical-profile-qualifications.md)