---
description: 本頁說明了通過Adobe Experience Platform Destination SDK建立受眾模板的API調用。
title: 建立受眾模板
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 3%

---


# 建立受眾模板

>[!IMPORTANT]
>
>**API終結點**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

對於使用Destination SDK建立的某些目標，您需要建立訪問群體元資料配置以寫程式方式在目標中建立、更新或刪除段元資料。 此頁顯示如何使用 `/authoring/audience-templates` 用於建立配置的API終結點。

有關可以通過此終結點配置的功能的詳細說明，請參見 [受眾元資料管理](../functionality/audience-metadata-management.md)。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 受眾模板API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 建立受眾模板 {#create}

通過建立 `POST` 請求 `/authoring/audience-templates` 端點。

**API格式**

```http
POST /authoring/audience-templates
```

+++請求

以下請求將建立由負載中提供的參數配置的新受眾模板。 下面的負載包括接受的所有參數 `/authoring/audience-templates` 端點。 請注意，您不必在調用中添加所有參數，並且模板可根據API要求進行自定義。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "notify":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      }
   },
   "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| 屬性 | 類型 | 說明 |
| -------- | ----------- | ----------- |
| `name` | 字串 | 目標的受眾元資料模板的名稱。 此名稱將出現在Experience Platform用戶介面中特定於合作夥伴的任何錯誤消息中，然後是從中分析的錯誤消息 `metadataTemplate.create.errorSchemaMap`。 |
| `url` | 字串 | API的URL和終結點，用於建立、更新、刪除或驗證平台中的受眾/段。 兩個行業示例： `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` 和 `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`。 |
| `httpMethod` | 字串 | 端點上用於以寫程式方式建立、更新、刪除或驗證目標中的段/受眾的方法。 例如: `POST`, `PUT`, `DELETE` |
| `headers.header` | 字串 | 指定應添加到對API的調用的任何HTTP標頭。 例如, `"Content-Type"` |
| `headers.value` | 字串 | 指定應添加到對API的調用的HTTP標頭的值。 例如, `"application/x-www-form-urlencoded"` |
| `requestBody` | 字串 | 指定應發送到API的消息正文的內容。 應添加到的參數 `requestBody` 對象取決於API接受的欄位。 例如，請參閱 [第一個模板示例](../functionality/audience-metadata-management.md#example-1) 在「受眾元資料」功能文檔中。 |
| `responseFields.name` | 字串 | 指定調用API時返回的任何響應欄位。 例如，請參閱 [模板示例](../functionality/audience-metadata-management.md#examples) 在「受眾元資料」功能文檔中。 |
| `responseFields.value` | 字串 | 指定調用API時返回的任何響應欄位的值。 |
| `responseErrorFields.name` | 字串 | 指定調用API時返回的任何響應欄位。 例如，請參閱 [ 模板示例](../functionality/audience-metadata-management.md#examples) 在「受眾元資料」功能文檔中。 |
| `responseErrorFields.value` | 字串 | 解析從目標API調用響應返回的任何錯誤消息。 這些錯誤消息將出現給Experience Platform用戶介面中的用戶。 |
| `validations.field` | 字串 | 指示在對目標進行API調用之前是否應為任何欄位運行驗證。 例如，您可以 `{{validations.accountId}}` 驗證用戶的帳戶ID。 |
| `validations.regex` | 字串 | 指示如何構造欄位以便驗證通過。 |

{style="table-layout:auto"}

+++

+++回應

成功的響應返回HTTP狀態200，其中包含新建立的受眾模板的詳細資訊。

+++

## API錯誤處理

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟

閱讀此文檔後，您現在知道何時使用受眾模板以及如何使用 `/authoring/audience-templates` API終結點。 閱讀 [如何使用Destination SDK配置目標](../guides/configure-destination-instructions.md) 瞭解此步驟在配置目標過程中的適用範圍。
