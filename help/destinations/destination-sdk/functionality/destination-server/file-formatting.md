---
description: 瞭解如何透過「/destination-servers」端點為以Adobe Experience Platform Destination SDK建立的檔案型目的地設定檔案格式選項。
title: 檔案格式設定
source-git-commit: 4f4ffc7fc6a895e529193431aba77d6f3dcafb6f
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 4%

---


# 檔案格式設定

Destination SDK支援一組彈性的功能，您可以根據整合需求進行設定。 其中一項功能是支援 [!DNL CSV] 檔案格式設定。

當您透過Destination SDK建立以檔案為基礎的目的地時，可以定義匯出的CSV檔案的格式設定。 您可以自訂許多格式選項，例如但不限於：

* CSV檔案是否應該包含標題；
* 引號值要使用的字元；
* 空值應該是什麼樣子。

視您的目的地設定而定，使用者在連線至檔案式目的地時，會在UI中看到某些選項。 您可以在以下連結中檢視這些選項的樣子 [檔案型目的地的檔案格式選項](../../../ui/batch-destinations-file-formatting-options.md) 檔案。


檔案格式設定是以檔案為基礎的目的地，屬於目的地伺服器組態的一部分。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱 [設定選項](../configuration-options.md) 檔案或請參閱操作說明指南 [使用Destination SDK來設定以檔案為基礎的目的地](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

您可以透過以下方式設定檔案格式選項 `/authoring/destination-servers` 端點。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面中顯示的元件。

* [建立目的地伺服器組態](../../authoring-api/destination-server/create-destination-server.md)
* [更新目的地伺服器設定](../../authoring-api/destination-server/update-destination-server.md)

本頁說明所有支援的匯出檔案格式設定 `CSV` 檔案。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值如下 **區分大小寫**. 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

如需瞭解哪些型別的整合支援本頁面所述功能的詳細資訊，請參閱下表。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 無 |
| 檔案式（批次）整合 | 是 |

## 支援的引數 {#supported-parameters}

您可以修改匯出檔案的數個屬性，以符合目的地檔案接收系統的需求，以最佳方式讀取和解譯從Experience Platform接收的檔案。

>[!NOTE]
>
>只有在匯出CSV檔案時才支援CSV選項。 此 `fileConfigurations` 區段在設定新的目的地伺服器時不是強制性的。 如果您沒有在API呼叫中為CSV選項傳遞任何值，預設值來自 [下方參考表格](#file-formatting-reference-and-example) 將會使用。


## 使用者無法選取組態選項的CSV選項 {#file-configuration-templating-none}

在以下的設定範例中，所有CSV選項皆為預先定義。 在每個 `csvOptions` 引數為最終引數，使用者無法加以修改。

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
        "maxFileRowCount":5000000,
        "includeFileManifest": {
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{ customerData.includeFileManifest }}"
      }
    }
```

## CSV選項，使用者可從中選取設定選項 {#file-configuration-templating-pebble}

在以下的設定範例中，並未預先定義任何CSV選項。 此 `value` 在每個 `csvOptions` 引數是透過在對應客戶資料欄位中設定 `/destinations` 端點(例如 [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) 針對 `quote` 檔案格式選項)，使用者可使用Experience PlatformUI在您於對應客戶資料欄位中設定的各種選項之間選取。 您可以在以下連結中檢視這些選項的樣子 [檔案型目的地的檔案格式選項](../../../ui/batch-destinations-file-formatting-options.md) 檔案。

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
      },
      "maxFileRowCount":5000000,
      "includeFileManifest": {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{ customerData.includeFileManifest }}"
      }
   }
}
```

## 支援的檔案格式選項完整參考和範例 {#file-formatting-reference-and-example}

>[!TIP]
>
>以下所述的CSV檔案格式選項也記錄在 [CSV檔案的Apache Spark指南](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). 以下使用的說明取自Apache Spark指南。

以下是Destination SDK中所有可用檔案格式選項的完整參考，連同每個選項的輸出範例。

| 欄位 | 必填/選填 | 說明 | 預設值 | 範例輸出1 | 範例輸出2 |
|---|---|---|---|---|---|
| `templatingStrategy` | 必要 | 對於您設定的每個檔案格式選項，您必須新增引數 `templatingStrategy`，其中可以有兩個值： <br><ul><li>`NONE`：如果您不打算允許使用者在設定的不同值之間選取，請使用此值。 另請參閱 [此設定](#file-configuration-templating-none) 例如，檔案格式選項固定的範例。</li><li>`PEBBLE_V1`：如果您希望允許使用者在設定的不同值之間選取，請使用此值。 在此情況下，您還必須在以下欄位中設定對應的客戶資料欄位： `/destination` 端點設定，在UI中向使用者呈現各種選項。 另請參閱 [此設定](#file-configuration-templating-pebble) 例如，使用者可以在不同的檔案格式選項值之間選取。</li></ul> | - | - | - |
| `compression.value` | 選填 | 將資料儲存至檔案時使用的壓縮轉碼器。 支援的值： `none`， `bzip2`， `gzip`， `lz4`、和 `snappy`. | `none` | - | - |
| `fileType.value` | 選填 | 指定輸出檔案格式。 支援的值： `csv`， `parquet`、和 `json`. | `csv` | - | - |
| `csvOptions.quote.value` | 選填 | *僅用於`"fileType.value": "csv"`*. 設定用於逸出引號值的單一字元，其中分隔符號可以是值的一部分。 | `null` | 預設值範例： `quote.value: "u0000"` —> `male,NULJohn,LastNameNUL` | 自訂範例： `quote.value: "\""` —> `male,"John,LastName"` |
| `csvOptions.quoteAll.value` | 選填 | *僅用於`"fileType.value": "csv"`*. 指示是否所有值都一律以引號括住。 預設為僅逸出包含引號字元的值。 | `false` | `quoteAll`：`false` —> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | 選填 | *僅用於`"fileType.value": "csv"`*. 為每個欄位和值設定分隔符號。 此分隔符號可為一或多個字元。 | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | 選填 | *僅用於`"fileType.value": "csv"`*. 在已引用的值中設定用於逸出引號的單一字元。 | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | 選填 | *僅用於`"fileType.value": "csv"`*. 指示是否一律將包含引號的值括在引號中。 預設為逸出包含引號字元的所有值。 | `true` | - | - |
| `csvOptions.header.value` | 選填 | *僅用於`"fileType.value": "csv"`*. 指示是否將欄名稱寫入匯出檔案的第一行。 | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | 選填 | *僅用於`"fileType.value": "csv"`*. 指示是否從值中修剪前導空格。 | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | 選填 | *僅用於`"fileType.value": "csv"`*. 指示是否從值修剪尾端空格。 | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | 選填 | *僅用於`"fileType.value": "csv"`*. 設定null值的字串表示。 | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | 選填 | *僅用於`"fileType.value": "csv"`*. 指示日期格式。 | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | 選填 | *僅用於`"fileType.value": "csv"`*. 設定表示時間戳記格式的字串。 | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | 選填 | *僅用於`"fileType.value": "csv"`*. 設定用於逸出引號字元的單一字元。 | `\` 當逸出和引號字元不同時。 `\0` 當逸出和引號字元相同時。 | - | - |
| `csvOptions.emptyValue.value` | 選填 | *僅用於`"fileType.value": "csv"`*. 設定空值的字串表示。 | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |
| `maxFileRowCount` | 選填 | 表示每個匯出檔案的最大列數，介於1,000,000到10,000,000列之間。 | 5,000,000 |
| `includeFileManifest` | 選填 | 啟用匯出檔案資訊清單與檔案匯出的支援。 資訊清單JSON檔案包含有關匯出位置、匯出大小等的資訊。 資訊清單的命名格式為 `manifest-<<destinationId>>-<<dataflowRunId>>.json`. | 檢視 [範例資訊清單檔案](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). 資訊清單檔案包含下列欄位： <ul><li>`flowRunId`：此 [資料流執行](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 產生匯出的檔案。</li><li>`scheduledTime`：檔案匯出的時間(UTC)。 </li><li>`exportResults.sinkPath`：儲存已匯出檔案所在儲存位置的路徑。 </li><li>`exportResults.name`：匯出的檔案名稱。</li><li>`size`：匯出的檔案大小，以位元組為單位。</li></ul> |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您應該更瞭解檔案格式設定在目標伺服器設定中的運作方式，以及如何進行設定。

若要深入瞭解其他目的地伺服器元件，請參閱下列文章：

* [以Destination SDK建立的目的地的伺服器規格](server-specs.md)
* [範本規格](templating-specs.md)
* [訊息格式](message-format.md)