---
description: 本頁列出並說明所有可透過「/authoring/destinations/publish」 API端點執行的API操作。
title: 發佈目標API端點作業
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 1fb0fde2054528679235268ae96e3b7e78de80ef
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 3%

---

# 發佈目標端點API操作 {#publish-destination}

>[!IMPORTANT]
>
>如果您要提交要供其他Experience Platform客戶使用的已分產品化（公開）目的地，則只需使用此API端點。 如果您要建立私人目的地供自己使用，則不需使用發佈API正式提交目的地。

>[!IMPORTANT]
>
>**API端點**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

此頁面列出並說明您可使用 `/authoring/destinations/publish` API端點。

設定並測試您的目的地後，您就可以將其提交至Adobe以進行審核和發佈。 閱讀 [提交以審核在Destination SDK中創作的目標](./submit-destination.md) 在目標提交程式中，您必須執行的所有其他步驟。

符合下列情形時，請使用發佈目標API端點提交發佈請求：

* 作為Destination SDK合作夥伴，您希望讓所有Experience Platform組織都能提供產品化目的地，供所有Experience Platform客戶使用；
* 你讓 *任何更新* 設定。 只有在您提交經Experience Platform團隊核准的新發佈請求後，設定更新才會反映在目的地中。

<!-- * You want to make your custom destination available in your own Experience Platform organization, across all sandboxes. -->

## 目的地發佈API作業快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 提交要發佈的目標配置 {#create}

您可以向提交POST請求，以提交要發佈的目標設定 `/authoring/destinations/publish` 端點。

**API格式**

```http
POST /authoring/destinations/publish
```

**要求**

下列要求會提交要發佈的目的地，涵蓋由裝載中提供的參數所設定的組織。 以下裝載包含接受的所有參數 `/authoring/destinations/publish` 端點。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `destinationId` | 字串 | 您要提交以進行發佈的目的地設定的目的地ID。 使用 [目的地設定API參考](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | 字串 | 使用 `ALL` 讓您的目的地出現在所有Experience Platform客戶的目錄中。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回HTTP狀態201，並包含目的地發佈請求的詳細資訊。

## 列出目標發佈請求 {#retrieve-list}

您可以向提出GET要求，以擷取所有提交供IMS組織發佈的目的地清單 `/authoring/destinations/publish` 端點。

**API格式**

```http
GET /authoring/destinations/publish
```

**要求**

下列請求會根據IMS組織和沙箱設定，擷取您有權存取的已提交以發佈目的地清單。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

下列回應會根據您使用的IMS組織ID和沙箱名稱，傳回HTTP狀態200，並附上您有權存取的發佈目的地清單。 一 `configId` 對應至一個目的地的發佈請求。

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
| `destinationId` | 字串 | 您提交以供發佈的目標配置的目標ID。 |
| `publishDetailsList.configId` | 字串 | 已提交目的地的目的地發佈請求的唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字串 | 傳回目標可用的Experience Platform組織。 <br> <ul><li> 針對 `"destinationType": "PUBLIC"`，此參數會傳回 `"*"`，這表示目的地可供所有Experience Platform組織使用。</li><li> 針對 `"destinationType": "DEV"`，此參數會傳回您用來製作和測試目的地之組織的組織ID。</li></ul> |
| `publishDetailsList.status` | 字串 | 目的地發佈請求的狀態。 可能的值包括 `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. 具有值的目的地 `PUBLISHED` 即時，可供Experience Platform客戶使用。 |
| `publishDetailsList.destinationType` | 字串 | 目的地的類型。 值可以是 `DEV` 和 `PUBLIC`. `DEV` 對應至Experience Platform組織中的目的地。 `PUBLIC` 對應至您提交以供發佈的目的地。 以Git術語來思考這兩個選項， `DEV` 版本代表您的本機製作分支和 `PUBLIC` 版本代表遠端主分支。 |
| `publishDetailsList.publishedDate` | 字串 | 目的地提交以進行發佈的日期（以紀元時間為單位）。 |

{style="table-layout:auto"}

## 取得特定目標發佈請求的狀態 {#get}

您可以向提出GET請求，以擷取特定目標發佈請求的詳細資訊 `/authoring/destinations/publish` 端點，並提供您要擷取發佈狀態之目的地的ID。

**API格式**

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 您要擷取發佈狀態的目的地ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定目的地發佈請求的詳細資訊。

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

## API錯誤處理

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟

閱讀本檔案後，您現在知道如何提交目的地的發佈請求。 Adobe Experience Platform團隊將檢閱您的發佈請求，並在5個工作天內回覆給您。
