---
title: 內容API端點
description: 瞭解如何使用Privacy Service API擷取您的存取資料。
role: Developer
badgePrivateBeta: label="私人測試版" type="Informative"
exl-id: b3b7ea0f-957d-4e51-bf92-121e9ae795f5
source-git-commit: e3a453ad166fe244b82bd1f90e669579fcf09d17
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# 內容端點

>[!IMPORTANT]
>
>此 `/content` 端點目前為測試版，您的組織可能尚未擁有存取權。 功能和檔案可能會有所變更。

使用 `/content` 要安全擷取的端點 *存取資訊* （隱私權主體有權要求存取的資訊）提供給您的客戶。 回應中提供的下載URL `/jobs/{JOB_ID}` GET要求指向Adobe服務端點。 然後，您可以發出GET請求給 `/jobs/:JOB_ID/content` 以傳回JSON格式的客戶資料。 此存取方法實作多層驗證和存取控制以增強安全性。

在使用本指南之前，請參閱 [快速入門手冊](./getting-started.md) 以取得有關以下範例API呼叫中呈現的必要驗證標題的資訊。

>[!TIP]
>
>如果您目前不知道所需存取資訊的工作ID，請呼叫 `/jobs` 端點並使用其他查詢引數來篩選結果。 完整的可用查詢引數清單可在 [隱私權工作端點指南](./privacy-jobs.md).

## 擷取隱私工作資訊

若要擷取特定工作的相關資訊（例如其目前的處理狀態），請包含該工作的 `jobId` 在GET請求的路徑中 `/jobs` 端點。

**API格式**

```http
GET /jobs/{JOB_ID}
```

**要求**

以下請求會擷取下列工作之詳細資訊： `jobId` 請求路徑中會提供。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的回應會傳回指定工作的詳細資訊。

>[!NOTE]
>
>隱私權工作必須具備 `complete` 狀態以包含 `downloadUrl`.

```json
{
    "jobId":"dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5",
    "requestId":"17129380910360540RX-753",
    "userKey":"1234",
    "action":"access",
    "status":"complete",
    "submittedBy":"jsnow@adobe.com",
    "createdDate":"04/12/2024 04:08 PM GMT",
    "lastModifiedDate":"04/12/2024 04:08 PM GMT",
    "userIds":[{
        "namespace":"ECID",
        "value":"1234",
        "type":"standard",
        "namespaceId":4,
        "isDeletedClientSide":false
        }],
    "productResponses":[{
        "product":"Identity",
        "retryCount":0,
        "processedDate":"04/12/2024 04:08 PM GMT",
        "productStatusResponse":{"status":"submitted"
        }}],
    "downloadUrl":"https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5/content",
    "regulation":"gdpr"
}
```

| 屬性 | 說明 |
|----------------------|---------------------------------------------------------------------------------------------------------------|
| `jobId` | 隱私權工作的唯一識別碼。 |
| `requestId` | 向Privacy Service提出之特定要求的唯一識別碼。 |
| `userKey` | `userKey` 是 `key` 您在提交隱私權請求時提供的值。 此 `key` 值是您為有意義之資料主體提供識別碼的機會。 這通常是您的系統為追蹤該資料主體而建立的唯一識別碼。 提示：您可以列出所有作用中的隱私權工作，並比較您的 `key` 至每個工作。 |
| `action` | 要求的動作型別。 接受的值為 `access` 和 `delete`. |
| `status` | 隱私權工作的目前狀態。 |
| `submittedBy` | 提交隱私權工作之人員的電子郵件地址。 |
| `createdDate` | 隱私權工作的建立日期和時間。 |
| `lastModifiedDate` | 上次修改隱私權工作的日期與時間。 |
| `userIds` | 包含使用者識別碼和相關資訊的陣列。 |
| `userIds.namespace` | 用於使用者識別碼的名稱空間。 |
| `userIds.value` | 使用者識別碼的實際值。 |
| `userIds.type` | 識別碼的型別(例如 `standard` 或 `custom`)。 |
| `userIds.namespaceId` | 用來分類和管理使用者身分的名稱空間識別碼。 |
| `userIds.isDeletedClientSide` | 表示識別碼在使用者端是否已刪除的布林值。 |
| `productResponses` | 一個陣列，包含與隱私權工作相關的不同產品或服務的回應。 |
| `productResponses.product` | 用來取得資料主體資訊的產品或服務名稱。 |
| `productResponses.retryCount` | 重試請求的次數。 |
| `productResponses.processedDate` | 處理產品回應的日期和時間。 |
| `productResponses.productStatusResponse` | 包含產品回應狀態的物件。 |
| `productResponses.productStatusResponse.status` | 產品回應的狀態。 |
| `downloadURL` | 此屬性會提供端點，可在工作完成後的60天內呼叫。 工作的狀態必須為 `complete` 和 `action` 必須是 `access`. 否則，此欄位不存在。 |
| `regulation` | 處理隱私權請求的法規架構，例如 `gdpr`， `ccpa`， `lgpd_bra`， `pdpa_tha`、等等。 |

{style="table-layout:auto"}

## 擷取客戶存取資訊 {#retrieve-access-data}

GET若要取得回應資料主體查詢而產生的「存取資訊」，請對 `/jobs/{JOB_ID}/content` 端點。 回應為zip檔案(*.zip)，其中包含資料夾，每個產品都有子資料夾，其中包含資料主體的資料。

>[!TIP]
>
>您需要特定工作ID才能提出此請求。 GET如果您需要擷取特定作業ID，請先向 `/jobs` 端點並使用其他查詢引數來篩選結果。 包含允許查詢引數的詳細資訊可在以下網址找到： [隱私權工作端點指南](./privacy-jobs.md).

**API格式**

```http
GET /jobs/{JOB_ID}/content
```

**要求**

以下請求會針對請求中提供的作業ID傳回「存取資訊」。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/32d429b1-f7f4-11ee-a365-574bcf5a525d/content \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'Accept: application/json`
```

**回應**

回應為zip檔案(*.zip)。 雖然無法保證此資訊，但通常會以JSON格式傳回。 擷取的資料可以任何格式傳回。

