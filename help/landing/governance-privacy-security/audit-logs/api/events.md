---
title: 稽核事件API端點
description: 瞭解如何使用稽核查詢API在Experience Platform中擷取稽核事件。
role: Developer
feature: Audits, API
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# 稽核事件端點

稽核記錄用於提供各種服務和功能的使用者活動細節。 記錄中記錄的每個動作都包含中繼資料，其指出動作型別、日期和時間、執行動作之使用者的電子郵件ID，以及與動作型別相關的其他屬性。 [!DNL Audit Query] API中的`/audit/events`端點可讓您以程式設計方式擷取貴組織在[!DNL Experience Platform]中的活動事件資料。

## 快速入門

本指南中使用的API端點是[[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/)的一部分。 繼續之前，請先檢閱[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何[!DNL Experience Platform] API所需必要標題的重要資訊。

## 列出稽核事件

您可以對`/audit/events`端點發出GET要求，指定您要在裝載中擷取的事件，以擷取事件資料。

**API格式**

```http
GET /audit/events
```

[!DNL Audit Query] API支援在列出事件時使用查詢引數來頁面和篩選結果。

| 參數 | 說明 |
| --- | --- |
| `limit` | 回應中可傳回的最大記錄數。 預設`limit`為50。 |
| `start` | 針對傳回的搜尋結果，指向第一個專案的指標。 若要存取結果的下一頁，此引數應該以限制所指示的相同量增加。 範例：若要存取limit=50之要求的下一頁結果，請使用引數start=50，然後對其後的頁面使用start=100，以此類推。 |
| `queryId` | 向/audit/events端點提出查詢時，回應會包含queryId字串屬性。 若要在個別呼叫中進行相同的查詢，您可以將ID值納入為單一查詢引數，而非再次手動設定搜尋引數。 |

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events?limit=10
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**回應**

成功的回應會傳回要求中所指定量度和篩選器的結果資料點。

```json
{
   "_embedded": {
     "customerAuditLogList": [
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "32b72208-3035-4bc6-b434-39e34401a864",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "5NphpgUQdQnjTWOcS9DSMs2wD1EUMlYG",
         "authId": "96715f98-d100-4575-8491-ebbcea654eb9",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:58:09.745+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "a178736a-8fa1-47da-bac5-b0d9e741e414",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "7AlGIAhWvaEzYWHLzvuf26AAFAkqSyKg",
         "authId": "60fc1077-4aef-4e1f-a5ff-f64183e060f4",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:28:00.301+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "ccfe8c77-9b93-481d-a561-0b2edf3b77dc",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "hArqS4CAa8wfRPnKuxV4yaA82atxwzYu",
         "authId": "80b7d887-9338-4cd5-9d79-2483b03f0160",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T20:58:07.750+0000"
       }
     ]    
   },
   "_links": {
     "self": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?limit=10&start=0&property=type%253D%253Dcore"
     },
     "next": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&start=10&limit=10"
     },
     "page": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&limit=10{&start}",
       "templated": true
     }
  },
  "page": {
    "size": 10,
    "totalElements": 3,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2"
}
```

| 屬性 | 說明 |
| --- | --- |
| `customerAuditLogList` | 陣列，其物件代表要求中指定的每個事件。 每個物件都包含有關篩選器設定和傳回事件資料的資訊。 |
| `userEmail` | 執行事件之使用者的電子郵件。 |
| `eventType` | 事件型別。 事件型別包括`Core`和`Enhanced`。 |
| `imsOrgId` | 發生事件之組織的ID。 |
| `permissionResource` | 提供許可權的產品或功能會執行此動作。 資源可以是下列任一專案： <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | 動作涉及的許可權型別。 |
| `assetType` | 執行動作的Experience Platform資源型別。 |
| `assetId` | 執行動作之Experience Platform資源的唯一識別碼。 |
| `assetName` | 執行動作的Experience Platform資源名稱。 |
| `action` | 為事件記錄的動作型別。 動作可以是下列任一專案： <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | 動作的狀態。 狀態可以是下列任一專案： </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style="table-layout:auto"}
