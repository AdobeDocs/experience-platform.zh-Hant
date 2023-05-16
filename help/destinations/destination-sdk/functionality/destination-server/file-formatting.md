---
description: 了解如何透過「/destination-servers」端點，為以Adobe Experience Platform Destination SDK建置的檔案式目的地設定檔案格式選項。
title: 檔案格式設定
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 4%

---


# 檔案格式設定

Destination SDK支援一組彈性的功能，您可以根據整合需求進行設定。 這些功能包括 [!DNL CSV] 檔案格式。

透過Destination SDK建立檔案式目的地時，您可以定義匯出CSV檔案的格式。 您可以自訂許多格式選項，例如，但不限於：

* CSV檔案是否應包含標題；
* 用於引號值的字元；
* 空值應該是什麼樣子。

根據您的目的地設定，使用者在連線至檔案式目的地時，會在UI中看到特定選項。 您可以在 [基於檔案的目的地的檔案格式選項](../../../ui/batch-destinations-file-formatting-options.md) 檔案。


檔案格式設定是檔案型目的地的目的地伺服器設定的一部分。

若要了解此元件在透過Destination SDK建立的整合中的插入位置，請參閱 [配置選項](../configuration-options.md) 檔案，或參閱如何 [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

您可以透過 `/authoring/destination-servers` 端點。 如需詳細API呼叫範例，請參閱下列API參考頁面，您可在其中設定本頁面所示的元件。

* [建立目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)
* [更新目標伺服器配置](../../authoring-api/destination-server/update-destination-server.md)

本頁面說明所有支援的檔案格式設定，以供匯出 `CSV` 檔案。

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

您可以修改導出檔案的多個屬性以符合目標的檔案接收系統的要求，以便以最佳方式讀取和解釋從Experience Platform接收的檔案。

>[!NOTE]
>
>只有匯出CSV檔案時，才支援CSV選項。 此 `fileConfigurations` 設定新的目標伺服器時，區段不是必填欄位。 如果您未在CSV選項的API呼叫中傳遞任何值，則會是 [下文](#file-formatting-reference-and-example) 中指定的規則。


## CSV選項，使用者無法選取設定選項 {#file-configuration-templating-none}

在以下的設定範例中，所有CSV選項皆預先定義。 每個 `csvOptions` 參數為最終參數，用戶無法修改參數。

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

## CSV選項，讓使用者可以選取設定選項 {#file-configuration-templating-pebble}

在下列設定範例中，未預先定義任何CSV選項。 此 `value` 在 `csvOptions` 參數會透過 `/destinations` 例如 [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) 針對 `quote` 檔案格式選項)，而使用者可以使用「Experience PlatformUI」，在您在對應客戶資料欄位中設定的各種選項之間進行選取。 您可以在 [基於檔案的目的地的檔案格式選項](../../../ui/batch-destinations-file-formatting-options.md) 檔案。

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

## 支援的檔案格式選項的完整參考資料和範例 {#file-formatting-reference-and-example}

>[!TIP]
>
>以下所述的CSV檔案格式選項也記錄在 [適用於CSV檔案的Apache Spark指南](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). 以下說明取自Apache Spark指南。

以下是Destination SDK中所有可用檔案格式選項的完整參考，以及每個選項的輸出範例。

| 欄位 | 必填/選填 | 說明 | 預設值 | 範例輸出1 | 範例輸出2 |
|---|---|---|---|---|---|
| `templatingStrategy` | 必填 | 針對您設定的每個檔案格式選項，您必須新增參數 `templatingStrategy`，其中可以有兩個值： <br><ul><li>`NONE`:如果您不打算讓使用者為設定在不同值之間進行選取，請使用此值。 請參閱 [此配置](#file-configuration-templating-none) 例如，檔案格式選項已修正。</li><li>`PEBBLE_V1`:如果您想要讓使用者為設定在不同值之間進行選取，請使用此值。 在此情況下，您也必須在 `/destination` 端點設定，在UI中向使用者顯示各種選項。 請參閱 [此配置](#file-configuration-templating-pebble) 例如，使用者可以為檔案格式選項在不同值之間進行選取。</li></ul> | - | - | - |
| `compression.value` | 選填 | 在將資料保存到檔案時使用的壓縮編解碼器。 支援的值： `none`, `bzip2`, `gzip`, `lz4`，和 `snappy`. | `none` | - | - |
| `fileType.value` | 選填 | 指定輸出檔案格式。 支援的值： `csv`, `parquet`，和 `json`. | `csv` | - | - |
| `csvOptions.quote.value` | 選填 | *僅限`"fileType.value": "csv"`*. 設定用於逸出引號值的單一字元，其中分隔符可以是值的一部分。 | `null` | - | - |
| `csvOptions.quoteAll.value` | 選填 | *僅限`"fileType.value": "csv"`*. 指示是否應始終以引號括住所有值。 預設值為僅逸出包含引號字元的值。 | `false` | `quoteAll`:`false` —> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | 選填 | *僅限`"fileType.value": "csv"`*. 為每個欄位和值設定分隔符號。 此分隔符號可以是一或多個字元。 | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | 選填 | *僅限`"fileType.value": "csv"`*. 在已引用的值中設定用於逸出引號的單一字元。 | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | 選填 | *僅限`"fileType.value": "csv"`*. 指示是否應始終將包含引號的值括在引號中。 預設值是逸出包含引號字元的所有值。 | `true` | - | - |
| `csvOptions.header.value` | 選填 | *僅限`"fileType.value": "csv"`*. 指示是否將列的名稱寫入導出檔案中的第一行。 | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | 選填 | *僅限`"fileType.value": "csv"`*. 指示是否從值中修剪前導空格。 | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | 選填 | *僅限`"fileType.value": "csv"`*. 指示是否從值修剪尾隨空格。 | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | 選填 | *僅限`"fileType.value": "csv"`*. 設定空值的字串表示。 | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | 選填 | *僅限`"fileType.value": "csv"`*. 指出日期格式。 | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | 選填 | *僅限`"fileType.value": "csv"`*. 設定指示時間戳格式的字串。 | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | 選填 | *僅限`"fileType.value": "csv"`*. 設定用於逸出引號字元的逸出的單一字元。 | `\` 當逸出字元和引號字元不同時。 `\0` 引號和轉義字元相同時，就會顯示此變數。 | - | - |
| `csvOptions.emptyValue.value` | 選填 | *僅限`"fileType.value": "csv"`*. 設定空值的字串表示。 | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您應該更清楚了解檔案格式設定在目標伺服器設定中的運作方式，以及如何設定。

若要進一步了解其他目標伺服器元件，請參閱下列文章：

* [使用Destination SDK建立的目的地的伺服器規格](server-specs.md)
* [模板規格](templating-specs.md)
* [訊息格式](message-format.md)