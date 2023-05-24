---
description: 瞭解如何在Experience PlatformUI中建立輸入欄位，以便用戶指定與如何連接資料並將資料導出到目標相關的各種資訊。
title: 客戶資料欄位
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 2%

---


# 通過客戶資料欄位配置用戶輸入

在Experience PlatformUI中連接到目標時，可能需要您的用戶提供特定配置詳細資訊或選擇可供他們使用的特定選項。 在Destination SDK中，這些選項稱為客戶資料欄位。

要瞭解此元件在與Destination SDK建立的整合中的位置，請參閱 [配置選項](../configuration-options.md) 文檔，或參閱以下目標配置概述頁：

* [使用Destination SDK配置流目標](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

## 客戶資料欄位的使用案例 {#use-cases}

使用客戶資料欄位可用於需要用戶將資料輸入Experience PlatformUI的各種使用情形。 例如，當用戶需要提供以下內容時，請使用客戶資料欄位：

* 雲儲存儲存桶名稱和路徑，用於基於檔案的目標。
* 客戶資料欄位接受的格式。
* 用戶可以從中選擇的可用檔案壓縮類型。
* 用於即時（流式處理）整合的可用終結點清單。

您可以通過 `/authoring/destinations` 端點。 有關詳細的API調用示例，請參閱以下API參考頁，在這些示例中可以配置此頁中顯示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介紹可用於目標的所有受支援的客戶資料欄位配置類型，並顯示客戶將在Experience PlatformUI中看到哪些內容。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 支援的整合類型 {#supported-integration-types}

有關哪些類型的整合支援本頁所述功能的詳細資訊，請參閱下表。

| 整合類型 | 支援功能 |
|---|---|
| 即時（流）整合 | 是 |
| 基於檔案（批處理）的整合 | 是 |

## 支援的參數 {#supported-parameters}

在建立您自己的客戶資料欄位時，您可以使用下表中描述的參數來配置其行為。

| 參數 | 類型 | 必填/選填 | 說明 |
|---------|----------|------|---|
| `name` | 字串 | 必填 | 提供要引入的自定義欄位的名稱。 此名稱在平台UI中不可見，除非 `title` 欄位為空或缺失。 |
| `type` | 字串 | 必填 | 指示要引入的自定義欄位的類型。 接受的值： <ul><li>`string`</li><li>`object`</li><li>`integer`</li></ul> |
| `title` | 字串 | 選填 | 指示欄位的名稱，如客戶在平台UI中看到的。 如果此欄位為空或缺失，則UI將繼承 `name` 值。 |
| `description` | 字串 | 選填 | 提供自定義欄位的說明。 此說明在平台UI中不可見。 |
| `isRequired` | 布林值 | 選填 | 指示是否需要用戶在目標配置工作流中為此欄位提供值。 |
| `pattern` | 字串 | 選填 | 如果需要，為自定義欄位強制實施模式。 使用規則運算式來強制模式。 例如，如果客戶ID不包括數字或下划線，請輸入 `^[A-Za-z]+$` 的子菜單。 |
| `enum` | 字串 | 選填 | 將自定義欄位呈現為下拉菜單並列出用戶可用的選項。 |
| `default` | 字串 | 選填 | 從 `enum` 清單框。 |
| `hidden` | 布林值 | 選填 | 指示UI中是否顯示客戶資料欄位。 |
| `unique` | 布林值 | 選填 | 當您需要建立客戶資料欄位時，使用此參數，該欄位的值必須在用戶組織設定的所有目標資料流中唯一。 例如， **[!UICONTROL 整合別名]** 的 [自定義個性化](../../../catalog/personalization/custom-personalization.md) 目標必須唯一，這意味著到此目標的兩個單獨的資料流不能為此欄位具有相同的值。 |
| `readOnly` | 布林值 | 選填 | 指示客戶是否可以更改欄位的值。 |

{style="table-layout:auto"}

在下面的示例中， `customerDataFields` 部分定義了在連接到目標時用戶必須在平台UI中輸入的兩個欄位：

* `Account ID`:目標平台的用戶帳戶ID。
* `Endpoint region`:它們要連接的API的區域端點。 的 `enum` 部分將建立一個下拉菜單，其中定義了用戶可選擇的值。

```json
"customerDataFields":[
   {
      "name":"accountID",
      "title":"User account ID",
      "description":"User account ID for the destination platform.",
      "type":"string",
      "isRequired":true
   },
   {
      "name":"region",
      "title":"API endpoint region",
      "description":"The API endpoint region that the user should connect to.",
      "type":"string",
      "isRequired":true,
      "enum":[
         "EU"
         "US",
      ],
      "readOnly":false,
      "hidden":false
   }
]
```

生成的UI體驗顯示在下圖中。

![顯示客戶資料欄位示例的UI影像。](../../assets/functionality/destination-configuration/customer-data-fields-example.png)

## 目標連接名稱和說明 {#names-description}

建立新目標時，Destination SDK會自動添加 **[!UICONTROL 名稱]** 和 **[!UICONTROL 說明]** 欄位到平台UI中的目標連接螢幕。 如上例所示， **[!UICONTROL 名稱]** 和 **[!UICONTROL 說明]** 欄位將在UI中呈現，而不包括在客戶資料欄位配置中。

>[!IMPORTANT]
>
>如果添加 **[!UICONTROL 名稱]** 和 **[!UICONTROL 說明]** 配置中的欄位，用戶將在UI中看到這些欄位重複。

## 訂購客戶資料欄位 {#ordering}

在目標配置中添加客戶資料欄位的順序反映在平台UI中。

例如，下面的配置會相應地反映在UI中，選項按順序顯示 **[!UICONTROL 名稱]**。 **[!UICONTROL 說明]**。 **[!UICONTROL 儲存段名稱]**。 **[!UICONTROL 資料夾路徑]**。 **[!UICONTROL 檔案類型]**。 **[!UICONTROL 壓縮格式]**。

```json
"customerDataFields":[
{
   "name":"bucketName",
   "title":"Bucket name",
   "description":"Amazon S3 bucket name",
   "type":"string",
   "isRequired":true,
   "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
   "readOnly":false,
   "hidden":false
},
{
   "name":"path",
   "title":"Folder path",
   "description":"Enter the path to your S3 bucket folder",
   "type":"string",
   "isRequired":true,
   "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
   "readOnly":false,
   "hidden":false
},
{
   "name":"fileType",
   "title":"File Type",
   "description":"Select the exported file type.",
   "type":"string",
   "isRequired":true,
   "readOnly":false,
   "hidden":false,
   "enum":[
      "csv",
      "json",
      "parquet"
   ],
   "default":"csv"
},
{
   "name":"compression",
   "title":"Compression format",
   "description":"Select the desired file compression format.",
   "type":"string",
   "isRequired":true,
   "readOnly":false,
   "enum":[
      "SNAPPY",
      "GZIP",
      "DEFLATE",
      "NONE"
   ]
}
]
```

![顯示Experience PlatformUI中檔案格式選項順序的影像。](../../assets/functionality/destination-configuration/customer-data-fields-order.png)

## 將客戶資料欄位分組 {#grouping}

您可以在一個部分中對多個客戶資料欄位進行分組。 在UI中設定到目標的連接時，用戶可以看到類似欄位的可視分組並從中受益。

要執行此操作，請使用 `"type": "object"` 在 `properties` 對象，如下圖所示，其中分組 **[!UICONTROL CSV選項]** 的子菜單。

```json {line-numbers="true" highlight="6-28"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![該影像顯示UI中的客戶資料欄位分組。](../../assets/functionality/destination-configuration/group-customer-data-fields.png)

## 為客戶資料欄位建立下拉清單選擇器 {#dropdown-selectors}

對於希望允許用戶在多個選項之間進行選擇的情況，例如，應使用哪個字元來分隔CSV檔案中的欄位，可以向UI中添加下拉欄位。

要執行此操作，請使用 `namedEnum` 如下所示對象並配置 `default` 選項的值。

```json {line-numbers="true" highlight="15-24"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![螢幕錄制顯示了使用上面所示配置建立的下拉選擇器示例。](../../assets/functionality/destination-configuration/customer-data-fields-dropdown.gif)

## 建立條件客戶資料欄位 {#conditional-options}

您可以建立條件客戶資料欄位，這些欄位僅在用戶選擇特定選項時顯示在激活工作流中。

例如，您可以建立條件檔案格式選項，僅當用戶選擇特定檔案導出類型時才顯示。

以下配置為CSV檔案格式設定選項建立條件分組。 僅當用戶選擇CSV作為所需的檔案類型以進行導出時，才顯示CSV檔案選項。

要將欄位設定為條件，請使用 `conditional` 參數，如下所示：

```json
"conditional": {
   "field": "fileType",
   "operator": "EQUALS",
   "value": "CSV"
}
```

在更廣的上下文中，您可以 `conditional` 在下面的目標配置中使用的欄位 `fileType` 字串和 `csvOptions` 定義對象。

```json {line-numbers="true" highlight="3-15, 21-25"}
"customerDataFields":[
   {
      "name":"fileType",
      "title":"File Type",
      "description":"Select your file type",
      "type":"string",
      "isRequired":true,
      "enum":[
         "PARQUET",
         "CSV",
         "JSON"
      ],
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "conditional":{
         "field":"fileType",
         "operator":"EQUALS",
         "value":"CSV"
      },
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"quote",
            "title":"Quote Character",
            "description":"Select your Quote character",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Double Quotes (\")",
                  "value":"\""
               },
               {
                  "name":"Null Character (\u0000)",
                  "value":"\u0000"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"escape",
            "title":"Escape Character",
            "description":"Select your Escape character",
            "type":"string",
            "isRequired":false,
            "default":"\\",
            "namedEnum":[
               {
                  "name":"Back Slash (\\)",
                  "value":"\\"
               },
               {
                  "name":"Single Quote (')",
                  "value":"'"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"emptyValue",
            "title":"Empty Value",
            "description":"Select the output value of blank fields",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"nullValue",
            "title":"Null Value",
            "description":"Select the output value of 'null' fields",
            "type":"string",
            "isRequired":false,
            "default":"null",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ],
      "isRequired":false,
      "readOnly":false,
      "hidden":false
   }
]
```

在下面，您可以根據上述配置看到生成的UI螢幕。 當用戶選擇檔案類型CSV時，UI中將顯示引用CSV檔案類型的其他檔案格式選項。

![螢幕錄制顯示CSV檔案的條件檔案格式選項。](../../assets/functionality/destination-configuration/customer-data-fields-conditional.gif)

## 訪問模板化客戶資料欄位 {#accessing-templatized-fields}

當目標需要用戶輸入時，您必須向用戶提供一系列客戶資料欄位，用戶可通過平台UI填寫這些欄位。 然後，您必須配置目標伺服器以正確讀取客戶資料欄位中的用戶輸入。 這是通過模板化欄位完成的。

模板化欄位使用格式 `{{customerData.fieldName}}`，也請參見Wiki頁。 `fieldName` 是您正在從中讀取資訊的客戶資料欄位的名稱。 所有模板化客戶資料欄位前面都帶有 `customerData.` 在雙括弧內 `{{ }}`。

例如，讓我們考慮以下AmazonS3目標配置：

```json
"customerDataFields":[
   {
      "name":"bucketName",
      "title":"Enter the name of your Amazon S3 bucket",
      "description":"Amazon S3 bucket name",
      "type":"string",
      "isRequired":true,
      "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"path",
      "title":"Enter the path to your S3 bucket folder",
      "description":"Enter the path to your S3 bucket folder",
      "type":"string",
      "isRequired":true,
      "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
      "readOnly":false,
      "hidden":false
   }
]
```

此配置提示用戶輸入 [!DNL Amazon S3] 儲存段名稱和資料夾路徑進入各自的客戶資料欄位。

用於Experience Platform正確連接到 [!DNL Amazon S3]，必須將目標伺服器配置為從這兩個客戶資料欄位讀取值，如下所示：

```json
 "fileBasedS3Destination":{
      "bucketName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucketName}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
```

模板化值 `{{customerData.bucketName}}` 和 `{{customerData.path}}` 讀取用戶提供的值，以便Experience Platform可以成功連接到目標平台。

有關如何配置目標伺服器以讀取模板化欄位的詳細資訊，請參閱 [硬編碼與模板化場](../destination-server/server-specs.md#templatized-fields)。

## 後續步驟 {#next-steps}

閱讀本文後，您應該更好地瞭解如何允許用戶通過客戶資料欄位在Experience PlatformUI中輸入資訊。 您現在還知道如何為您的使用案例選擇正確的客戶資料欄位，以及在平台UI中配置、訂購和分組客戶資料欄位。

要瞭解有關其他目標元件的詳細資訊，請參閱以下文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2身份驗證](oauth2-authentication.md)
* [UI屬性](ui-attributes.md)
* [架構配置](schema-configuration.md)
* [標識命名空間配置](identity-namespace-configuration.md)
* [支援的映射配置](supported-mapping-configurations.md)
* [目標傳遞](destination-delivery.md)
* [受眾元資料配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批配置](batch-configuration.md)
* [歷史配置檔案資格](historical-profile-qualifications.md)