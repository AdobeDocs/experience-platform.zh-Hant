---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK擷取目的地發佈請求之詳細資料的API呼叫範例。
title: 擷取目的地發佈請求
exl-id: fceef12d-a52c-4259-a91e-7af88b132800
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 2%

---

# 擷取目的地發佈請求

>[!IMPORTANT]
>
>如果您要提交產品化（公用）目的地以供其他Experience Platform客戶使用，則只需使用此API端點即可。 如果您要建立私人目的地以供您自用，則不需要使用發佈API正式提交目的地。

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/destinations/publish`

設定並測試目的地後，您就可以將其提交至Adobe進行檢閱和發佈。 閱讀[針對在Destination SDK](../guides/submit-destination.md)中撰寫的目的地，提交以供檢閱作為目的地提交程式一部分而必須執行的所有其他步驟。

發生下列情況時，請使用發佈目的地API端點提交發佈請求：

* 身為Destination SDK合作夥伴，您想要讓所有Experience Platform組織都能使用您的產品化目的地，供所有Experience Platform客戶使用；
* 您對設定進行了&#x200B;*任何更新*。 只有在您提交經Experience Platform團隊核准的新發佈請求後，設定更新才會反映在目的地中。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都會區分大小寫&#x200B;****。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## Destination Publishing API操作快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 列出目的地發佈請求 {#retrieve-list}

您可以向`/authoring/destinations/publish`端點發出GET請求，以擷取為您的IMS組織提交的所有目的地清單。

**API格式**

使用下列API格式來擷取您帳戶的所有發佈請求。

```http
GET /authoring/destinations/publish
```

使用下列API格式來擷取由`{DESTINATION_ID}`引數定義的特定發佈要求。

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**要求**

以下兩個要求會擷取您IMS組織的所有發佈要求，或特定的發佈要求，端視您是否在要求中傳遞`DESTINATION_ID`引數而定。

選取下方的每個索引標籤以檢視對應的裝載。

>[!BEGINTABS]

>[!TAB 擷取所有發佈要求]

+++要求

下列請求將根據[!DNL IMS Org ID]和沙箱設定，擷取您提交的發佈請求清單。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++回應

以下回應會根據您使用的IMS組織ID和沙箱名稱，傳回HTTP狀態200，其中包含您有權存取的提交以進行發佈的所有目的地清單。 一個`configId`對應至一個目的地的發佈要求。

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"ab41387c0-4772-4709-a3ce-6d5fee654520",
         "allowedOrgs":[
            "716543205DB85F7F0A495E5B@AdobeOrg"
         ],
         "status":"TEST",
         "destinationType":"DEV"
      },
      {
         "configId":"cd568c67-f25e-47e4-b9a2-d79297a20b27",
         "allowedOrgs":[
            "*"
         ],
         "status":"DEPRECATED",
         "destinationType":"PUBLIC",
         "publishedDate":1630525501009
      },
      {
         "configId":"ef6f07154-09bc-4bee-8baf-828ea9c92fba",
         "allowedOrgs":[
            "*"
         ],
         "status":"PUBLISHED",
         "destinationType":"PUBLIC",
         "publishedDate":1630531586002
      }
   ]
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `destinationId` | 字串 | 您已提交發佈的目的地組態目的地ID。 |
| `publishDetailsList.configId` | 字串 | 您提交之目的地的目的地發佈要求唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字串 | 傳回目的地適用的Experience Platform組織。<br> <ul><li> 對於`"destinationType": "PUBLIC"`，此引數會傳回`"*"`，這表示所有Experience Platform組織都可以使用此目的地。</li><li> 針對`"destinationType": "DEV"`，此引數會傳回您用來製作及測試目的地的組織組織識別碼。</li></ul> |
| `publishDetailsList.status` | 字串 | 目的地發佈要求的狀態。 可能的值為`TEST`、`REVIEW`、`APPROVED`、`PUBLISHED`、`DENIED`、`REVOKED`、`DEPRECATED`。 值為`PUBLISHED`的目的地已上線，可供Experience Platform客戶使用。 |
| `publishDetailsList.destinationType` | 字串 | 目的地的型別。 值可以是`DEV`和`PUBLIC`。 `DEV`對應至您Experience Platform組織中的目的地。 `PUBLIC`對應於您已提交發佈的目的地。 以Git術語來思考這兩個選項，其中`DEV`版本代表您本機編寫分支，`PUBLIC`版本代表遠端主要分支。 |
| `publishDetailsList.publishedDate` | 字串 | 以紀元時間提交目的地以供發佈的日期。 |

{style="table-layout:auto"}

+++

>[!TAB 擷取特定發佈要求]

+++要求

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/{DESTINATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 您要擷取發佈狀態之目的地的ID。 |

+++

+++回應

如果您在API呼叫中傳遞`DESTINATION_ID`，回應會傳回HTTP狀態200，其中包含指定之目的地發佈要求的詳細資訊。

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"123cs780-ce29-434f-921e-4ed6ec2a6c35",
         "allowedOrgs": [
            "*"
         ],    
         "status":"PUBLISHED",
         "destinationType": "PUBLIC",
         "publishedDate":"1630617746"
      }
   ]
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `destinationId` | 字串 | 您已提交發佈的目的地組態目的地ID。 |
| `publishDetailsList.configId` | 字串 | 您提交之目的地的目的地發佈要求唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字串 | 傳回目的地適用的Experience Platform組織。<br> <ul><li> 對於`"destinationType": "PUBLIC"`，此引數會傳回`"*"`，這表示所有Experience Platform組織都可以使用此目的地。</li><li> 針對`"destinationType": "DEV"`，此引數會傳回您用來製作及測試目的地的組織組織識別碼。</li></ul> |
| `publishDetailsList.status` | 字串 | 目的地發佈要求的狀態。 可能的值為`TEST`、`REVIEW`、`APPROVED`、`PUBLISHED`、`DENIED`、`REVOKED`、`DEPRECATED`。 值為`PUBLISHED`的目的地已上線，可供Experience Platform客戶使用。 |
| `publishDetailsList.destinationType` | 字串 | 目的地的型別。 值可以是`DEV`和`PUBLIC`。 `DEV`對應至您Experience Platform組織中的目的地。 `PUBLIC`對應於您已提交發佈的目的地。 以Git術語來思考這兩個選項，其中`DEV`版本代表您本機編寫分支，`PUBLIC`版本代表遠端主要分支。 |
| `publishDetailsList.publishedDate` | 字串 | 以紀元時間提交目的地以供發佈的日期。 |

{style="table-layout:auto"}

+++

>[!ENDTABS]

## API錯誤處理

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Experience Platform疑難排解指南中的[API狀態碼](../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors)。
