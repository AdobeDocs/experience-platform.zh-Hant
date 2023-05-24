---
description: 本頁說明了用於通過Adobe Experience Platform Destination SDK檢索有關目標發佈請求的詳細資訊的API調用。
title: 檢索目標發佈請求
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 2%

---


# 檢索目標發佈請求

>[!IMPORTANT]
>
>只有在提交要供其他Experience Platform客戶使用的產品化（公共）目標時，才需要使用此API終結點。 如果您正在建立專用目標供自己使用，則無需使用發佈API正式提交目標。

>[!IMPORTANT]
>
>**API終結點**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

配置和測試目標後，您可以將其提交給Adobe以進行審閱和發佈。 閱讀 [提交以審閱在Destination SDK中創作的目標](../guides/submit-destination.md) 對於作為目標提交流程的一部分必須執行的所有其他步驟。

在以下情況下，使用發佈目標API終結點提交發佈請求：

* 作為Destination SDK合作夥伴，您希望使所有Experience Platform組織中的產品化目標都可用於所有Experience Platform客戶；
* 你 *任何更新* 配置。 配置更新僅在您提交新發佈請求後才反映在目標中，新發佈請求已獲得Experience Platform團隊的批准。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 目標發佈API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 列出目標發佈請求 {#retrieve-list}

通過向IMS組織發出GET請求，您可以檢索為發佈而提交的所有目標的清單 `/authoring/destinations/publish` 端點。

**API格式**

使用以下API格式檢索帳戶的所有發佈請求。

```http
GET /authoring/destinations/publish
```

使用以下API格式檢索由 `{DESTINATION_ID}` 的下界。

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**要求**

以下兩個請求將檢索IMS組織的所有發佈請求或特定的發佈請求，具體取決於您是否通過 `DESTINATION_ID` 中的設定。

選擇下面的每個頁籤以查看相應的負載。

>[!BEGINTABS]

>[!TAB 檢索所有發佈請求]

+++請求

以下請求將根據 [!DNL IMS Org ID] 和沙盒配置。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++回應

以下響應將返回HTTP狀態200，其中列出了您有權訪問的所有要發佈的目標，這些目標基於您使用的IMS組織ID和沙盒名稱。 一 `configId` 對應於一個目標的發佈請求。

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
| `destinationId` | 字串 | 已提交用於發佈的目標配置的目標ID。 |
| `publishDetailsList.configId` | 字串 | 已提交目標的目標發佈請求的唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字串 | 返回目標可用的Experience Platform組織。 <br> <ul><li> 對於 `"destinationType": "PUBLIC"`，此參數將返回 `"*"`，這意味著目標可用於所有Experience Platform組織。</li><li> 對於 `"destinationType": "DEV"`，此參數返回您用於建立和test目標的組織的組織ID。</li></ul> |
| `publishDetailsList.status` | 字串 | 目標發佈請求的狀態。 可能的值為 `TEST`。 `REVIEW`。 `APPROVED`。 `PUBLISHED`。 `DENIED`。 `REVOKED`。 `DEPRECATED`。 具有值的目標 `PUBLISHED` 可供Experience Platform客戶使用。 |
| `publishDetailsList.destinationType` | 字串 | 目標類型。 值可以是 `DEV` 和 `PUBLIC`。 `DEV` 對應於您的Experience Platform組織中的目標。 `PUBLIC` 與您已提交用於發佈的目標相對應。 用Git的話來想這兩個選擇 `DEV` 版本表示本地創作分支和 `PUBLIC` 版本表示遠程主分支。 |
| `publishDetailsList.publishedDate` | 字串 | 提交目標以進行發佈的日期（以大紀元為單位）。 |

{style="table-layout:auto"}

+++

>[!TAB 檢索特定發佈請求]

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
| `{DESTINATION_ID}` | 要檢索其發佈狀態的目標的ID。 |

+++

+++回應

如果你通過 `DESTINATION_ID` 在API調用中，響應返回HTTP狀態200，其中包含有關指定目標發佈請求的詳細資訊。

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

{style="table-layout:auto"}

+++

>[!ENDTABS]

## API錯誤處理

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors) 中。