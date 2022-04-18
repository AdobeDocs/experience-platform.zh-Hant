---
description: 此頁列出並說明了可以使用「/authoring/destination/publish」 API終結點執行的所有API操作。
title: 發佈目標API終結點操作
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: a73a4ea93a432f60d62da5e234d8e357009b2d88
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 4%

---

# 發佈目標終結點API操作 {#publish-destination}

>[!IMPORTANT]
>
>**API終結點**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

此頁列出並說明了可以使用 `/authoring/destinations/publish` API終結點。

配置和測試目標後，您可以將其提交給Adobe以進行審閱和發佈。 閱讀 [提交以審閱在Destination SDK中創作的目標](./submit-destination.md) 對於作為目標提交流程的一部分必須執行的所有其他步驟。

在以下情況下，使用發佈目標API終結點提交發佈請求：

* 作為Destination SDK合作夥伴，您希望使所有Experience Platform組織中的產品化目標都可用於所有Experience Platform客戶；
* 您希望在您自己的Experience Platform組織中跨所有沙箱提供自定義目標。
* 你 *任何更新* 配置。 配置更新僅在您提交新發佈請求後才反映在目標中，新發佈請求已獲得Experience Platform團隊的批准。

## 目標發佈API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](./getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 提交要發佈的目標配置 {#create}

通過向發佈伺服器發出POST請求，可以提交要發佈的目標配置 `/authoring/destinations/publish` 端點。

**API格式**

```http
POST /authoring/destinations/publish
```

**要求**

以下請求將提交一個目標，以便跨由負載中提供的參數配置的組織發佈。 下面的負載包括接受的所有參數 `/authoring/destinations/publish` 端點。

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
   "destinationAccess":"ALL"
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `destinationId` | 字串 | 要提交以發佈的目標配置的目標ID。 使用 [目標配置API參考](./destination-configuration-api.md#retrieve-list)。 |
| `destinationAccess` | 字串 | 使用 `ALL` 目標在所有Experience Platform客戶的目錄中。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的響應返回HTTP狀態201，其中包含目標發佈請求的詳細資訊。

## 列出目標發佈請求 {#retrieve-list}

通過向IMS組織發出GET請求，您可以檢索為發佈而提交的所有目標的清單 `/authoring/destinations/publish` 端點。

**API格式**

```http
GET /authoring/destinations/publish
```

**要求**

以下請求將根據IMS組織和沙盒配置檢索您有權訪問的已提交發佈的目標清單。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

以下響應將返回HTTP狀態200，其中根據您使用的IMS組織ID和沙盒名稱，列出您有權訪問的已提交發佈目標。 一 `configId` 對應於一個目標的發佈請求。

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
| `destinationId` | 字串 | 已提交用於發佈的目標配置的目標ID。 |
| `publishDetailsList.configId` | 字串 | 已提交目標的目標發佈請求的唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字串 | 返回目標可用的Experience Platform組織。 <br> <ul><li> 對於 `"destinationType": "PUBLIC"`，此參數將返回 `"*"`，這意味著目標可用於所有Experience Platform組織。</li><li> 對於 `"destinationType": "DEV"`，此參數返回您用於建立和test目標的組織的組織ID。</li></ul> |
| `publishDetailsList.status` | 字串 | 目標發佈請求的狀態。 可能的值為 `TEST`。 `REVIEW`。 `APPROVED`。 `PUBLISHED`。 `DENIED`。 `REVOKED`。 `DEPRECATED`。 具有值的目標 `PUBLISHED` 可供Experience Platform客戶使用。 |
| `publishDetailsList.destinationType` | 字串 | 目標類型。 值可以是 `DEV` 和 `PUBLIC`。 `DEV` 對應於您的Experience Platform組織中的目標。 `PUBLIC` 與您已提交用於發佈的目標相對應。 用Git的話來想這兩個選擇 `DEV` 版本表示本地創作分支和 `PUBLIC` 版本表示遠程主分支。 |
| `publishDetailsList.publishedDate` | 字串 | 提交目標以進行發佈的日期（以大紀元為單位）。 |

{style=&quot;table-layout:auto&quot;&quot;

## 獲取特定目標發佈請求的狀態 {#get}

您可以通過向以下站點發出GET請求來檢索有關特定目標發佈請求的詳細資訊 `/authoring/destinations/publish` 終結點，並提供要檢索其發佈狀態的目標的ID。

**API格式**

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 要檢索其發佈狀態的目標的ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關指定目標發佈請求的詳細資訊。

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

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟

閱讀此文檔後，您現在知道如何提交目標的發佈請求。 Adobe Experience Platform團隊將審閱您的發佈請求，並在5個工作日後回復您。
