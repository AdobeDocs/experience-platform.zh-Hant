---
description: 此頁列出並說明了可以使用「/authoring/destinations」 API終結點執行的所有API操作。
title: 目標API終結點操作
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 75399d2fbe111a296479f8d3404d43c6ba0d50b5
workflow-type: tm+mt
source-wordcount: '2572'
ht-degree: 4%

---

# 目標終結點API操作 {#destination-configuration}

>[!IMPORTANT]
>
>**API終結點**: `platform.adobe.io/data/core/activation/authoring/destinations`

此頁列出並說明了可以使用 `/authoring/destinations` API終結點。 有關此終結點支援的功能的說明，請閱讀 [目標配置](./destination-configuration.md)。

## 目標API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](./getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 建立流目標的配置 {#create}

您可以通過向POST請求建立新的目標配置 `/authoring/destinations` 端點。

**API格式**

```http
POST /authoring/destinations
```

**要求**

以下請求將建立新的流式傳輸目標配置，該配置由負載中提供的參數配置。 下面的負載包括所有參數，用於流目標，由 `/authoring/destinations` 端點。 請注意，您不必在調用中添加所有參數，並且模板可根據API要求進行自定義。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
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
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
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
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `name` | 字串 | 指示Experience Platform目錄中目標的標題 |
| `description` | 字串 | 提供Adobe將用於目標卡的Experience Platform目標目錄的說明。 目標不超過4-5句。 |
| `status` | 字串 | 指示目標卡的生命週期狀態。 接受的值為 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 在首次配置目標時。 |
| `customerAuthenticationConfigurations` | 字串 | 指示用於將Experience Platform客戶驗證到伺服器的配置。 請參閱 `authType` 下面是接受的值。 |
| `customerAuthenticationConfigurations.authType` | 字串 | 流目標支援的值為： <ul><li>`OAUTH2`</li><li>`BEARER`</li></ul> 基於檔案的目標支援的值為： <ul><li>`S3`</li><li>`AZURE_CONNECTION_STRING`</li><li>`AZURE_SERVICE_PRINCIPAL`</li><li>`SFTP_WITH_SSH_KEY`</li><li>`SFTP_WITH_PASSWORD`</li></ul> |
| `customerDataFields.name` | 字串 | 提供要引入的自定義欄位的名稱。 |
| `customerDataFields.type` | 字串 | 指示您要引入的自定義欄位類型。 接受的值為 `string`。 `object`。 `integer` |
| `customerDataFields.title` | 字串 | 指示欄位的名稱，如客戶在Experience Platform用戶介面中看到的 |
| `customerDataFields.description` | 字串 | 提供自定義欄位的說明。 |
| `customerDataFields.isRequired` | 布林值 | 指示目標設定工作流中是否需要此欄位。 |
| `customerDataFields.enum` | 字串 | 將自定義欄位呈現為下拉菜單並列出用戶可用的選項。 |
| `customerDataFields.pattern` | 字串 | 如果需要，為自定義欄位強制實施模式。 使用規則運算式來強制模式。 例如，如果客戶ID不包括數字或下划線，請輸入 `^[A-Za-z]+$` 的子菜單。 |
| `uiAttributes.documentationLink` | 字串 | 引用中的文檔頁面 [目標目錄](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `https://www.adobe.com/go/destinations-YOURDESTINATION-en`，也請參見Wiki頁。 `YOURDESTINATION` 是目標的名稱。 對於名為Moviestar的目標，您將使用 `https://www.adobe.com/go/destinations-moviestar-en`。 請注意，此連結僅在Adobe設定目標即時並發佈文檔後才起作用。 |
| `uiAttributes.category` | 字串 | 指分配給您在Adobe Experience Platform的目標的類別。 有關詳細資訊，請閱讀 [目標類別](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories)。 使用以下值之一： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`。 |
| `uiAttributes.connectionType` | 字串 | `Server-to-server` 是當前唯一可用的選項。 |
| `uiAttributes.frequency` | 字串 | `Streaming` 是當前唯一可用的選項。 |
| `identityNamespaces.externalId.acceptsAttributes` | 布林值 | 指示目標是否接受標準配置檔案屬性。 通常，這些屬性會在合作夥伴的文檔中加以強調。 |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 布林值 | 指示客戶是否可以在目標中設定自定義命名空間。 |
| `identityNamespaces.externalId.transformation` | 字串 | _未在示例配置中顯示_。 例如，在 [!DNL Platform] 客戶將純電子郵件地址作為屬性，而您的平台只接受經過散列的電子郵件。 您將在此處提供需要應用的轉換（例如，將電子郵件轉換為小寫，然後進行散列）。 |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 用於平台接受 [標準標識命名空間](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) （例如，IDFA），因此您可以限制平台用戶只選擇這些標識命名空間。 <br> 使用 `acceptedGlobalNamespaces`，您可以使用 `"requiredTransformation":"sha256(lower($))"` 到小寫和散列電子郵件地址或電話號碼。 |
| `destinationDelivery.authenticationRule` | 字串 | 指示如何 [!DNL Platform] 客戶連接到您的目標。 接受的值為 `CUSTOMER_AUTHENTICATION`。 `PLATFORM_AUTHENTICATION`。 `NONE`。 <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果平台客戶通過用戶名和密碼、持有者令牌或其他身份驗證方法登錄到您的系統。 例如，如果同時選擇了 `authType: OAUTH2` 或 `authType:BEARER` 在 `customerAuthenticationConfigurations`。 </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe與目標之間有全局身份驗證系統， [!DNL Platform] 客戶不需要提供任何身份驗證憑據來連接到目標。 在這種情況下，必須使用 [憑據](./credentials-configuration-api.md) 配置。 </li><li>使用 `NONE` 如果向目標平台發送資料不需要身份驗證。 </li></ul> |
| `destinationDelivery.destinationServerId` | 字串 | 的 `instanceId` 的 [目標伺服器模板](./destination-server-api.md) 用於此目標。 |
| `backfillHistoricalProfileData` | 布林值 | 控制在將段激活到目標時是否導出歷史配置檔案資料。 <br> <ul><li> `true`: [!DNL Platform] 發送在激活段之前符合段的歷史用戶配置檔案。 </li><li> `false`: [!DNL Platform] 僅包括激活段後符合段條件的用戶配置檔案。 </li></ul> |
| `segmentMappingConfig.mapUserInput` | 布林值 | 控制用戶是否輸入目標激活工作流中的段映射ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 布林值 | 控制目標激活工作流中的段映射ID是否是Experience Platform段ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 布林值 | 控制目標激活工作流中的段映射id是否是Experience Platform段名稱。 |
| `segmentMappingConfig.audienceTemplateId` | 布林值 | 的 `instanceId` 的 [受眾元資料模板](./audience-metadata-api.md) 用於此目標。 |
| `schemaConfig.profileFields` | 陣列 | 添加預定義項時 `profileFields` 如上面的配置所示，用戶可以選擇將Experience Platform屬性映射到目標側的預定義屬性。 |
| `schemaConfig.profileRequired` | 布林值 | 使用 `true` 如果用戶應能將配置檔案屬性從Experience Platform映射到目標側的自定義屬性，如上面的示例配置所示。 |
| `schemaConfig.segmentRequired` | 布林值 | 始終使用 `segmentRequired:true`。 |
| `schemaConfig.identityRequired` | 布林值 | 使用 `true` 如果用戶應能夠將標識命名空間從Experience Platform映射到所需的架構。 |
| `aggregation.aggregationType` | - | 選取「`BEST_EFFORT`」或「`CONFIGURABLE_AGGREGATION`」。上面的示例配置包括 `BEST_EFFORT` 聚合。 例如 `CONFIGURABLE_AGGREGATION`，請參閱 [目標配置](./destination-configuration.md#example-configuration) 的子菜單。 下表介紹了與可配置聚合相關的參數。 |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | 整數 | Experience Platform可以在單個HTTP調用中聚合多個導出的配置檔案。 指定終結點在單個HTTP調用中應接收的最大配置檔案數。 請注意，這是一種盡力的聚合。 例如，如果指定值100，平台可能會在呼叫時發送小於100的任意數量的配置檔案。 <br> 如果伺服器不接受每個請求的多個用戶，請將此值設定為1。 |
| `aggregation.bestEffortAggregation.splitUserById` | 布林值 | 如果應按標識拆分到目標的調用，則使用此標誌。 將此標誌設定為 `true` 如果伺服器對給定命名空間每次只接受一個標識。 |
| `aggregation.configurableAggregation.splitUserById` | 布林值 | 請參見示例配置中的參數 [這裡](./destination-configuration.md#example-configuration)。 如果應按標識拆分到目標的調用，則使用此標誌。 將此標誌設定為 `true` 如果伺服器對給定命名空間每次只接受一個標識。 |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | 整數 | <ul><li>*最小值：1800*</li><li>*最大值：3600*</li><li>請參見示例配置中的參數 [這裡](./destination-configuration.md#example-configuration)。 配置最小值和最大可接受值之間的值。 與 `maxNumEventsInBatch`，此參數確定Experience Platform應等待多長時間，直到將API調用發送到您的終結點。 <br> 例如，如果對這兩個參數都使用最大值，Experience Platform將等待3600秒或直到有10000個限定配置檔案才進行API調用（以先發生的情況為準）。 </li></ul> |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | 整數 | <ul><li>*最小值：1000*</li><li>*最大值：10000*</li><li>請參見示例配置中的參數 [這裡](./destination-configuration.md#example-configuration)。 配置最小值和最大可接受值之間的值。 有關此參數的說明，請參見 `maxBatchAgeInSecs` 就在上面。</li></ul> |
| `aggregation.configurableAggregation.aggregationKey` | 布林值 | 請參見示例配置中的參數 [這裡](./destination-configuration.md#example-configuration)。 允許您根據以下參數聚合映射到目標的導出配置檔案： <br> <ul><li>段ID</li><li> 段狀態 </li><li> 標識命名空間 </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | 布林值 | 請參見示例配置中的參數 [這裡](./destination-configuration.md#example-configuration)。 將此設定為 `true` 按段ID對導出到目標的配置檔案進行分組。 |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | 布林值 | 請參見示例配置中的參數 [這裡](./destination-configuration.md#example-configuration)。 必須同時設定 `includeSegmentId:true` 和 `includeSegmentStatus:true` 按段ID和段狀態對導出到目標的配置檔案進行分組。 |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | 布林值 | 請參見示例配置中的參數 [這裡](./destination-configuration.md#example-configuration)。 將此設定為 `true` 按標識名稱空間將導出到目標的配置檔案分組。 |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | 布林值 | 請參見示例配置中的參數 [這裡](./destination-configuration.md#example-configuration)。 使用此參數可指定是否希望導出的配置檔案聚合為單個標識的組（GAID、IDFA、電話號碼、電子郵件等）。 |
| `aggregation.configurableAggregation.aggregationKey.groups` | 字串 | 請參見示例配置中的參數 [這裡](./destination-configuration.md#example-configuration)。 如果要按標識命名空間的組將導出到目標的配置檔案分組，請建立標識組清單。 例如，您可以使用示例中的配置將包含IDFA和GAID移動標識符的配置檔案合併為一個到目標的呼叫和電子郵件，再將另一個組合為電子郵件。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的響應返回HTTP狀態200，其中包含您新建立的目標配置的詳細資訊。

## 為基於檔案的目標建立配置 {#create-file-based}

您可以通過向POST請求建立新的目標配置 `/authoring/destinations` 端點。

**API格式**

```http
POST /authoring/destinations
```

**要求**

以下請求將建立新 [!DNL Amazon S3] 基於檔案的目標配置，由負載中提供的參數配置。 以下負載包括接受的基於檔案的目標的所有參數 `/authoring/destinations` 端點。 請注意，您不必在調用中添加所有參數，並且模板可根據API要求進行自定義。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
        "name": "S3 Destination with CSV Options",
        "description": "S3 Destination with CSV Options",
        "releaseNotes": "S3 Destination with CSV Options",
        "status": "TEST",
        "customerAuthenticationConfigurations": [
            {
                "authType": "S3"
            }
        ],
        "customerEncryptionConfigurations": [
            {
                "encryptionAlgo": ""
            }
        ],
        "customerDataFields": [
            {
                "name": "bucket",
                "title": "Select S3 Bucket",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "path",
                "title": "S3 path",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "pattern": "^[A-Za-z]+$",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "sep",
                "title": "Select separator for each field and value",
                "description": "Select for each field and value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "encoding",
                "title": "Specify encoding (charset) of saved CSV files",
                "description": "Select encoding of csv files",
                "type": "string",
                "enum": ["UTF-8", "UTF-16"],
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quote",
                "title": "Select a single character used for escaping quoted values",
                "description": "Select single charachter for escaping quoted values",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quoteAll",
                "title": "Quote All",
                "description": "Select flag for escaping quoted values",
                "type": "string",
                "enum" : ["true","false"],
                "default": "true",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "escape",
                "title": "Select a single character used for escaping quotes",
                "description": "Select a single character used for escaping quotes inside an already quoted value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "escapeQuotes",
                "title": "Escape quotes",
                "description": "A flag indicating whether values containing quotes should always be enclosed in quotes",
                "type": "string",
                "enum" : ["true","false"],
                "isRequired": false,
                "default": "true",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "header",
                "title": "header",
                "description": "Writes the names of columns as the first line.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "ignoreLeadingWhiteSpace",
                "title": "Ignore leading white space",
                "description": "A flag indicating whether or not leading whitespaces from values being written should be skipped.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "nullValue",
                "title": "Select the string representation of a null value",
                "description": "Sets the string representation of a null value. ",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "dateFormat",
                "title": "Date format",
                "description": "Select the string that indicates a date format. ",
                "type": "string",
                "default": "yyyy-MM-dd",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "charToEscapeQuoteEscaping",
                "title": "Char to escape quote escaping",
                "description": "Sets a single character used for escaping the escape for the quote character",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "emptyValue",
                "title": "Select the string representation of an empty value",
                "description": "Select the string representation of an empty value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "default": "",
                "hidden": false
            },
            {
                "name": "compression",
                "title": "Select compression",
                "description": "Select compressiont",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "enum" : ["SNAPPY","GZIP","DEFLATE", "NONE"]
            },
            {
                "name": "fileType",
                "title": "Select a fileType",
                "description": "Select fileType",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false,
                "enum" :["csv", "json", "parquet"],
                "default" : "csv"
            }
        ],
        "uiAttributes": {
            "documentationLink": "https://www.adobe.io/apis/experienceplatform.html",
            "category": "S3",
            "iconUrl": "https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
            "connectionType": "S3",
            "flowRunsSupported": true,
            "monitoringSupported": true,
            "frequency": "Batch"
        },
        "destinationDelivery": [
            {
                "deliveryMatchers" : [
                    {
                        "type" : "SOURCE",
                        "value" : [
                            "batch"
                        ]
                    }
                ],
                "authenticationRule": "CUSTOMER_AUTHENTICATION",
                "destinationServerId": "{{destinationServerId}}"
            }
        ],
        "schemaConfig" : {
            "profileRequired" : true,
            "segmentRequired" : true,
            "identityRequired" : true
        },
        "batchConfig":{
            "allowMandatoryFieldSelection": true,
            "allowJoinKeyFieldSelection": true,
            "defaultExportMode": "DAILY_FULL_EXPORT",
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
                "ONCE",
                "EVERY_HOUR"
            ],
            "defaultFrequency":"DAILY",
            "defaultStartTime":"00:00"
        },
        "backfillHistoricalProfileData": true
    }
```

有關上述所有參數的詳細說明，請參見 [基於檔案的目標配置](file-based-destination-configuration.md)。

**回應**

成功的響應返回HTTP狀態200，其中包含您新建立的目標配置的詳細資訊。

## 列出目標配置 {#retrieve-list}

通過向IMS組織發出GET請求，您可以檢索IMS組織的所有目標配置清單 `/authoring/destinations` 端點。

**API格式**


```http
GET /authoring/destinations
```

**要求**

以下請求將根據IMS組織和沙盒配置檢索您有權訪問的目標配置清單。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

以下響應會根據您使用的IMS組織ID和沙盒名稱返回HTTP狀態200，其中包含您有權訪問的目標配置清單。 一 `instanceId` 對應於一個目標的模板。 響應被截斷以便簡化。

```json
{
   "items":[
      {
         "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
         "createdDate":"2020-10-28T06:14:09.784471Z",
         "lastModifiedDate":"2021-06-28T06:14:09.784471Z",
         "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
         "sandboxName":"prod",
         "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
         "name":"Moviestar",
         "description":"Moviestar is a fictional destination, used for this example.",
         "status":"TEST",
         "customerAuthenticationConfigurations":[
            {
               "authType":"BEARER"
            }
         ],
         "customerDataFields":[
            {
               "name":"endpointsInstance",
               "type":"string",
               "title":"Select Endpoint",
               "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
               "isRequired":true,
               "enum":[
                  "US",
                  "EU",
                  "APAC",
                  "NZ"
               ]
            },
            {
               "name":"customerID",
               "type":"string",
               "title":"Moviestar Customer ID",
               "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
               "isRequired":true,
               "pattern":"^[A-Za-z]+$"
            }
         ],
         "uiAttributes":{
            "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
            "category":"mobile",
            "connectionType":"Server-to-server",
            "frequency":"Streaming"
         },
         "identityNamespaces":{
            "external_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true,
               "acceptedGlobalNamespaces":{
                  "Email":{
                     
                  }
               }
            },
            "another_id":{
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
                  "name":"a_custom_attribute",
                  "title":"a_custom_attribute",
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
         "aggregation":{
            "aggregationType":"BEST_EFFORT",
            "bestEffortAggregation":{
               "maxUsersPerRequest":10,
               "splitUserById":false
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
    
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `name` | 字串 | 指示Experience Platform目錄中目標的標題。 |
| `description` | 字串 | 提供Adobe將用於目標卡的Experience Platform目標目錄的說明。 目標不超過4-5句。 |
| `status` | 字串 | 指示目標卡的生命週期狀態。 接受的值為 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 在首次配置目標時。 |
| `customerAuthenticationConfigurations` | 字串 | 指示用於將Experience Platform客戶驗證到伺服器的配置。 請參閱 `authType` 下面是接受的值。 |
| `customerAuthenticationConfigurations.authType` | 字串 | 接受的值為 `OAUTH2, BEARER`。 |
| `customerDataFields.name` | 字串 | 提供要引入的自定義欄位的名稱。 |
| `customerDataFields.type` | 字串 | 指示您要引入的自定義欄位類型。 接受的值為 `string`。 `object`。 `integer` |
| `customerDataFields.title` | 字串 | 指示欄位的名稱，如客戶在Experience Platform用戶介面中看到的 |
| `customerDataFields.description` | 字串 | 提供自定義欄位的說明。 |
| `customerDataFields.isRequired` | 布林值 | 指示目標設定工作流中是否需要此欄位。 |
| `customerDataFields.enum` | 字串 | 將自定義欄位呈現為下拉菜單並列出用戶可用的選項。 |
| `customerDataFields.pattern` | 字串 | 如果需要，為自定義欄位強制實施模式。 使用規則運算式來強制模式。 例如，如果客戶ID不包括數字或下划線，請輸入 `^[A-Za-z]+$` 的子菜單。 |
| `uiAttributes.documentationLink` | 字串 | 引用中的文檔頁面 [目標目錄](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `https://www.adobe.com/go/destinations-YOURDESTINATION-en`，也請參見Wiki頁。 `YOURDESTINATION` 是目標的名稱。 對於名為Moviestar的目標，您將使用 `https://www.adobe.com/go/destinations-moviestar-en`。 請注意，此連結僅在Adobe設定目標即時並發佈文檔後才起作用。 |
| `uiAttributes.category` | 字串 | 指分配給您在Adobe Experience Platform的目標的類別。 有關詳細資訊，請閱讀 [目標類別](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories)。 使用以下值之一： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | 字串 | `Server-to-server` 是當前唯一可用的選項。 |
| `uiAttributes.frequency` | 字串 | `Streaming` 是當前唯一可用的選項。 |
| `identityNamespaces.externalId.acceptsAttributes` | 布林值 | 指示目標是否接受標準配置檔案屬性。 通常，這些屬性會在合作夥伴的文檔中加以強調。 |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 布林值 | 指示客戶是否可以在目標中設定自定義命名空間。 閱讀有關 [自定義命名空間](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#manage-namespaces) 在Adobe Experience Platform。 |
| `identityNamespaces.externalId.transformation` | 字串 | _未在示例配置中顯示_。 例如，在 [!DNL Platform] 客戶將純電子郵件地址作為屬性，而您的平台只接受經過散列的電子郵件。 您將在此處提供需要應用的轉換（例如，將電子郵件轉換為小寫，然後進行散列）。 |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 用於平台接受 [標準標識命名空間](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) （例如，IDFA），因此您可以限制平台用戶只選擇這些標識命名空間。 |
| `destinationDelivery.authenticationRule` | 字串 | 指示如何 [!DNL Platform] 客戶連接到您的目標。 接受的值為 `CUSTOMER_AUTHENTICATION`。 `PLATFORM_AUTHENTICATION`。 `NONE`。 <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果平台客戶通過用戶名和密碼、持有者令牌或其他身份驗證方法登錄到您的系統。 例如，如果同時選擇了 `authType: OAUTH2` 或 `authType:BEARER` 在 `customerAuthenticationConfigurations`。 </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe與目標之間有全局身份驗證系統， [!DNL Platform] 客戶不需要提供任何身份驗證憑據來連接到目標。 在這種情況下，必須使用 [憑據](./authentication-configuration.md) 配置。 </li><li>使用 `NONE` 如果向目標平台發送資料不需要身份驗證。 </li></ul> |
| `destinationDelivery.destinationServerId` | 字串 | 的 `instanceId` 的 [目標伺服器模板](./destination-server-api.md) 用於此目標。 |
| `destConfigId` | 字串 | 此欄位是自動生成的，不需要輸入。 |
| `backfillHistoricalProfileData` | 布林值 | 控制在將段激活到目標時是否導出歷史配置檔案資料。 <br> <ul><li> `true`: [!DNL Platform] 發送在激活段之前符合段的歷史用戶配置檔案。 </li><li> `false`: [!DNL Platform] 僅包括激活段後符合段條件的用戶配置檔案。 </li></ul> |
| `segmentMappingConfig.mapUserInput` | 布林值 | 控制用戶是否輸入目標激活工作流中的段映射ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 布林值 | 控制目標激活工作流中的段映射ID是否是Experience Platform段ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 布林值 | 控制目標激活工作流中的段映射id是否是Experience Platform段名稱。 |
| `segmentMappingConfig.audienceTemplateId` | 布林值 | 的 `instanceId` 的 [受眾元資料模板](./audience-metadata-management.md) 用於此目標。 要設定受眾元資料模板，請閱讀 [受眾元資料API參考](./audience-metadata-api.md)。 |

{style=&quot;table-layout:auto&quot;&quot;

## 更新現有目標配置 {#update}

您可以通過向PUT請求更新現有目標配置 `/authoring/destinations` 終結點並提供要更新的目標配置的實例ID。 在呼叫正文中，提供更新的目標配置。

**API格式**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要更新的目標配置的ID。 |

**要求**

以下請求更新現有目標配置，該配置由負載中提供的參數配置。 在下面的示例調用中，我們正在更新配置 [建立早](./destination-configuration-api.md#create) 現在接受GAID、IDFA和散列電子郵件標識符作為標識命名空間。

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-04-28T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
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
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
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
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

## 檢索特定目標配置 {#get}

通過向Web站點發出GET請求，可以檢索有關特定目標配置的詳細資訊 `/authoring/destinations` 終結點並提供要檢索的目標配置的實例ID。

**API格式**


```http
GET /authoring/destinations/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要檢索的目標配置的ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關指定目標配置的詳細資訊。

```json
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-06-04T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
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
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
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
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```


## 刪除特定目標配置 {#delete}

您可以通過向DELETE請求刪除指定的目標配置 `/authoring/destinations` 終結點，並提供您希望在請求路徑中刪除的目標配置的ID。

**API格式**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 的 `id` 目標配置。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的響應返回HTTP狀態200以及空的HTTP響應。

## API錯誤處理

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟

閱讀此文檔後，您現在知道如何使用 `/authoring/destinations` API終結點。 閱讀 [如何使用Destination SDK配置目標](./configure-destination-instructions.md) 瞭解此步驟在配置目標過程中的適用範圍。
