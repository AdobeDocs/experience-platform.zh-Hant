---
description: 本頁面是API呼叫的範例，用於透過Adobe Experience Platform Destination SDK擷取目的地發佈請求的詳細資訊。
title: 擷取目的地發佈請求
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 2%

---


# 擷取目的地發佈請求

>[!IMPORTANT]
>
>如果您要提交要供其他Experience Platform客戶使用的已分產品化（公開）目的地，則只需使用此API端點。 如果您要建立私人目的地供自己使用，則不需使用發佈API正式提交目的地。

>[!IMPORTANT]
>
>**API端點**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

設定並測試您的目的地後，您就可以將其提交至Adobe以進行審核和發佈。 閱讀 [提交以審核在Destination SDK中創作的目標](../guides/submit-destination.md) 在目標提交程式中，您必須執行的所有其他步驟。

符合下列情形時，請使用發佈目標API端點提交發佈請求：

* 作為Destination SDK合作夥伴，您希望讓所有Experience Platform組織都能提供產品化目的地，供所有Experience Platform客戶使用；
* 你讓 *任何更新* 設定。 只有在您提交經Experience Platform團隊核准的新發佈請求後，設定更新才會反映在目的地中。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 目的地發佈API作業快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 列出目標發佈請求 {#retrieve-list}

您可以向提出GET要求，以擷取所有提交供IMS組織發佈的目的地清單 `/authoring/destinations/publish` 端點。

**API格式**

使用下列API格式來擷取您的帳戶的所有發佈請求。

```http
GET /authoring/destinations/publish
```

使用下列API格式來擷取由 `{DESTINATION_ID}` 參數。

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**要求**

以下兩個請求會根據您是否傳遞 `DESTINATION_ID` 參數。

選取下方的每個標籤，以檢視對應的裝載。

>[!BEGINTABS]

>[!TAB 擷取所有發佈請求]

+++請求

下列請求會根據 [!DNL IMS Org ID] 和沙箱設定。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++回應

下列回應會根據您使用的IMS組織ID和沙箱名稱，傳回HTTP狀態200，並列出您有權存取的所有已提交以供發佈的目的地。 一 `configId` 對應至一個目的地的發佈請求。

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
| `destinationId` | 字串 | 您提交以供發佈的目標配置的目標ID。 |
| `publishDetailsList.configId` | 字串 | 已提交目的地的目的地發佈請求的唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字串 | 傳回目標可用的Experience Platform組織。 <br> <ul><li> 針對 `"destinationType": "PUBLIC"`，此參數會傳回 `"*"`，這表示目的地可供所有Experience Platform組織使用。</li><li> 針對 `"destinationType": "DEV"`，此參數會傳回您用來製作和測試目的地之組織的組織ID。</li></ul> |
| `publishDetailsList.status` | 字串 | 目的地發佈請求的狀態。 可能的值包括 `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. 具有值的目的地 `PUBLISHED` 即時，可供Experience Platform客戶使用。 |
| `publishDetailsList.destinationType` | 字串 | 目的地的類型。 值可以是 `DEV` 和 `PUBLIC`. `DEV` 對應至Experience Platform組織中的目的地。 `PUBLIC` 對應至您提交以供發佈的目的地。 以Git術語來思考這兩個選項， `DEV` 版本代表您的本機製作分支和 `PUBLIC` 版本代表遠端主分支。 |
| `publishDetailsList.publishedDate` | 字串 | 目的地提交以進行發佈的日期（以紀元時間為單位）。 |

{style="table-layout:auto"}

+++

>[!TAB 擷取特定發佈請求]

+++請求

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/{DESTINATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 您要擷取發佈狀態的目的地ID。 |

+++

+++回應

若您傳入 `DESTINATION_ID` 在API呼叫中，回應會傳回HTTP狀態200，並包含指定目的地發佈請求的詳細資訊。

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

+++

>[!ENDTABS]

## API錯誤處理

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。