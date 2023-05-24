---
description: 瞭解如何通過Adobe Experience Platform Destination SDK構造API調用以建立目標配置。
title: 建立目標配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 3%

---


# 建立目標配置

本頁說明了API請求和負載，您可以使用 `/authoring/destinations` API終結點。

有關可以通過此端點配置的功能的詳細說明，請閱讀以下文章：

* [客戶身份驗證配置](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth2身份驗證](../../functionality/destination-configuration/oauth2-authentication.md)
* [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md)
* [UI屬性](../../functionality/destination-configuration/ui-attributes.md)
* [架構配置](../../functionality/destination-configuration/schema-configuration.md)
* [標識命名空間配置](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [目標傳遞](../../functionality/destination-configuration/destination-delivery.md)
* [受眾元資料配置](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [受眾元資料配置](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [聚合策略](../../functionality/destination-configuration/aggregation-policy.md)
* [批配置](../../functionality/destination-configuration/batch-configuration.md)
* [歷史配置檔案資格](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 目標配置API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](../../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 建立目標配置 {#create}

您可以通過向POST請求建立新的目標配置 `/authoring/destinations` 端點。

>[!TIP]
>
>**API終結點**: `platform.adobe.io/data/core/activation/authoring/destinations`

**API格式**

```http
POST /authoring/destinations
```

以下請求將建立新 [!DNL Amazon S3] 目標配置，由負載中提供的參數配置。 以下負載包括接受的基於檔案的目標的所有參數 `/authoring/destinations` 端點。

請注意，您不必向API調用添加所有參數，並且負載可根據API要求進行自定義。

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
| `name` | 字串 | 指示Experience Platform目錄中目標的標題。 |
| `description` | 字串 | 提供Adobe將用於目標卡的Experience Platform目標目錄的說明。 目標不超過4-5句。 ![顯示目標說明的平台UI映像。](../../assets/authoring-api/destination-configuration/destination-description.png "目標描述"){width="100" zoomable="yes"} |
| `status` | 字串 | 指示目標卡的生命週期狀態。 接受的值為 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 在首次配置目標時。 |
| `customerAuthenticationConfigurations.authType` | 字串 | 指示用於將Experience Platform客戶驗證到目標伺服器的配置。 請參閱 [客戶驗證配置](../../functionality/destination-configuration/customer-authentication.md) 的子菜單。 |
| `customerDataFields.name` | 字串 | 提供要引入的自定義欄位的名稱。 <br/><br/> 請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 的子菜單。 ![顯示客戶資料欄位的平台UI映像。](../../assets/authoring-api/destination-configuration/customer-data-fields.png "客戶資料欄位"){width="100" zoomable="yes"} |
| `customerDataFields.type` | 字串 | 指示您要引入的自定義欄位類型。 接受的值為 `string`。 `object`。 `integer`。 <br/><br/> 請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 的子菜單。 |
| `customerDataFields.title` | 字串 | 指示欄位的名稱，如客戶在Experience Platform用戶介面中看到的。 <br/><br/> 請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 的子菜單。 |
| `customerDataFields.description` | 字串 | 提供自定義欄位的說明。 請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 的子菜單。 |
| `customerDataFields.isRequired` | 布林值 | 指示目標設定工作流中是否需要此欄位。 <br/><br/> 請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 的子菜單。 |
| `customerDataFields.enum` | 字串 | 將自定義欄位呈現為下拉菜單並列出用戶可用的選項。 <br/><br/> 請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 的子菜單。 |
| `customerDataFields.default` | 字串 | 從 `enum` 清單框。 |
| `customerDataFields.pattern` | 字串 | 如果需要，為自定義欄位強制實施模式。 使用規則運算式來強制模式。 例如，如果客戶ID不包括數字或下划線，請輸入 `^[A-Za-z]+$` 的子菜單。 <br/><br/> 請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 的子菜單。 |
| `uiAttributes.documentationLink` | 字串 | 引用中的文檔頁面 [目標目錄](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `https://www.adobe.com/go/destinations-YOURDESTINATION-en`，也請參見Wiki頁。 `YOURDESTINATION` 是目標的名稱。 對於名為Moviestar的目標，您將使用 `https://www.adobe.com/go/destinations-moviestar-en`。 請注意，此連結僅在Adobe設定目標即時並發佈文檔後才起作用。 <br/><br/> 請參閱 [UI屬性](../../functionality/destination-configuration/ui-attributes.md) 的子菜單。 ![顯示文檔連結的平台UI影像。](../../assets/authoring-api/destination-configuration/documentation-url.png "文檔URL"){width="100" zoomable="yes"} |
| `uiAttributes.category` | 字串 | 指分配給您在Adobe Experience Platform的目標的類別。 有關詳細資訊，請閱讀 [目標類別](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories)。 使用以下值之一： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`。 <br/><br/> 請參閱 [UI屬性](../../functionality/destination-configuration/ui-attributes.md) 的子菜單。 |
| `uiAttributes.connectionType` | 字串 | 連接類型（取決於目標）。 支援的值： <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | 字串 | 引用目標支援的資料導出類型。 設定為 `Streaming` 用於基於API的整合，或 `Batch` 將檔案導出到目標。 |
| `identityNamespaces.externalId.acceptsAttributes` | 布林值 | 指示客戶是否可以將標準配置檔案屬性映射到您正在配置的標識。 |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 布林值 | 指示客戶是否可以映射屬於 [自定義命名空間](/help/identity-service/namespaces.md#manage-namespaces) 到您正在配置的標識。 |
| `identityNamespaces.externalId.transformation` | 字串 | _未在示例配置中顯示_。 例如，在 [!DNL Platform] 客戶將純電子郵件地址作為屬性，而您的平台只接受經過散列的電子郵件。 您將在此處提供需要應用的轉換（例如，將電子郵件轉換為小寫，然後進行散列）。 |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 指示 [標準標識命名空間](/help/identity-service/namespaces.md#standard) （例如，IDFA）客戶可以映射到您正在配置的標識。 <br> 使用 `acceptedGlobalNamespaces`，您可以使用 `"requiredTransformation":"sha256(lower($))"` 到小寫和散列電子郵件地址或電話號碼。 |
| `destinationDelivery.authenticationRule` | 字串 | 指示如何 [!DNL Platform] 客戶連接到您的目標。 接受的值為 `CUSTOMER_AUTHENTICATION`。 `PLATFORM_AUTHENTICATION`。 `NONE`。 <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果平台客戶通過用戶名和密碼、持有者令牌或其他身份驗證方法登錄到您的系統。 例如，如果同時選擇了 `authType: OAUTH2` 或 `authType:BEARER` 在 `customerAuthenticationConfigurations`。 </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe與目標之間有全局身份驗證系統， [!DNL Platform] 客戶不需要提供任何身份驗證憑據來連接到目標。 在這種情況下，必須使用 [憑據API](../../credentials-api/create-credential-configuration.md) 配置。 </li><li>使用 `NONE` 如果向目標平台發送資料不需要身份驗證。 </li></ul> |
| `destinationDelivery.destinationServerId` | 字串 | 的 `instanceId` 的 [目標伺服器模板](../destination-server/create-destination-server.md) 用於此目標。 |
| `backfillHistoricalProfileData` | 布林值 | 控制在將段激活到目標時是否導出歷史配置檔案資料。 始終將此設定為 `true`。 |
| `segmentMappingConfig.mapUserInput` | 布林值 | 控制用戶是否輸入目標激活工作流中的段映射ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 布林值 | 控制目標激活工作流中的段映射ID是否是Experience Platform段ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 布林值 | 控制目標激活工作流中的段映射ID是否是Experience Platform段名稱。 |
| `segmentMappingConfig.audienceTemplateId` | 布林值 | 的 `instanceId` 的 [受眾元資料模板](../../metadata-api/create-audience-template.md) 用於此目標。 |
| `schemaConfig.profileFields` | 陣列 | 添加預定義項時 `profileFields` 如上面的配置所示，用戶可以選擇將Experience Platform屬性映射到目標側的預定義屬性。 |
| `schemaConfig.profileRequired` | 布林值 | 使用 `true` 如果用戶應能將配置檔案屬性從Experience Platform映射到目標側的自定義屬性，如上面的示例配置所示。 |
| `schemaConfig.segmentRequired` | 布林值 | 始終使用 `segmentRequired:true`。 |
| `schemaConfig.identityRequired` | 布林值 | 使用 `true` 如果用戶應能夠將標識命名空間從Experience Platform映射到所需的架構。 |

{style="table-layout:auto"}

+++

+++回應

成功的響應返回HTTP狀態200，其中包含您新建立的目標配置的詳細資訊。

+++

## API錯誤處理

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟

閱讀此文檔後，您現在知道如何通過Destination SDK建立新的目標配置 `/authoring/destinations` API終結點。

要瞭解有關可以使用此端點執行什麼操作的詳細資訊，請參閱以下文章：

* [檢索目標配置](retrieve-destination-configuration.md)
* [更新目標配置](update-destination-configuration.md)
* [刪除目標配置](delete-destination-configuration.md)

要瞭解此端點在目標創作流程中的位置，請參閱以下文章：

* [使用Destination SDK配置流目標](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
