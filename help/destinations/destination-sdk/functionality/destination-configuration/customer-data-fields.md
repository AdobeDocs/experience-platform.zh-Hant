---
description: 了解如何在Experience PlatformUI中建立輸入欄位，讓使用者能指定與如何連線及將資料匯出至目的地相關的各種資訊。
title: 客戶資料欄位
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 2%

---


# 透過客戶資料欄位設定使用者輸入

在Experience PlatformUI中連線至目的地時，您可能需要您的使用者提供特定的設定詳細資訊，或選取您提供給他們的特定選項。 在Destination SDK中，這些選項稱為客戶資料欄位。

若要了解此元件在透過Destination SDK建立的整合中的插入位置，請參閱 [配置選項](../configuration-options.md) 檔案或請參閱下列目的地組態概觀頁面：

* [使用Destination SDK來設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

## 客戶資料欄位的使用案例 {#use-cases}

在您需要使用者將資料輸入Experience PlatformUI的各種使用案例中，請使用客戶資料欄位。 例如，當使用者需要提供以下項目時，請使用客戶資料欄位：

* 適用於檔案型目的地的雲端儲存貯體名稱和路徑。
* 客戶資料欄位接受的格式。
* 用戶可以選擇的可用檔案壓縮類型。
* 即時（串流）整合的可用端點清單。

您可以透過 `/authoring/destinations` 端點。 如需詳細API呼叫範例，請參閱下列API參考頁面，您可在其中設定本頁面所示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文說明您可用於目的地的所有支援客戶資料欄位設定類型，並顯示客戶在Experience PlatformUI中會看到什麼內容。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 支援的整合類型 {#supported-integration-types}

如需詳細資訊，請參閱下表以了解哪些類型的整合支援本頁面所述的功能。

| 整合類型 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 支援的參數 {#supported-parameters}

建立您自己的客戶資料欄位時，您可以使用下表中所述的參數來設定其行為。

| 參數 | 類型 | 必填/選填 | 說明 |
|---------|----------|------|---|
| `name` | 字串 | 必填 | 提供您要引入的自訂欄位名稱。 此名稱不會顯示在Platform UI中，除非 `title` 欄位為空或缺少。 |
| `type` | 字串 | 必填 | 指出您要引入的自訂欄位類型。 接受的值： <ul><li>`string`</li><li>`object`</li><li>`integer`</li></ul> |
| `title` | 字串 | 選填 | 指出欄位的名稱，如Platform UI中的客戶所見。 如果此欄位為空或遺失，UI會繼承 `name` 值。 |
| `description` | 字串 | 選填 | 提供自訂欄位的說明。 平台UI中不會顯示此說明。 |
| `isRequired` | 布林值 | 選填 | 指示在目標配置工作流中是否需要用戶為此欄位提供值。 |
| `pattern` | 字串 | 選填 | 視需要為自訂欄位強制使用模式。 使用規則運算式來強制模式。 例如，若您的客戶ID未包含數字或底線，請輸入 `^[A-Za-z]+$` 在此欄位中。 |
| `enum` | 字串 | 選填 | 將自訂欄位轉譯為下拉式功能表，並列出使用者可用的選項。 |
| `default` | 字串 | 選填 | 從 `enum` 清單。 |
| `hidden` | 布林值 | 選填 | 指出UI中是否顯示客戶資料欄位。 |
| `unique` | 布林值 | 選填 | 當您需要建立客戶資料欄位時，使用此參數，該欄位的值必須在用戶組織設定的所有目標資料流中是唯一的。 例如， **[!UICONTROL 整合別名]** 欄位 [自訂個人化](../../../catalog/personalization/custom-personalization.md) 目標必須是唯一的，這表示到此目標的兩個單獨的資料流不能具有此欄位的相同值。 |
| `readOnly` | 布林值 | 選填 | 指出客戶是否可變更欄位的值。 |

{style="table-layout:auto"}

在以下範例中， `customerDataFields` 區段定義使用者連線至目的地時，必須在Platform UI中輸入的兩個欄位：

* `Account ID`:目的地平台的使用者帳戶ID。
* `Endpoint region`:他們將連線至的API地區端點。 此 `enum` 區段會建立下拉式功能表，其中所定義的值可供使用者選取。

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

產生的UI體驗會顯示在下圖中。

![顯示客戶資料欄位範例的UI影像。](../../assets/functionality/destination-configuration/customer-data-fields-example.png)

## 目標連接名稱和說明 {#names-description}

建立新目的地時，Destination SDK會自動新增 **[!UICONTROL 名稱]** 和 **[!UICONTROL 說明]** Platform UI中的「目標連線」畫面欄位。 如上例所示， **[!UICONTROL 名稱]** 和 **[!UICONTROL 說明]** 欄位會在UI中呈現，而不會包含在客戶資料欄位設定中。

>[!IMPORTANT]
>
>如果您新增 **[!UICONTROL 名稱]** 和 **[!UICONTROL 說明]** 欄位設定中，使用者會在UI中看到重複的欄位。

## 訂購客戶資料欄位 {#ordering}

在目的地設定中新增客戶資料欄位的順序會反映在Platform UI中。

例如，UI會相應反映下列設定，並依順序顯示選項 **[!UICONTROL 名稱]**, **[!UICONTROL 說明]**, **[!UICONTROL 貯體名稱]**, **[!UICONTROL 資料夾路徑]**, **[!UICONTROL 檔案類型]**, **[!UICONTROL 壓縮格式]**.

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

您可以在一個區段內將多個客戶資料欄位分組。 在UI中設定與目的地的連線時，使用者可以看到類似欄位的視覺化分組，並從中獲益。

若要這麼做，請使用 `"type": "object"` 若要建立群組，並收集 `properties` 物件，如下圖所示，其中分組 **[!UICONTROL CSV選項]** 會加亮顯示。

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

![影像顯示UI中客戶資料欄位分組。](../../assets/functionality/destination-configuration/group-customer-data-fields.png)

## 為客戶資料欄位建立下拉式選取器 {#dropdown-selectors}

若您想要讓使用者在多個選項之間進行選取（例如應使用哪個字元來分隔CSV檔案中的欄位），您可以將下拉式清單欄位新增至UI。

若要這麼做，請使用 `namedEnum` 物件，如下所示，並設定 `default` 值，供使用者選取。

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

![螢幕記錄顯示以上所示組態建立的下拉式選取器範例。](../../assets/functionality/destination-configuration/customer-data-fields-dropdown.gif)

## 建立條件式客戶資料欄位 {#conditional-options}

您可以建立條件式客戶資料欄位，這些欄位只會在使用者選取特定選項時，才會顯示在啟動工作流程中。

例如，您可以建立條件式檔案格式選項，這些選項僅在用戶選擇特定的檔案導出類型時顯示。

以下設定會為CSV檔案格式選項建立條件式分組。 只有當使用者選取CSV作為要匯出的檔案類型時，才會顯示CSV檔案選項。

若要將欄位設為條件式，請使用 `conditional` 參數，如下所示：

```json
"conditional": {
   "field": "fileType",
   "operator": "EQUALS",
   "value": "CSV"
}
```

在更廣泛的情境中，您可以看到 `conditional` 欄位(與 `fileType` 字串和 `csvOptions` 定義對象的對象。

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

在下方，您可以根據上述設定，查看產生的UI畫面。 當使用者選取檔案類型CSV時，UI中會顯示引用CSV檔案類型的其他檔案格式選項。

![螢幕記錄，顯示CSV檔案的條件式檔案格式選項。](../../assets/functionality/destination-configuration/customer-data-fields-conditional.gif)

## 存取範本化客戶資料欄位 {#accessing-templatized-fields}

當您的目的地需要使用者輸入內容時，您必須為使用者提供客戶資料欄位的選取項目，使用者可透過Platform UI填寫這些欄位。 然後，您必須設定目標伺服器，才能從客戶資料欄位正確讀取使用者輸入。 這可透過範本欄位完成。

範本化欄位使用格式 `{{customerData.fieldName}}`，其中 `fieldName` 是您要從中讀取資訊的客戶資料欄位的名稱。 所有範本化客戶資料欄位前面都有 `customerData.` 雙括弧內 `{{ }}`.

例如，請考量下列Amazon S3目的地設定：

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

此設定會提示您的使用者輸入 [!DNL Amazon S3] 貯體名稱和資料夾路徑，放入其個別的客戶資料欄位。

若要讓Experience Platform正確連線至 [!DNL Amazon S3]，您的目的地伺服器必須設定為從這兩個客戶資料欄位讀取值，如下所示：

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

範本化值 `{{customerData.bucketName}}` 和 `{{customerData.path}}` 讀取使用者提供的值，讓Experience Platform能成功連線至目的地平台。

如需如何將目標伺服器設定為讀取範本欄位的詳細資訊，請參閱 [硬式編碼與範本化欄位](../destination-server/server-specs.md#templatized-fields).

## 後續步驟 {#next-steps}

閱讀本文後，您應該更了解如何讓使用者透過Experience Platform資料欄位，在客戶UI中輸入資訊。 您現在也知道如何為您的使用案例選取正確的客戶資料欄位，以及在Platform UI中設定、排序和分組客戶資料欄位。

若要進一步了解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [UI屬性](ui-attributes.md)
* [結構配置](schema-configuration.md)
* [身分命名空間設定](identity-namespace-configuration.md)
* [支援的對應配置](supported-mapping-configurations.md)
* [目的地傳送](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)