---
description: 本頁列出並說明您可使用「/authoring/destinations」 API端點執行的所有API操作。
title: 目的地API端點作業
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '2536'
ht-degree: 4%

---

# 目的地端點API作業 {#destination-configuration}

>[!IMPORTANT]
>
>**API端點**: `platform.adobe.io/data/core/activation/authoring/destinations`

此頁面列出並說明您可使用 `/authoring/destinations` API端點。 有關此端點支援的功能的說明，請閱讀 [目的地配置](./destination-configuration.md).

## 目的地API作業快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 建立串流目的地的設定 {#create}

您可以向 `/authoring/destinations` 端點。

**API格式**

```http
POST /authoring/destinations
```

**要求**

下列請求會建立新的串流目的地設定，由裝載中提供的參數所設定。 以下裝載包含所接受串流目的地的所有參數 `/authoring/destinations` 端點。 請注意，您不必在呼叫上新增所有參數，且可根據您的API需求自訂範本。

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
| `name` | 字串 | 指出Experience Platform目錄中的目的地標題 |
| `description` | 字串 | 提供說明，供Adobe用於目的地卡的Experience Platform目的地目錄。 目標不超過4-5句。 |
| `status` | 字串 | 指示目標卡的生命週期狀態。 接受的值為 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 設定目的地時。 |
| `customerAuthenticationConfigurations` | 字串 | 指示用於驗證Experience Platform客戶到伺服器的配置。 請參閱 `authType` 以取得接受的值。 |
| `customerAuthenticationConfigurations.authType` | 字串 | 串流目的地的支援值為： <ul><li>`BASIC`</li><li>`BEARER`</li><li>`OAUTH2`</li></ul> 檔案型目的地的支援值為： <ul><li>`S3`</li><li>`AZURE_CONNECTION_STRING`</li><li>`AZURE_SERVICE_PRINCIPAL`</li><li>`SFTP_WITH_SSH_KEY`</li><li>`SFTP_WITH_PASSWORD`</li></ul> |
| `customerDataFields.name` | 字串 | 提供您要引入的自訂欄位名稱。 |
| `customerDataFields.type` | 字串 | 指出您要引入的自訂欄位類型。 接受的值為 `string`, `object`, `integer` |
| `customerDataFields.title` | 字串 | 指出欄位的名稱，如Experience Platform使用者介面中的客戶所見 |
| `customerDataFields.description` | 字串 | 提供自訂欄位的說明。 |
| `customerDataFields.isRequired` | 布林值 | 指示目標設定工作流中是否需要此欄位。 |
| `customerDataFields.enum` | 字串 | 將自訂欄位轉譯為下拉式功能表，並列出使用者可用的選項。 |
| `customerDataFields.pattern` | 字串 | 視需要為自訂欄位強制使用模式。 使用規則運算式來強制模式。 例如，若您的客戶ID未包含數字或底線，請輸入 `^[A-Za-z]+$` 在此欄位中。 |
| `uiAttributes.documentationLink` | 字串 | 指 [目的地目錄](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `https://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中 `YOURDESTINATION` 是您目的地的名稱。 對於名為Moviestar的目的地，您將使用 `https://www.adobe.com/go/destinations-moviestar-en`. 請注意，此連結只有在Adobe將您的目的地設為現時且檔案已發佈後才有效。 |
| `uiAttributes.category` | 字串 | 是指指派給Adobe Experience Platform中目的地的類別。 如需詳細資訊，請閱讀 [目標類別](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). 使用下列其中一個值： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | 字串 | `Server-to-server` 是目前唯一可用的選項。 |
| `uiAttributes.frequency` | 字串 | `Streaming` 是目前唯一可用的選項。 |
| `identityNamespaces.externalId.acceptsAttributes` | 布林值 | 指出客戶是否可將標準設定檔屬性對應至您正在設定的身分。 |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 布林值 | 指出客戶是否可對應屬於 [自訂命名空間](/help/identity-service/namespaces.md#manage-namespaces) 至您所設定的身分。 |
| `identityNamespaces.externalId.transformation` | 字串 | _範例設定中未顯示_. 例如，當 [!DNL Platform] 客戶有純電子郵件地址作為屬性，而您的平台僅接受雜湊電子郵件。 您可在此提供需要套用的轉換（例如，將電子郵件轉換為小寫，然後雜湊）。 |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 指出 [標準身分命名空間](/help/identity-service/namespaces.md#standard) （例如IDFA）客戶可對應至您所設定的身分。 <br> 使用 `acceptedGlobalNamespaces`，您可以使用 `"requiredTransformation":"sha256(lower($))"` 小寫和雜湊電子郵件地址或電話號碼。 |
| `destinationDelivery.authenticationRule` | 字串 | 指示方式 [!DNL Platform] 客戶可連線至您的目的地。 接受的值為 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客戶透過使用者名稱和密碼、承載權杖或其他驗證方法登入您的系統。 例如，如果您也選取了 `authType: OAUTH2` 或 `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe與目的地之間有全域驗證系統，則 [!DNL Platform] 客戶不需要提供任何驗證憑證來連線至您的目的地。 在此情況下，您必須使用 [憑證](./credentials-configuration-api.md) 設定。 </li><li>使用 `NONE` 若無需驗證即可將資料傳送至目的地平台。 </li></ul> |
| `destinationDelivery.destinationServerId` | 字串 | 此 `instanceId` 的 [目的地伺服器範本](./destination-server-api.md) 用於此目的地。 |
| `backfillHistoricalProfileData` | 布林值 | 控制在將區段啟動至目的地時，是否匯出歷史設定檔資料。 <br> <ul><li> `true`: [!DNL Platform] 傳送在啟用區段之前符合區段資格的歷史使用者設定檔。 </li><li> `false`: [!DNL Platform] 僅包含區段啟動後符合區段資格的使用者設定檔。 </li></ul> |
| `segmentMappingConfig.mapUserInput` | 布林值 | 控制使用者是否輸入目標啟動工作流程中的區段對應ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 布林值 | 控制目標啟動工作流程中的區段對應ID是否為Experience Platform區段ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 布林值 | 控制目標啟動工作流程中的區段對應ID是否為Experience Platform區段名稱。 |
| `segmentMappingConfig.audienceTemplateId` | 布林值 | 此 `instanceId` 的 [對象中繼資料範本](./audience-metadata-api.md) 用於此目的地。 |
| `schemaConfig.profileFields` | 陣列 | 新增預先定義的 `profileFields` 如上方的設定所示，使用者將可以選擇將Experience Platform屬性對應至目的地端的預先定義屬性。 |
| `schemaConfig.profileRequired` | 布林值 | 使用 `true` 如果使用者應能將設定檔屬性從Experience Platform對應至目的地端的自訂屬性，如上方的範例設定所示。 |
| `schemaConfig.segmentRequired` | 布林值 | 一律使用 `segmentRequired:true`. |
| `schemaConfig.identityRequired` | 布林值 | 使用 `true` 如果您的使用者應能將身分識別命名空間從Experience Platform對應至您想要的架構。 |
| `aggregation.aggregationType` | - | 選取「`BEST_EFFORT`」或「`CONFIGURABLE_AGGREGATION`」。上述範例設定包含 `BEST_EFFORT` 匯總。 例如 `CONFIGURABLE_AGGREGATION`，請參閱 [目的地配置](./destination-configuration.md#example-configuration) 檔案。 下表介紹了與可配置聚合相關的參數。 |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | 整數 | Experience Platform可以在單一HTTP呼叫中匯總多個匯出的設定檔。 指定端點在單一HTTP呼叫中應接收的設定檔數上限。 請注意，這是最佳的匯總方式。 例如，如果您指定值100,Platform可能會在呼叫中傳送小於100的任何設定檔數量。 <br> 如果您的伺服器不接受每個請求有多個使用者，請將此值設為1。 |
| `aggregation.bestEffortAggregation.splitUserById` | 布林值 | 如果目標的呼叫應依身分分割，請使用此標幟。 將此標幟設為 `true` 如果您的伺服器在每次呼叫中僅接受一個身分，則會接受指定命名空間的。 |
| `aggregation.configurableAggregation.splitUserById` | 布林值 | 請參閱範例設定中的參數 [此處](./destination-configuration.md#example-configuration). 如果目標的呼叫應依身分分割，請使用此標幟。 將此標幟設為 `true` 如果您的伺服器在每次呼叫中僅接受一個身分，則會接受指定命名空間的。 |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | 整數 | <ul><li>*最小值：1800*</li><li>*最大值：3600*</li><li>請參閱範例設定中的參數 [此處](./destination-configuration.md#example-configuration). 在最小值和最大接受值之間配置一個值。 與 `maxNumEventsInBatch`，此參數會決定Experience Platform應等待多久，直到傳送API呼叫至您的端點。 <br> 例如，如果您對這兩個參數使用最大值，Experience Platform會先等候3600秒或直到有10,000個合格設定檔，再進行API呼叫（以先發生者為準）。 </li></ul> |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | 整數 | <ul><li>*最小值：1000*</li><li>*最大值：10000*</li><li>請參閱範例設定中的參數 [此處](./destination-configuration.md#example-configuration). 在最小值和最大接受值之間配置一個值。 如需此參數的說明，請參閱 `maxBatchAgeInSecs` 就在上面。</li></ul> |
| `aggregation.configurableAggregation.aggregationKey` | 布林值 | 請參閱範例設定中的參數 [此處](./destination-configuration.md#example-configuration). 可讓您根據下列參數，匯總對應至目的地的匯出設定檔： <br> <ul><li>區段ID</li><li> 區段狀態 </li><li> 身分命名空間 </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | 布林值 | 請參閱範例設定中的參數 [此處](./destination-configuration.md#example-configuration). 將此設定為 `true` 如果您想要依區段ID將匯出至目的地的設定檔分組。 |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | 布林值 | 請參閱範例設定中的參數 [此處](./destination-configuration.md#example-configuration). 您必須同時設定 `includeSegmentId:true` 和 `includeSegmentStatus:true` 如果您想要依區段ID和區段狀態，將匯出至目的地的設定檔分組。 |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | 布林值 | 請參閱範例設定中的參數 [此處](./destination-configuration.md#example-configuration). 將此設定為 `true` 如果您想要依身分命名空間將匯出至目的地的設定檔分組。 |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | 布林值 | 請參閱範例設定中的參數 [此處](./destination-configuration.md#example-configuration). 使用此參數可指定是否要將匯出的設定檔匯總為單一身分的群組（GAID、IDFA、電話號碼、電子郵件等）。 |
| `aggregation.configurableAggregation.aggregationKey.groups` | 字串 | 請參閱範例設定中的參數 [此處](./destination-configuration.md#example-configuration). 如果您想要依身分命名空間的群組，將匯出至目的地的設定檔分組，請建立身分群組清單。 例如，您可以使用範例中的設定，將包含IDFA和GAID行動識別碼的設定檔，合併至對您目的地的呼叫和電子郵件中。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回HTTP狀態200，並包含您新建立之目的地組態的詳細資訊。

## 建立檔案型目的地的設定 {#create-file-based}

您可以向 `/authoring/destinations` 端點。

**API格式**

```http
POST /authoring/destinations
```

**要求**

下列請求會建立新 [!DNL Amazon S3] 檔案式目的地設定，由裝載中提供的參數設定。 以下裝載包含接受之檔案式目的地的所有參數 `/authoring/destinations` 端點。 請注意，您不必在呼叫上新增所有參數，且可根據您的API需求自訂範本。

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

如需上述所有參數的詳細說明，請參閱 [基於檔案的目標配置](file-based-destination-configuration.md).

**回應**

成功的回應會傳回HTTP狀態200，並包含您新建立之目的地組態的詳細資訊。

## 列出目標配置 {#retrieve-list}

您可以向 `/authoring/destinations` 端點。

**API格式**


```http
GET /authoring/destinations
```

**要求**

下列請求會根據組織和沙箱設定，擷取您有權存取的目的地設定清單。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

下列回應會根據您使用的組織ID和沙箱名稱，傳回HTTP狀態200，並列出您可存取的目標設定。 一 `instanceId` 對應至一個目的地的範本。 回應會為簡潔而截斷。

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
| `name` | 字串 | 指出Experience Platform目錄中的目的地標題。 |
| `description` | 字串 | 提供說明，供Adobe用於目的地卡的Experience Platform目的地目錄。 目標不超過4-5句。 |
| `status` | 字串 | 指示目標卡的生命週期狀態。 接受的值為 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 設定目的地時。 |
| `customerAuthenticationConfigurations` | 字串 | 指示用於驗證Experience Platform客戶到伺服器的配置。 請參閱 `authType` 以取得接受的值。 |
| `customerAuthenticationConfigurations.authType` | 字串 | 接受的值為 `OAUTH2, BEARER`. |
| `customerDataFields.name` | 字串 | 提供您要引入的自訂欄位名稱。 |
| `customerDataFields.type` | 字串 | 指出您要引入的自訂欄位類型。 接受的值為 `string`, `object`, `integer` |
| `customerDataFields.title` | 字串 | 指出欄位的名稱，如Experience Platform使用者介面中的客戶所見 |
| `customerDataFields.description` | 字串 | 提供自訂欄位的說明。 |
| `customerDataFields.isRequired` | 布林值 | 指示目標設定工作流中是否需要此欄位。 |
| `customerDataFields.enum` | 字串 | 將自訂欄位轉譯為下拉式功能表，並列出使用者可用的選項。 |
| `customerDataFields.pattern` | 字串 | 視需要為自訂欄位強制使用模式。 使用規則運算式來強制模式。 例如，若您的客戶ID未包含數字或底線，請輸入 `^[A-Za-z]+$` 在此欄位中。 |
| `uiAttributes.documentationLink` | 字串 | 指 [目的地目錄](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `https://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中 `YOURDESTINATION` 是您目的地的名稱。 對於名為Moviestar的目的地，您將使用 `https://www.adobe.com/go/destinations-moviestar-en`. 請注意，此連結只有在Adobe將您的目的地設為現時且檔案已發佈後才有效。 |
| `uiAttributes.category` | 字串 | 是指指派給Adobe Experience Platform中目的地的類別。 如需詳細資訊，請閱讀 [目標類別](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). 使用下列其中一個值： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | 字串 | `Server-to-server` 是目前唯一可用的選項。 |
| `uiAttributes.frequency` | 字串 | `Streaming` 是目前唯一可用的選項。 |
| `identityNamespaces.externalId.acceptsAttributes` | 布林值 | 指出客戶是否可將標準設定檔屬性對應至您正在設定的身分。 |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 布林值 | 指出客戶是否可對應屬於 [自訂命名空間](/help/identity-service/namespaces.md#manage-namespaces) 至您所設定的身分。 |
| `identityNamespaces.externalId.transformation` | 字串 | _範例設定中未顯示_. 例如，當 [!DNL Platform] 客戶有純電子郵件地址作為屬性，而您的平台僅接受雜湊電子郵件。 您可在此提供需要套用的轉換（例如，將電子郵件轉換為小寫，然後雜湊）。 |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 指出 [標準身分命名空間](/help/identity-service/namespaces.md#standard) （例如IDFA）客戶可對應至您所設定的身分。 <br> 使用 `acceptedGlobalNamespaces`，您可以使用 `"requiredTransformation":"sha256(lower($))"` 小寫和雜湊電子郵件地址或電話號碼。 |
| `destinationDelivery.authenticationRule` | 字串 | 指示方式 [!DNL Platform] 客戶可連線至您的目的地。 接受的值為 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客戶透過使用者名稱和密碼、承載權杖或其他驗證方法登入您的系統。 例如，如果您也選取了 `authType: OAUTH2` 或 `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe與目的地之間有全域驗證系統，則 [!DNL Platform] 客戶不需要提供任何驗證憑證來連線至您的目的地。 在此情況下，您必須使用 [憑證](./authentication-configuration.md) 設定。 </li><li>使用 `NONE` 若無需驗證即可將資料傳送至目的地平台。 </li></ul> |
| `destinationDelivery.destinationServerId` | 字串 | 此 `instanceId` 的 [目的地伺服器範本](./destination-server-api.md) 用於此目的地。 |
| `destConfigId` | 字串 | 此欄位會自動產生，不需要您輸入。 |
| `backfillHistoricalProfileData` | 布林值 | 控制在將區段啟動至目的地時，是否匯出歷史設定檔資料。 <br> <ul><li> `true`: [!DNL Platform] 傳送在啟用區段之前符合區段資格的歷史使用者設定檔。 </li><li> `false`: [!DNL Platform] 僅包含區段啟動後符合區段資格的使用者設定檔。 </li></ul> |
| `segmentMappingConfig.mapUserInput` | 布林值 | 控制使用者是否輸入目標啟動工作流程中的區段對應ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 布林值 | 控制目標啟動工作流程中的區段對應ID是否為Experience Platform區段ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 布林值 | 控制目標啟動工作流程中的區段對應ID是否為Experience Platform區段名稱。 |
| `segmentMappingConfig.audienceTemplateId` | 布林值 | 此 `instanceId` 的 [對象中繼資料範本](./audience-metadata-management.md) 用於此目的地。 若要設定對象中繼資料範本，請閱讀 [對象中繼資料API參考](./audience-metadata-api.md). |

{style="table-layout:auto"}

## 更新現有目標配置 {#update}

您可以向 `/authoring/destinations` 端點，並提供您要更新之目的地設定的例項ID。 在呼叫內文中，提供更新的目的地設定。

**API格式**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要更新的目標配置ID。 |

**要求**

下列要求會更新現有的目的地設定，由裝載中提供的參數所設定。 在以下範例呼叫中，我們會更新設定 [已建立較早](./destination-configuration-api.md#create) 現在接受GAID、IDFA和雜湊電子郵件識別碼做為身分識別命名空間。

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

## 擷取特定目的地設定 {#get}

您可以向提出GET要求，以擷取特定目標設定的詳細資訊 `/authoring/destinations` 端點，並提供您要擷取之目的地設定的例項ID。

**API格式**


```http
GET /authoring/destinations/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 您要擷取的目的地設定ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定目的地設定的詳細資訊。

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

您可以向發出DELETE要求，以刪除指定的目的地設定 `/authoring/destinations` 端點，並提供您要在請求路徑中刪除之目標設定的ID。

**API格式**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 此 `id` 刪除的目標配置。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回HTTP狀態200，並傳回空的HTTP回應。

## API錯誤處理

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟

閱讀本檔案後，您現在知道如何使用 `/authoring/destinations` API端點。 閱讀 [如何使用Destination SDK來設定您的目的地](./configure-destination-instructions.md) 了解此步驟在設定目的地程式中的適用位置。
