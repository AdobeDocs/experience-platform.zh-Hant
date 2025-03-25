---
title: 套用存取標籤以管理使用API之來源資料流程的使用者存取權
description: 瞭解如何使用流量服務API來套用存取權標籤，並管理使用者對您的來源資料流的存取權。
hide: true
hidefromtoc: true
source-git-commit: 80fb60abdf33eb2a7ca691a9a48a811c632b34fc
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 3%

---

# 套用存取標籤以管理使用API之來源資料流程的使用者存取權

您可以使用Real-Time CDP中[以屬性為基礎的存取控制](../../../access-control/abac/overview.md)所提供的功能，將標籤套用至您的來源資料流。 透過此功能，您可以確保組織中只有一部分使用者有權存取特定來源資料流。

將存取標籤新增至特定資料流時，只有具備該標籤指派之角色存取權的使用者才能檢視及編輯該資料流。 如果來源資料流未標籤任何標籤，則屬於您組織的所有使用者皆可看到該資料流。 例如，如果您將C12標籤套用至資料流，則指派給沒有C12標籤之角色的使用者，將無法檢視和編輯具有C12標籤的資料流。

閱讀本指南，瞭解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)將存取標籤套用至您的來源資料流。

## 快速入門

在使用存取控制標籤之前，請務必先熟悉屬性型存取控制的功能。 如需詳細資訊，請參閱下列檔案：

* [屬性式存取控制概觀](../../../access-control/abac/overview.md)
* [以屬性為基礎的存取控制端對端指南](../../../access-control/abac/end-to-end-guide.md)
* [屬性型存取控制API指南](../../../access-control/abac/api/overview.md)
* [資料使用標籤字彙表](../../../data-governance/labels/reference.md)

## 將存取權標籤套用至來源資料流

>[!NOTE]
>
>* 您不能將標籤套用到資料流執行。 不過，資料流執行會繼承您套用至父資料流的任何標籤。
>
>* 如果您沒有資料流的檢視存取權，那麼您將無法檢視其對應的資料流執行。

若要新增標籤至資料流，請對`/flows`端點發出PATCH請求，並提供您要更新的資料流識別碼。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{FLOW_ID}` | 您要更新的資料流的ID。 |

**要求**

>[!TIP]
>
>若要提出PATCH請求，請提供您要更新的資料流版本/etag做為`if-match`標頭引數。

下列要求將C12標籤新增至識別碼為`84224def-1e2a-4d95-9ea2-132d697ed2aa`的資料流。

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/84224def-1e2a-4d95-9ea2-132d697ed2aa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'if-match: "c5002e0e-0000-0200-0000-67a3c3b70000"'
  -d '[
    {
        "op": "add",
        "path": "/labels",
        "value": ["core/C12"]
    }
]'
```

| 屬性 | 說明 |
| --- | --- |
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`、`replace`和`remove`。 |
| `path` | 要更新的資料流部分。 |
| `value` | 您想要用來更新屬性的新值。 |



**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以透過向[!DNL Flow Service] API發出GET請求來驗證更新，同時提供您的流量ID。

```json
{
    "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

當您成功設定資料流的存取標籤後，任何無法存取該標籤的使用者將無法再擷取資料流。 例如，如果未布建C12標籤的使用者發出GET要求，以擷取具有ID `84224def-1e2a-4d95-9ea2-132d697ed2aa`的資料流，他們會收到下列回應：

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-1439-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "detailed-message": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
        "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
        "request-id": "{REQUEST_ID}",
        "type": "flows"
    },
    "errorMessage": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
    "errorDetails": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again."
}
```

同樣地，無法存取C12標籤的使用者將無法針對更新的資料流提出任何PATCH或DELETE請求，並將收到以下回應：

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-2120-403",
    "title": "Forbidden",
    "status": 403,
    "report": {
        "detailed-message": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
        "request-id": "{REQUEST_ID}"
    },
    "errorMessage": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
    "errorDetails": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again."
}
```

## 後續步驟

您現在知道如何將存取權標籤套用至來源資料流。 您現在可以確保組織內只有特定群組使用者可以存取特定來源資料流。 如需詳細資訊，請參閱下列檔案：

* [在UI中套用存取標籤至來源資料流](../ui/labels.md)
* [存取控制概覽](../../../access-control/home.md)