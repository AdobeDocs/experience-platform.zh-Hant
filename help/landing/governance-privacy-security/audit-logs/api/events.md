---
title: 稽核事件API端點
description: 瞭解如何使用稽核查詢API在Experience Platform中擷取稽核事件。
role: Developer
feature: Audits, API
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: dec895e3ea625fb86d1891bad713185d39c47c81
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# 稽核事件端點

稽核記錄用於提供各種服務和功能的使用者活動細節。 記錄中記錄的每個動作都包含中繼資料，其指出動作型別、日期和時間、執行動作之使用者的電子郵件ID，以及與動作型別相關的其他屬性。 `/audit/events` API中的[!DNL Audit Query]端點可讓您以程式設計方式擷取貴組織在[!DNL Experience Platform]中的活動事件資料。

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
    "events": [
      {
        "id": "6ecc125d-da03-4882-a944-88c707ddc3f7",
        "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
        "permissionResource": "Dataset",
        "permissionType": "WRITE",
        "assetType": "Dataset",
        "action": "Create",
        "status": "Allow",
        "failureCode": "",
        "timestamp": "2025-06-24T16:50:28.318+0000",
        "version": "1.0",
        "imsOrgId": "{ORGANIZATION_ID}",
        "region": "VA7",
        "authId": "e6b46821-e2b4-4729-952f-2e4afd713b31",
        "assetId": "685ad754fb1abe2b263df4b3",
        "assetName": "my-dataset",
        "sandboxName": "prod",
        "sandboxId": "{SANDBOX_ID}",
        "userEmail": "{USER_EMAIL}",
        "userIpAddresses": [
          "130.*.*.*",
          "10.*.*.*"
        ],
        "enhancedEvents": [
          {
            "id": "0ee91e42-ac46-4f35-a01a-f74a1569c404",
            "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
            "permissionResource": "Dataset",
            "permissionType": "Write",
            "assetType": "Dataset",
            "action": "Create",
            "status": "Success",
            "failureCode": "",
            "timestamp": "2025-06-24T16:50:28.883+0000",
            "assetId": "685ad754fb1abe2b263df4b3",
            "assetName": "my-dataset"
          }
        ]
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?property=user%253D%253Ddraghici%2540adobe.com"
    },
    "page": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3&limit=50{&start}",
      "templated": true
    }
  },
  "page": {
    "size": 1,
    "totalElements": 1,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3"
}
```

| 屬性 | 說明 |
| --- | --- |
| `events` | 陣列，其物件代表要求中指定的每個事件。 每個物件都包含有關篩選器設定和傳回事件資料的資訊。 |
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
