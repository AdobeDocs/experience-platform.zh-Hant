---
description: 此配置允許您指明基本資訊，如目標名稱、類別、說明、徽標等。 此配置中的設定還確定Experience Platform用戶如何驗證到目標、Experience Platform用戶介面中的顯示方式以及可以導出到目標的身份。
title: （測試版）基於檔案的目標配置選項，用於Destination SDK
exl-id: 6b0a0398-6392-470a-bb27-5b34b0062793
source-git-commit: 301cef53644e813c3fd43e7f2dbaf730c9e5fc11
workflow-type: tm+mt
source-wordcount: '2330'
ht-degree: 5%

---

# （測試版）基於檔案的目標配置 {#destination-configuration}

## 總覽 {#overview}

>[!IMPORTANT]
>
>Adobe Experience Platform Destination SDK中基於檔案的目標支援當前處於測試版中。 文檔和功能可能會更改。

此配置允許您指示基於檔案的目標的基本資訊，如目標名稱、類別、說明等。 此配置中的設定還確定Experience Platform用戶如何驗證到目標、Experience Platform用戶介面中的顯示方式以及可以導出到目標的身份。

此配置還將目標工作所需的其他配置（目標伺服器和受眾元資料）連接到此配置。 閱讀如何在 [下](./destination-configuration.md#connecting-all-configurations)。

您可以使用 `/authoring/destinations` API終結點。 閱讀 [目標API終結點操作](./destination-configuration-api.md) 可在端點上執行的操作的完整清單。

## AmazonS3目標配置示例 {#batch-example-configuration}

```json
{
   "name":"S3 Destination with CSV Options",
   "description":"S3 Destination with CSV Options",
   "status":"TEST",
   "maxProfileAttributes":"2000",
   "maxIdentityAttributes":"10",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
      
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"header",
         "description":"Writes the names of columns as the first line.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"Select a fileType",
         "description":"Select fileType",
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
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   },
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ],
   "identityNamespaces":{
      "adobe_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "mobile_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"phoneNo",
            "title":"phoneNo",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
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
      "backfillHistoricalProfileData":true
   }
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `name` | 字串 | 指示Experience Platform目錄中目標的標題。 |
| `description` | 字串 | 在Experience Platform目標目錄中提供目標卡的說明。 目標不超過4-5句。 |
| `status` | 字串 | 指示目標卡的生命週期狀態。 接受的值為 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 在首次配置目標時。 |
| `maxProfileAttributes` | 字串 | 指示客戶可導出到目標的配置檔案屬性的最大數量。 預設值為 `2000`。 |
| `maxIdentityAttributes` | 字串 | 指示客戶可導出到目標的標識命名空間的最大數量。 預設值為 `10`。 |

{style=&quot;table-layout:auto&quot;}

## 客戶驗證配置 {#customer-authentication-configurations}

目標配置中的此部分將生成 [配置新目標](/help/destinations/ui/connect-destination.md) Experience Platform用戶介面中的「Experience Platform」頁，其中用戶將連接到他們與目標的帳戶。

```json
"customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
```

取決於 [驗證選項](authentication-configuration.md##supported-authentication-types) 在 `authType` 欄位中，將為用戶生成Experience Platform頁，如下所示：

### AmazonS3驗證 {#s3}

配置AmazonS3身份驗證類型時，用戶需要輸入S3憑據。

![使用S3身份驗證的UI呈現](assets/s3-authentication-ui.png)

### Azure Blob身份驗證  {#blob}

配置Azure Blob身份驗證類型時，用戶需要輸入連接字串。

![UI呈現與Blob身份驗證](assets/blob-authentication-ui.png)

### 具有密碼驗證的SFTP

使用密碼驗證類型配置SFTP時，用戶需要輸入SFTP用戶名和密碼以及SFTP域和埠（預設埠為22）。

![UI呈現，SFTP帶密碼驗證](assets/sftp-password-authentication-ui.png)

### SFTP與SSH密鑰驗證

使用SSH密鑰驗證類型配置SFTP時，用戶需要輸入SFTP用戶名和SSH密鑰，以及SFTP域和埠（預設埠為22）。

![UI呈現，SFTP帶SSH密鑰驗證](assets/sftp-key-authentication-ui.png)

## 客戶資料欄位 {#customer-data-fields}

使用此部分可在連接到Experience PlatformUI中的目標時要求用戶填寫特定於目標的自定義欄位。

在下面的示例中， `customerDataFields` 要求用戶輸入其目標的名稱，並提供 [!DNL Amazon S3] 儲存段名稱和資料夾路徑，以及壓縮類型、檔案格式和多個其他檔案導出選項。

```json
 "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"header",
         "description":"Writes the names of columns as the first line.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"Select a fileType",
         "description":"Select fileType",
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
      }
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `name` | 字串 | 提供要引入的自定義欄位的名稱。 |
| `title` | 字串 | 指示欄位的名稱，如客戶在Experience Platform用戶介面中看到的。 |
| `description` | 字串 | 提供自定義欄位的說明。 |
| `type` | 字串 | 指示您要引入的自定義欄位類型。 接受的值為 `string`。 `object`。 `integer`。 |
| `isRequired` | 布林值 | 指示目標設定工作流中是否需要此欄位。 |
| `pattern` | 字串 | 如果需要，為自定義欄位強制實施模式。 使用規則運算式來強制模式。 例如，如果客戶ID不包括數字或下划線，請輸入 `^[A-Za-z]+$` 的子菜單。 |
| `enum` | 字串 | 將自定義欄位呈現為下拉菜單並列出用戶可用的選項。 |
| `default` | 字串 | 從 `enum` 清單框。 |

{style=&quot;table-layout:auto&quot;&quot;

## UI屬性 {#ui-attributes}

本節指上述配置中的UI元素，該Adobe應用於Adobe Experience Platform用戶介面中的目標。

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   }
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `documentationLink` | 字串 | 引用中的文檔頁面 [目標目錄](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `http://www.adobe.com/go/destinations-YOURDESTINATION-en`，也請參見Wiki頁。 `YOURDESTINATION` 是目標的名稱。 對於名為Moviestar的目標，您將使用 `http://www.adobe.com/go/destinations-moviestar-en`。 請注意，此連結僅在Adobe設定目標即時並發佈文檔後才起作用。 |
| `category` | 字串 | 指分配給您在Adobe Experience Platform的目標的類別。 有關詳細資訊，請閱讀 [目標類別](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html)。 使用以下值之一： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`。 |
| `iconUrl` | 字串 | 承載要顯示在目標目錄卡中的表徵圖的URL。 |
| `connectionType` | 字串 | 連接類型（取決於目標）。 支援的值： <ul><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li></ul> |
| `flowRunsSupported` | 布林值 | 指示目標連接是否包含在 [流運行UI](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard)。 將此設定為 `true`: <ul><li>的 **[!UICONTROL 上次資料流運行日期]** 和 **[!UICONTROL 上次資料流運行狀態]** 顯示在目標瀏覽頁中。</li><li>的 **[!UICONTROL 資料流運行]** 和 **[!UICONTROL 激活資料]** 頁籤顯示在目標視圖頁中。</li></ul> |
| `monitoringSupported` | 布林值 | 指示目標連接是否包含在 [監視UI](../ui/destinations-workspace.md#browse)。 將此設定為 `true`，也請參見Wiki頁。 **[!UICONTROL 在監視中查看]** 選項。 |
| `frequency` | 字串 | 引用目標支援的資料導出類型。 設定為 `Batch` 用於基於檔案的目標。 |

{style=&quot;table-layout:auto&quot;&quot;

## 目標傳遞 {#destination-delivery}

```json
 "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `authenticationRule` | 字串 | 指示如何 [!DNL Platform] 客戶連接到您的目標。 接受的值為 `CUSTOMER_AUTHENTICATION`。 `PLATFORM_AUTHENTICATION`。 `NONE`。 <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果平台客戶通過以下任何方法登錄到您的系統： <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe與目標之間有全局身份驗證系統， [!DNL Platform] 客戶不需要提供任何身份驗證憑據來連接到目標。 在這種情況下，必須使用 [憑據](./credentials-configuration-api.md) 配置。 </li><li>使用 `NONE` 如果向目標平台發送資料不需要身份驗證。 </li></ul> |
| `destinationServerId` | 字串 | 的 `instanceId` 的 [目標伺服器配置](./destination-server-api.md) 用於此目標。 |

{style=&quot;table-layout:auto&quot;&quot;

## 段映射配置 {#segment-mapping}

目標配置的這一部分涉及段元資料（如段名稱或ID）在Experience Platform與目標之間應如何共用。

通過 `audienceTemplateId`，本節還將此配置與 [觀眾元資料配置](./audience-metadata-management.md)。

```json
   "segmentMappingConfig":{
       "mapExperiencePlatformSegmentName":false,
       "mapExperiencePlatformSegmentId":false,
       "mapUserInput":false,
       "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | 布林值 | 控制目標激活工作流中的段映射id是否是Experience Platform段名稱。 |
| `mapExperiencePlatformSegmentId` | 布林值 | 控制目標激活工作流中的段映射ID是否是Experience Platform段ID。 |
| `mapUserInput` | 布林值 | 控制用戶是否輸入目標激活工作流中的段映射ID。 |
| `audienceTemplateId` | 布林值 | 的 `instanceId` 的 [受眾元資料模板](./audience-metadata-management.md) 用於此目標。 要設定受眾元資料模板，請閱讀 [受眾元資料API參考](./audience-metadata-api.md)。 |

## 映射步驟中的架構配置 {#schema-configuration}

使用中的參數 `schemaConfig` 啟用目標激活工作流的映射步驟。 通過使用下面描述的參數，您可以確定Experience Platform用戶是否可以將配置檔案屬性和/或標識映射到基於檔案的目標。

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `profileFields` | 陣列 | 添加預定義項時 `profileFields`,Experience Platform用戶可以選擇將平台屬性映射到目標中的預定義屬性。 |
| `profileRequired` | 布林值 | 使用 `true` 如果用戶應能將配置檔案屬性從Experience Platform映射到目標側的自定義屬性，如上面的示例配置所示。 |
| `segmentRequired` | 布林值 | 始終使用 `segmentRequired:true`。 |
| `identityRequired` | 布林值 | 使用 `true` 如果用戶應能將標識命名空間從Experience Platform映射到所需的架構。 |

{style=&quot;table-layout:auto&quot;&quot;

### 映射步驟中的動態架構配置 {#dynamic-schema-configuration}

Adobe Experience Platform Destination SDK支援夥伴定義的架構。 合作夥伴定義的架構允許用戶將配置檔案屬性和標識映射到由目標合作夥伴定義的自定義架構，類似於 [流目標](destination-configuration.md#schema-configuration) 工作流。

使用中的參數  `dynamicSchemaConfig` 定義平台配置檔案屬性和/或標識可以映射到的您自己的架構。

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `profileRequired` | 布林值 | 使用 `true` 如果用戶應能將配置檔案屬性從Experience Platform映射到目標側的自定義屬性，如上面的示例配置所示。 |
| `segmentRequired` | 布林值 | 始終使用 `segmentRequired:true`。 |
| `identityRequired` | 布林值 | 使用 `true` 如果用戶應能將標識命名空間從Experience Platform映射到所需的架構。 |
| `destinationServerId` | 字串 | 的 `instanceId` 的 [目標伺服器配置](./destination-server-api.md) 用於此目標。 |
| `authenticationRule` | 字串 | 指示如何 [!DNL Platform] 客戶連接到您的目標。 接受的值為 `CUSTOMER_AUTHENTICATION`。 `PLATFORM_AUTHENTICATION`。 `NONE`。 <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果平台客戶通過以下任何方法登錄到您的系統： <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe與目標之間有全局身份驗證系統， [!DNL Platform] 客戶不需要提供任何身份驗證憑據來連接到目標。 在這種情況下，必須使用 [憑據](./credentials-configuration-api.md) 配置。 </li><li>使用 `NONE` 如果向目標平台發送資料不需要身份驗證。 </li></ul> |
| `value` | 字串 | 要在Experience Platform用戶介面中顯示的映射步驟中的架構的名稱。 |
| `responseFormat` | 字串 | 始終設定為 `SCHEMA` 定義自定義架構時。 |

{style=&quot;table-layout:auto&quot;&quot;

## 標識和屬性 {#identities-and-attributes}

本節中的參數確定目標接受的標識。 此配置還填充中的目標標識和屬性 [映射步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) Experience Platform用戶介面中，用戶將標識和屬性從其XDM架構映射到目標中的架構。


```json
"identityNamespaces": {
        "adobe_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        }
    },
```

必須指明 [!DNL Platform] 標識客戶能夠導出到您的目標。 一些示例 [!DNL Experience Cloud ID]，散列電子郵件，設備ID([!DNL IDFA]。 [!DNL GAID])。 這些值 [!DNL Platform] 客戶可以從目標映射到標識命名空間的標識命名空間。 您還可以指示客戶是否可以將自定義命名空間映射到目標支援的標識。

標識命名空間不需要在 [!DNL Platform] 和你的目的地。
例如，客戶可以 [!DNL Platform] [!DNL IDFA] 命名空間到 [!DNL IDFA] 命名空間，或者它們可以映射 [!DNL Platform] [!DNL IDFA] 命名空間到 [!DNL Customer ID] 目標中的命名空間。

## 批配置 {#batch-configuration}

本節指上述配置中的檔案導出設定，該Adobe應用於Adobe Experience Platform用戶介面中的目標。

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
| `allowMandatoryFieldSelection` | 布林值 | 設定為 `true` 允許客戶指定哪些配置檔案屬性是必需的。 預設值為 `false`。請參閱 [必需屬性](../ui/activate-batch-profile-destinations.md#mandatory-attributes) 的子菜單。 |
| `allowDedupeKeyFieldSelection` | 布林值 | 設定為 `true` 允許客戶指定重複資料消除密鑰。 預設值為 `false`。請參閱 [重複資料消除密鑰](../ui/activate-batch-profile-destinations.md#deduplication-keys) 的子菜單。 |
| `defaultExportMode` | 枚舉 | 定義預設檔案導出模式。 支援的值：<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> 預設值為 `DAILY_FULL_EXPORT`。查看 [批量激活文檔](../ui/activate-batch-profile-destinations.md#scheduling) 的子菜單。 |
| `allowedExportModes` | 清單 | 定義客戶可用的檔案導出模式。 支援的值：<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | 清單 | 定義客戶可用的檔案導出頻率。 支援的值：<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | 枚舉 | 定義預設檔案導出頻率。支援的值：<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> 預設值為 `DAILY`。 |
| `defaultStartTime` | 字串 | 定義檔案導出的預設開始時間。 使用24小時檔案格式。 預設值為「00:00」。 |
| `filenameConfig.allowedFilenameAppendOptions` | 字串 | *必填*. 可供用戶選擇的可用檔案名宏清單。 這確定將哪些項附加到導出的檔案名（段ID、組織名稱、導出日期和時間等）。 設定時 `defaultFilename`，確保避免複製宏。 <br><br>支援的值： <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>無論宏的定義順序如何，Experience PlatformUI始終按此處顯示的順序顯示宏。 <br><br> 如果 `defaultFilename` 是空的， `allowedFilenameAppendOptions` 清單必須至少包含一個宏。 |
| `filenameConfig.defaultFilenameAppendOptions` | 字串 | *必填*. 用戶可以取消選中的預選預設檔案名宏。<br><br> 此清單中的宏是中定義的宏的子集 `allowedFilenameAppendOptions`。 |
| `filenameConfig.defaultFilename` | 字串 | *可選*. 定義導出檔案的預設檔案名宏。 用戶無法覆蓋這些內容。 <br><br>由定義的任何宏 `allowedFilenameAppendOptions` 將在 `defaultFilename` 宏。 <br><br>如果 `defaultFilename` 為空，您必須在 `allowedFilenameAppendOptions`。 |

{style=&quot;table-layout:auto&quot;&quot;

### 檔案名配置 {#file-name-configuration}

使用檔案名配置宏定義導出的檔案名應包括的內容。 下表中的宏描述了在UI中找到的元素 [檔案名配置](../ui/activate-batch-profile-destinations.md#file-names) 的上界。

作為最佳做法，您應始終包括 `SEGMENT_ID` 宏。 段ID是唯一的，因此將它們包括在檔案名中是確保檔案名也唯一的最佳方法。

| 宏 | UI標籤 | 說明 | 範例 |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL 目標] | UI中的目標名稱。 | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL 段ID] | 唯一、平台生成的段ID | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL 段名稱] | 用戶定義的段名稱 | VIP訂戶 |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL 目標ID] | 目標實例的唯一、平台生成的ID | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL 目標名稱] | 目標實例的用戶定義的名稱。 | 我2022年的廣告目的地 |
| `ORGANIZATION_NAME` | [!UICONTROL 組織名稱] | 客戶組織在Adobe Experience Platform的名稱。 | 我的組織名稱 |
| `SANDBOX_NAME` | [!UICONTROL 沙盒名稱] | 客戶使用的沙盒的名稱。 | 收縮 |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL 日期和時間] | `DATETIME` 和 `TIMESTAMP` 兩者都定義生成檔案的時間，但格式不同。 <br><br><ul><li>`DATETIME` 使用以下格式：YYYYMMDD_HHMMSS。</li><li>`TIMESTAMP` 使用10位Unix格式。 </li></ul> `DATETIME` 和 `TIMESTAMP` 互斥，不能同時使用。 | <ul><li>`DATETIME`:20220509_210543</li><li>`TIMESTAMP`:1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL 自定義文本] | 要包含在檔案名中的用戶定義的自定義文本。 不能用於 `defaultFilename`。 | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL 日期和時間] | 以Unix格式生成檔案的時間的10位時間戳。 | 1652131584 |

{style=&quot;table-layout:auto&quot;&quot;

![顯示帶有預選宏的檔案名配置螢幕的UI影像](assets/file-name-configuration.png)

上圖所示的示例使用以下檔案名宏配置：

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


## 歷史配置檔案資格 {#profile-backfill}

您可以使用 `backfillHistoricalProfileData` 目標配置中的參數，以確定是否應將歷史配置檔案資格導出到目標。

```json
   "backfillHistoricalProfileData":true
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `backfillHistoricalProfileData` | 布林值 | 控制在將段激活到目標時是否導出歷史配置檔案資料。 <br> <ul><li> `true`: [!DNL Platform] 發送在激活段之前符合段的歷史用戶配置檔案。 </li><li> `false`: [!DNL Platform] 僅包括激活段後符合段條件的用戶配置檔案。 </li></ul> |

{style=&quot;table-layout:auto&quot;&quot;

## 此配置如何連接目標的所有必要資訊 {#connecting-all-configurations}

您的某些目標設定必須通過 [目標伺服器](./server-and-file-configuration.md) 或 [觀眾元資料配置](./audience-metadata-management.md)。 此處描述的目標配置通過引用以下兩個其他配置來連接所有這些設定：

* 使用 `destinationServerId` 引用為目標設定的目標伺服器和模板配置。
* 使用 `audienceMetadataId` 引用為目標設定的受眾元資料配置。
