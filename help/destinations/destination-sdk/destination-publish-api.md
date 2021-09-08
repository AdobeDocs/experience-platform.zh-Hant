---
description: 本頁列出並說明所有可透過「/authoring/destinations/publish」 API端點執行的API操作。
title: 發佈目標API端點作業
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 4%

---

# 發佈目標端點API操作 {#publish-destination}

>[!IMPORTANT]
>
>**API端點**:  `platform.adobe.io/data/core/activation/authoring/destinations/publish`

本頁列出並說明了所有可使用`/authoring/destinations/publish` API端點執行的API操作。

設定並測試您的目的地後，您就可以將其提交至Adobe以進行審核和發佈。

符合下列情形時，請使用發佈目標API端點提交發佈請求：
* 作為目的地SDK合作夥伴，您想要讓所有Experience Platform組織中都可使用已產品化的目的地，供所有Experience Platform客戶使用；
* 您想要讓自訂目的地可在您自己的Experience Platform組織中使用，且可跨所有沙箱使用。

## 目的地發佈API作業快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](./getting-started.md)，以取得成功呼叫API所需的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 提交要發佈的目標配置 {#create}

您可以向`/authoring/destinations/publish`端點提出POST請求，以提交要發佈的目標配置。

**API格式**


```http
POST /authoring/destinations/publish
```

**要求**

下列要求會提交要發佈的目的地，涵蓋由裝載中提供的參數所設定的組織。 以下裝載包含`/authoring/destinations/publish`端點接受的所有參數。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "xyz@AdobeOrg",
      "lmn@AdobeOrg"
   ]
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `destinationId` | 字串 | 您要提交以進行發佈的目的地設定的目的地ID。 使用[目標配置API參考](./destination-configuration-api.md#retrieve-list)獲取目標配置的目標ID。 |
| `destinationAccess` | 字串 | `ALL` 或 `LIMITED`. 指定您要讓所有Experience Platform客戶或特定組織的目的地顯示在目錄中。<br> **注意**:如果您使 `LIMITED`用，則只會針對您的Experience Platform組織發佈目的地。如果您想要將目的地發佈至Experience Platform組織的子集合以進行客戶測試，請聯絡Adobe支援。 |
| `allowedOrgs` | 字串 | 如果您使用`"destinationAccess":"LIMITED"`，請指定目標可用的Experience Platform組織。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回HTTP狀態201，並包含目的地發佈請求的詳細資訊。

## 列出目標發佈請求 {#retrieve-list}

您可以向`/authoring/destinations/publish`端點提出GET請求，以擷取所有提交供IMS組織發佈的目的地清單。

**API格式**


```http
GET /authoring/destinations/publish
```

**要求**

下列請求會根據IMS組織和沙箱設定，擷取您有權存取的已提交以發佈目的地清單。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

下列回應會根據您使用的IMS組織ID和沙箱名稱，傳回HTTP狀態200，並附上您有權存取的發佈目的地清單。 一個`configId`對應於一個目的地的發佈請求。

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"1630617746"
      }
   ]
}
    
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `destinationId` | 字串 | 您已提交以供發佈的目標配置的目標ID。 |
| `publishDetailsList.configId` | 字串 | 已提交目的地的目的地發佈請求的唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字串 | 傳回目標應可用的Experience Platform組織。 |
| `publishDetailsList.status` | 字串 | 目的地發佈請求的狀態。 可能的值為`TEST`、`REVIEW`、`APPROVED`、`PUBLISHED`、`DENIED`、`REVOKED`、`DEPRECATED`。 |
| `publishDetailsList.publishedDate` | 字串 | 提交目的地以進行發佈的日期（以紀元時間為單位）。 |

## 更新現有的目標發佈請求 {#update}

您可以向`/authoring/destinations/publish`端點提出PUT請求，並提供要更新允許組織的目標ID，以更新現有目標發佈請求中允許的組織。 在呼叫內文中，提供更新的允許組織。

**API格式**


```http
PUT /authoring/destinations/publish/{DESTINATION_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 您要更新發佈請求的目的地ID。 |

**要求**

下列請求會更新現有的目的地發佈請求，由裝載中提供的參數所設定。 在以下範例呼叫中，我們正在更新允許的組織。

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "abc@AdobeOrg",
      "def@AdobeOrg"
   ]
}
```

## 取得特定目標發佈請求的狀態 {#get}

您可以向`/authoring/destinations/publish`端點提出GET請求，並提供您要擷取發佈狀態之目標的ID，以擷取特定目標發佈請求的詳細資訊。

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"string"
      }
   ]
}
```

## API錯誤處理

目標SDK API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱平台疑難排解指南中的[API狀態代碼](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes)和[要求標題錯誤](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors)。

## 後續步驟

閱讀本檔案後，您現在知道如何提交目的地的發佈請求。 Adobe Experience Platform團隊將檢閱您的發佈請求，並在5個工作天內回覆給您。
