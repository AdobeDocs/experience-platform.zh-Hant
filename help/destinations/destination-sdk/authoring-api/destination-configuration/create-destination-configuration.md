---
description: 了解如何透過Adobe Experience Platform Destination SDK來建構API呼叫，以建立目的地設定。
title: 建立目標配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 3%

---


# 建立目標配置

此頁面是API要求和裝載的範例，您可使用來建立自己的目的地設定 `/authoring/destinations` API端點。

如需可透過此端點設定之功能的詳細說明，請參閱下列文章：

* [客戶驗證配置](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth2驗證](../../functionality/destination-configuration/oauth2-authentication.md)
* [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md)
* [UI屬性](../../functionality/destination-configuration/ui-attributes.md)
* [結構配置](../../functionality/destination-configuration/schema-configuration.md)
* [身分命名空間設定](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [目的地傳送](../../functionality/destination-configuration/destination-delivery.md)
* [對象中繼資料設定](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [對象中繼資料設定](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [聚合策略](../../functionality/destination-configuration/aggregation-policy.md)
* [批次設定](../../functionality/destination-configuration/batch-configuration.md)
* [歷史設定檔資格](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 目標設定API操作快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 建立目標配置 {#create}

您可以向 `/authoring/destinations` 端點。

>[!TIP]
>
>**API端點**: `platform.adobe.io/data/core/activation/authoring/destinations`

**API格式**

```http
POST /authoring/destinations
```

下列請求會建立新 [!DNL Amazon S3] 目的地設定，由裝載中提供的參數設定。 以下裝載包含接受之檔案式目的地的所有參數 `/authoring/destinations` 端點。

請注意，您不必將所有參數新增至API呼叫，而且可根據您的API需求自訂裝載。

+++請求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
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
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
      "icon":{
         "key":"amazonS3"
      },
      "connectionType":"S3",
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
   "schemaConfig":{
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
}'
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `name` | 字串 | 指出Experience Platform目錄中的目的地標題。 |
| `description` | 字串 | 提供說明，供Adobe用於目的地卡的Experience Platform目的地目錄。 目標不超過4-5句。 ![顯示目的地說明的平台UI影像。](../../assets/authoring-api/destination-configuration/destination-description.png "目的地說明"){width="100" zoomable="yes"} |
| `status` | 字串 | 指示目標卡的生命週期狀態。 接受的值為 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 設定目的地時。 |
| `customerAuthenticationConfigurations.authType` | 字串 | 指示用於驗證Experience Platform客戶到目標伺服器的配置。 請參閱 [客戶驗證設定](../../functionality/destination-configuration/customer-authentication.md) 以取得支援驗證類型的詳細資訊。 |
| `customerDataFields.name` | 字串 | 提供您要引入的自訂欄位名稱。 <br/><br/> 請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 以取得這些設定的詳細資訊。 ![顯示客戶資料欄位的Platform UI影像。](../../assets/authoring-api/destination-configuration/customer-data-fields.png "客戶資料欄位"){width="100" zoomable="yes"} |
| `customerDataFields.type` | 字串 | 指出您要引入的自訂欄位類型。 接受的值為 `string`, `object`, `integer`. <br/><br/> 請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 以取得這些設定的詳細資訊。 |
| `customerDataFields.title` | 字串 | 指出欄位的名稱，如Experience Platform使用者介面中的客戶所見。 <br/><br/> 請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 以取得這些設定的詳細資訊。 |
| `customerDataFields.description` | 字串 | 提供自訂欄位的說明。 請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 以取得這些設定的詳細資訊。 |
| `customerDataFields.isRequired` | 布林值 | 指示目標設定工作流中是否需要此欄位。 <br/><br/> 請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 以取得這些設定的詳細資訊。 |
| `customerDataFields.enum` | 字串 | 將自訂欄位轉譯為下拉式功能表，並列出使用者可用的選項。 <br/><br/> 請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 以取得這些設定的詳細資訊。 |
| `customerDataFields.default` | 字串 | 從 `enum` 清單。 |
| `customerDataFields.pattern` | 字串 | 視需要為自訂欄位強制使用模式。 使用規則運算式來強制模式。 例如，若您的客戶ID未包含數字或底線，請輸入 `^[A-Za-z]+$` 在此欄位中。 <br/><br/> 請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 以取得這些設定的詳細資訊。 |
| `uiAttributes.documentationLink` | 字串 | 指 [目的地目錄](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `https://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中 `YOURDESTINATION` 是您目的地的名稱。 對於名為Moviestar的目的地，您將使用 `https://www.adobe.com/go/destinations-moviestar-en`. 請注意，此連結只有在Adobe將您的目的地設為現時且檔案已發佈後才有效。 <br/><br/> 請參閱 [UI屬性](../../functionality/destination-configuration/ui-attributes.md) 以取得這些設定的詳細資訊。 ![顯示檔案連結的Platform UI影像。](../../assets/authoring-api/destination-configuration/documentation-url.png "檔案URL"){width="100" zoomable="yes"} |
| `uiAttributes.category` | 字串 | 是指指派給Adobe Experience Platform中目的地的類別。 如需詳細資訊，請閱讀 [目標類別](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). 使用下列其中一個值： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br/><br/> 請參閱 [UI屬性](../../functionality/destination-configuration/ui-attributes.md) 以取得這些設定的詳細資訊。 |
| `uiAttributes.connectionType` | 字串 | 連線類型（視目的地而定）。 支援的值： <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | 字串 | 是指目的地支援的資料匯出類型。 設為 `Streaming` （適用於API型整合），或 `Batch` 將檔案匯出至目的地時。 |
| `identityNamespaces.externalId.acceptsAttributes` | 布林值 | 指出客戶是否可將標準設定檔屬性對應至您正在設定的身分。 |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 布林值 | 指出客戶是否可對應屬於 [自訂命名空間](/help/identity-service/namespaces.md#manage-namespaces) 至您所設定的身分。 |
| `identityNamespaces.externalId.transformation` | 字串 | _範例設定中未顯示_. 例如，當 [!DNL Platform] 客戶有純電子郵件地址作為屬性，而您的平台僅接受雜湊電子郵件。 您可在此提供需要套用的轉換（例如，將電子郵件轉換為小寫，然後雜湊）。 |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 指出 [標準身分命名空間](/help/identity-service/namespaces.md#standard) （例如IDFA）客戶可對應至您所設定的身分。 <br> 使用 `acceptedGlobalNamespaces`，您可以使用 `"requiredTransformation":"sha256(lower($))"` 小寫和雜湊電子郵件地址或電話號碼。 |
| `destinationDelivery.authenticationRule` | 字串 | 指示方式 [!DNL Platform] 客戶可連線至您的目的地。 接受的值為 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客戶透過使用者名稱和密碼、承載權杖或其他驗證方法登入您的系統。 例如，如果您也選取了 `authType: OAUTH2` 或 `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe與目的地之間有全域驗證系統，則 [!DNL Platform] 客戶不需要提供任何驗證憑證來連線至您的目的地。 在此情況下，您必須使用 [認證API](../../credentials-api/create-credential-configuration.md) 設定。 </li><li>使用 `NONE` 若無需驗證即可將資料傳送至目的地平台。 </li></ul> |
| `destinationDelivery.destinationServerId` | 字串 | 此 `instanceId` 的 [目的地伺服器範本](../destination-server/create-destination-server.md) 用於此目的地。 |
| `backfillHistoricalProfileData` | 布林值 | 控制在將區段啟動至目的地時，是否匯出歷史設定檔資料。 請一律將此設為 `true`. |
| `segmentMappingConfig.mapUserInput` | 布林值 | 控制使用者是否輸入目標啟動工作流程中的區段對應ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 布林值 | 控制目標啟動工作流程中的區段對應ID是否為Experience Platform區段ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 布林值 | 控制目標啟動工作流程中的區段對應ID是否為Experience Platform區段名稱。 |
| `segmentMappingConfig.audienceTemplateId` | 布林值 | 此 `instanceId` 的 [對象中繼資料範本](../../metadata-api/create-audience-template.md) 用於此目的地。 |
| `schemaConfig.profileFields` | 陣列 | 新增預先定義的 `profileFields` 如上方的設定所示，使用者將可以選擇將Experience Platform屬性對應至目的地端的預先定義屬性。 |
| `schemaConfig.profileRequired` | 布林值 | 使用 `true` 如果使用者應能將設定檔屬性從Experience Platform對應至目的地端的自訂屬性，如上方的範例設定所示。 |
| `schemaConfig.segmentRequired` | 布林值 | 一律使用 `segmentRequired:true`. |
| `schemaConfig.identityRequired` | 布林值 | 使用 `true` 如果您的使用者應能將身分識別命名空間從Experience Platform對應至您想要的架構。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含您新建立之目的地組態的詳細資訊。

+++

## API錯誤處理

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟

閱讀本檔案後，您現在知道如何透過Destination SDK建立新的目的地設定 `/authoring/destinations` API端點。

若要進一步了解您可以使用此端點執行的操作，請參閱下列文章：

* [檢索目標配置](retrieve-destination-configuration.md)
* [更新目標配置](update-destination-configuration.md)
* [刪除目標配置](delete-destination-configuration.md)

若要了解此端點在目標製作程式中的適用位置，請參閱下列文章：

* [使用Destination SDK來設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
