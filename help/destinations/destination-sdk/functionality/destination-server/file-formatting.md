---
description: 瞭解如何通過「/destination-servers」終結點為使用Adobe Experience Platform Destination SDK構建的基於檔案的目標配置檔案格式選項。
title: 檔案格式配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 4%

---


# 檔案格式配置

Destination SDK支援一組靈活的功能，您可以根據整合需要配置這些功能。 這些功能包括 [!DNL CSV] 檔案格式保存影像映射。

通過Destination SDK建立基於檔案的目標時，可以定義導出的CSV檔案的格式。 您可以自定義許多格式設定選項，例如，但不限於：

* CSV檔案是否應包括標題；
* 要用什麼字元來引用值；
* 空值應該是什麼樣。

根據目標配置，用戶在連接到基於檔案的目標時將在用戶介面中看到某些選項。 您可以在 [基於檔案的目標的檔案格式選項](../../../ui/batch-destinations-file-formatting-options.md) 文檔。


檔案格式設定是基於檔案的目標的目標伺服器配置的一部分。

要瞭解此元件在與Destination SDK建立的整合中的位置，請參閱 [配置選項](../configuration-options.md) 文檔，或參閱有關如何 [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)。

您可以通過 `/authoring/destination-servers` 端點。 有關詳細的API調用示例，請參閱以下API參考頁，在這些示例中可以配置此頁中顯示的元件。

* [建立目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)
* [更新目標伺服器配置](../../authoring-api/destination-server/update-destination-server.md)

此頁介紹導出的所有支援的檔案格式設定 `CSV` 的子菜單。

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

您可以修改導出檔案的幾個屬性以符合目標檔案接收系統的要求，以便以最佳方式讀取和解釋從Experience Platform接收的檔案。

>[!NOTE]
>
>僅當導出CSV檔案時才支援CSV選項。 的 `fileConfigurations` 設定新目標伺服器時，不必使用節。 如果在API調用中未傳遞任何CSV選項的值，則預設值 [參考表](#file-formatting-reference-and-example) 的下界。


## 用戶無法選擇配置選項的CSV選項 {#file-configuration-templating-none}

在下面的配置示例中，所有CSV選項都是預定義的。 在 `csvOptions` 參數是最終參數，用戶無法修改它們。

```json
"fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        },
        "maxFileRowCount":5000000
    }
```

## CSV選項，用戶可以在其中選擇配置選項 {#file-configuration-templating-pebble}

在下面的配置示例中，沒有預定義任何CSV選項。 的 `value` 在 `csvOptions` 參數通過相應的客戶資料欄位進行配置 `/destinations` 端點(例如 [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) 為 `quote` 檔案格式選項)，用戶可以使用Experience PlatformUI在您在相應的客戶資料欄位中配置的各種選項之間進行選擇。 您可以在 [基於檔案的目標的檔案格式選項](../../../ui/batch-destinations-file-formatting-options.md) 文檔。

```json
{
   "fileConfigurations":{
      "compression":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
      },
      "fileType":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.fileType}}"
      },
      "csvOptions":{
         "sep":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
         },
         "quote":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
         },
         "escape":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
         },
         "nullValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
         },
         "emptyValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
         }
      }
   }
}
```

## 完整的參考和支援的檔案格式選項示例 {#file-formatting-reference-and-example}

>[!TIP]
>
>下面介紹的CSV檔案格式選項也在 [CSV檔案的Apache Spark指南](https://spark.apache.org/docs/latest/sql-data-sources-csv.html)。 下面使用的說明摘自Apache Spark指南。

下面是Destination SDK中所有可用檔案格式選項的完整引用，以及每個選項的輸出示例。

| 欄位 | 必填/選填 | 說明 | 預設值 | 示例輸出1 | 示例輸出2 |
|---|---|---|---|---|---|
| `templatingStrategy` | 必填 | 對於您配置的每個檔案格式選項，需要添加參數 `templatingStrategy`，它可以有兩個值： <br><ul><li>`NONE`:如果您不打算允許用戶在配置的不同值之間進行選擇，請使用此值。 請參閱 [此配置](#file-configuration-templating-none) 例如，檔案格式選項是固定的。</li><li>`PEBBLE_V1`:如果希望允許用戶在配置的不同值之間進行選擇，請使用此值。 在這種情況下，您還必須在 `/destination` 端點配置，以在UI中向用戶顯示各種選項。 請參閱 [此配置](#file-configuration-templating-pebble) 例如，用戶可以在不同的值之間為檔案格式選項進行選擇。</li></ul> | - | - | - |
| `compression.value` | 選填 | 將資料保存到檔案時使用的壓縮編解碼器。 支援的值： `none`。 `bzip2`。 `gzip`。 `lz4`, `snappy`。 | `none` | - | - |
| `fileType.value` | 選填 | 指定輸出檔案格式。 支援的值： `csv`。 `parquet`, `json`。 | `csv` | - | - |
| `csvOptions.quote.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 設定用於轉義引號值的單個字元，其中分隔符可以是該值的一部分。 | `null` | - | - |
| `csvOptions.quoteAll.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 指示是否應始終將所有值括在引號中。 預設值是僅轉義包含引號字元的值。 | `false` | `quoteAll`:`false` —> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 為每個欄位和值設定分隔符。 此分隔符可以是一個或多個字元。 | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 在已引用的值中設定用於逸出引號的單一字元。 | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 指示是否應始終將包含引號的值括在引號中。 預設值是轉義包含引號字元的所有值。 | `true` | - | - |
| `csvOptions.header.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 指示是否將列名作為導出檔案中的第一行寫入。 | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 指示是否從值修剪前導空格。 | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 指示是否從值中裁切尾隨空格。 | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 設定空值的字串表示形式。 | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 指示日期格式。 | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 設定指示時間戳格式的字串。 | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 設定用於轉義引號字元轉義的單個字元。 | `\` 轉義和引號字元不同時， `\0` 轉義字元和引號字元相同時。 | - | - |
| `csvOptions.emptyValue.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 設定空值的字串表示形式。 | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您應更好地瞭解檔案格式在目標伺服器配置中的工作方式，以及如何配置。

要瞭解有關其他目標伺服器元件的詳細資訊，請參閱以下文章：

* [使用Destination SDK建立的目標的伺服器規格](server-specs.md)
* [模板規格](templating-specs.md)
* [訊息格式](message-format.md)