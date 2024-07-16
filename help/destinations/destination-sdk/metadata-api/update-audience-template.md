---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK更新對象範本的API呼叫的範例。
title: 更新對象範本
exl-id: 8185a015-256d-46a7-af33-8475832fb6c1
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---

# 更新對象範本

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/audience-templates`

此頁面以範例說明API要求與承載，您可以使用`/authoring/audience-templates` API端點來更新對象範本。

如需您可以透過此端點設定的功能的詳細說明，請參閱[對象中繼資料管理](../functionality/audience-metadata-management.md)。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都區分大小寫&#x200B;****。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 對象範本API操作快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 更新對象範本 {#create}

您可以透過對具有更新承載的`/authoring/audience-templates`端點發出`PUT`請求來更新[現有](create-audience-template.md)對象範本。

若要取得現有的對象範本及其對應的`{INSTANCE_ID}`，請參閱有關[擷取對象範本](retrieve-audience-template.md)的文章。

**API格式**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 您要更新之對象範本的ID。 若要取得現有的對象範本及其對應的`{INSTANCE_ID}`，請參閱[擷取對象範本](retrieve-audience-template.md)。 |

以下請求會更新現有的對象中繼資料範本，此範本已根據承載中提供的引數設定。

+++要求

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1.0/{{customerData.accountId}}/customaudiences?fields=name,description,account_id&subtype=CUSTOM&name={{segment.name}}&customer_file_source={{segment.metadata.customer_file_source}}&access_token={{authData.accessToken}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?field=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}&&name={{segment.name}}&description={{segment.description}}&customer_file_source={{segment.metadata.customer_file_source}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?fields=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "validate":{
         "url":"https://api.moviestar.com/v1.0/permissions?access_token={{authData.accessToken}}",
         "httpMethod":"GET",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.data[0].permission}}",
               "name":"Id"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      }
   }
}'
```

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新對象範本的詳細資料。

+++

## API錯誤處理

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Platform疑難排解指南中的[API狀態碼](../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟

閱讀本檔案後，您現在知道何時該使用對象範本，以及如何使用`/authoring/audience-templates` API端點更新對象範本。 閱讀[如何使用Destination SDK來設定您的目的地](../guides/configure-destination-instructions.md)，以瞭解此步驟在設定目的地的過程中適合到什麼位置。
