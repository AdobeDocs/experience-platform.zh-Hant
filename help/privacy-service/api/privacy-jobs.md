---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 隱私權工作API端點
description: 了解如何使用Experience CloudAPI管理Privacy Service應用程式的隱私權工作。
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 3%

---

# 隱私權作業端點

本檔案說明如何使用API呼叫處理隱私權工作。 具體來說，涵蓋 `/job` 端點 [!DNL Privacy Service] API。 閱讀本指南之前，請參閱 [快速入門手冊](./getting-started.md) 若要成功對API進行呼叫，您必須知道的重要資訊，包括必要的標題以及如何讀取範例API呼叫。

>[!NOTE]
>
>如果您嘗試管理客戶的同意或選擇退出請求，請參閱 [同意端點指南](./consent.md).

## 列出所有作業 {#list}

您可以向 `/jobs` 端點。

**API格式**

此請求格式使用 `regulation` 查詢參數 `/jobs` 端點，因此會以問號(`?`)，如下所示。 回應會以編頁方式呈現，可讓您使用其他查詢參數(`page` 和 `size`)來篩選回應。 您可以使用&amp;符號分隔多個參數(`&`)。

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| 參數 | 說明 |
| --- | --- |
| `{REGULATION}` | 要查詢的規則類型。 接受的值包括： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>請參閱 [支援的法規](../regulations/overview.md) 如需上述值代表之隱私權法規的詳細資訊。 |
| `{PAGE}` | 要顯示的資料頁，使用基於0的編號。 預設值為 `0`。 |
| `{SIZE}` | 每個頁面上要顯示的結果數。 預設為 `1` 而最大值是 `100`. 超過上限會導致API傳回400程式碼錯誤。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會從頁面大小為50的第三個頁面開始，擷取IMS組織內所有工作的編頁清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的回應會傳回作業清單，每個作業都包含其等詳細資訊 `jobId`. 在此範例中，回應會包含50個工作的清單，從結果的第三個頁面開始。

### 存取後續頁面

若要在編頁回應中擷取下一組結果，您必須對相同端點進行另一個API呼叫，同時增加 `page` 查詢參數（按1）。

## 建立隱私權工作 {#create-job}

建立新工作請求之前，您必須先收集有關資料主體的識別資訊，這些資料主體的資料要存取、刪除或選擇退出銷售。 取得所需資料後，必須在POST要求的裝載中提供給 `/jobs` 端點。

>[!NOTE]
>
>相容的Adobe Experience Cloud應用程式會使用不同的值來識別資料主體。 請參閱 [Privacy Service和Experience Cloud應用程式](../experience-cloud-apps.md) 以取得應用程式所需識別碼的詳細資訊。 如需決定要傳送給哪些ID的更一般指引 [!DNL Privacy Service]，請參閱 [隱私權要求中的身分資料](../identity-data.md).

此 [!DNL Privacy Service] API支援兩種個人資料的工作請求：

* [存取和/或刪除](#access-delete):存取（讀取）或刪除個人資料。
* [選擇退出銷售](#opt-out):將個人資料標示為不要出售。

>[!IMPORTANT]
>
>雖然存取和刪除請求可合併為單一API呼叫，但您必須個別提出選擇退出請求。

### 建立存取/刪除作業 {#access-delete}

本節示範如何使用API提出存取/刪除工作請求。

**API格式**

```http
POST /jobs
```

**要求**

下列請求會建立新的作業請求，由裝載中提供的屬性進行設定，如下所述。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager","profileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| 屬性 | 說明 |
| --- | --- |
| `companyContexts` **(必填)** | 包含貴組織驗證資訊的陣列。 所列的每個識別碼都包含下列屬性： <ul><li>`namespace`:識別碼的命名空間。</li><li>`value`:識別碼的值。</li></ul>是 **必填** 其中一個識別碼使用 `imsOrgId` as `namespace`，連同其 `value` 包含您IMS組織的唯一ID。 <br/><br/>其他識別碼可以是產品專屬的公司限定碼(例如 `Campaign`)，可識別與貴組織所屬Adobe應用程式的整合。 潛在值包括帳戶名稱、用戶端代碼、租用戶ID或其他應用程式識別碼。 |
| `users` **(必填)** | 一個陣列，其中包含至少一個用戶的集合，您要訪問或刪除其資訊。 單一請求最多可提供1000個使用者ID。 每個使用者物件包含下列資訊： <ul><li>`key`:用來限定回應資料中個別作業ID的使用者識別碼。 最佳實務是為此值選擇可輕鬆識別的唯一字串，以便日後輕鬆參考或查詢。</li><li>`action`:列出對使用者資料採取之所需動作的陣列。 根據您要執行的動作，此陣列必須包含 `access`, `delete`，或兩者皆有。</li><li>`userIDs`:使用者的身分集合。 單一使用者可擁有的身分數目上限為九。 每個身分都包含 `namespace`, `value`，以及命名空間限定符(`type`)。 請參閱 [附錄](appendix.md) 以取得這些必要屬性的詳細資訊。</li></ul> 有關 `users` 和 `userIDs`，請參閱 [疑難排解指南](../troubleshooting-guide.md#user-ids). |
| `include` **(必填)** | 要包含在處理中的Adobe產品陣列。 如果此值遺失或空白，則會拒絕要求。 僅包含貴組織已與整合的產品。 請參閱 [接受的產品值](appendix.md) ，以了解詳細資訊。 |
| `expandIDs` | 選用屬性，若設為 `true`，代表處理應用程式中ID的最佳化(目前僅支援 [!DNL Analytics])。 若省略，此值會預設為 `false`. |
| `priority` | Adobe Analytics使用的選用屬性，可設定處理要求的優先順序。 接受的值為 `normal` 和 `low`. 若 `priority` 則預設行為為 `normal`. |
| `analyticsDeleteMethod` | 選用屬性，指定Adobe Analytics如何處理個人資料。 此屬性接受兩個可能的值： <ul><li>`anonymize`:指定的使用者ID集合所參考的所有資料都會設為匿名。 若 `analyticsDeleteMethod` 則此為預設行為。</li><li>`purge`:所有資料都會完全移除。</li></ul> |
| `mergePolicyId` | 向即時客戶設定檔提出隱私權要求時(`profileService`)，您可以選擇提供特定 [合併策略](../../profile/merge-policies/overview.md) 供ID匯整使用。 透過指定合併原則，隱私權要求可在傳回客戶資料時包含區段資訊。 每個請求只能指定一個合併策略。 如果未提供合併原則，回應中就不會包含分段資訊。 |
| `regulation` **(必填)** | 隱私權工作的規範。 接受下列值： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>請參閱 [支援的法規](../regulations/overview.md) 如需上述值代表之隱私權法規的詳細資訊。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回新建立之作業的詳細資訊。

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076be029f3",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd023j1",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "delete"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 3
}
```

| 屬性 | 說明 |
| --- | --- |
| `jobId` | 作業的唯讀、唯一系統產生的ID。 此值將用於查找特定作業的下一步。 |

{style=&quot;table-layout:auto&quot;}

成功提交作業請求後，您可以繼續執行 [檢查作業狀態](#check-status).

## 檢查作業的狀態 {#check-status}

您可以包含特定作業的，以擷取該作業的相關資訊，例如其目前處理狀態 `jobId` 在GET請求的路徑中 `/jobs` 端點。

>[!IMPORTANT]
>
>先前建立的作業的資料僅可在作業完成日期後30天內檢索。

**API格式**

```http
GET /jobs/{JOB_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{JOB_ID}` | 要查找的作業的ID。 此ID會在 `jobId` 的成功API回應中 [建立工作](#create-job) 和 [列出所有作業](#list). |

{style=&quot;table-layout:auto&quot;}

**要求**

以下請求將檢索其 `jobId` 是在要求路徑中提供。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的回應會傳回指定作業的詳細資訊。

```json
{
    "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "complete",
    "submittedBy": "{ACCOUNT_ID}",
    "createdDate": "10/02/2019 08:25 PM GMT",
    "lastModifiedDate": "10/02/2019 08:25 PM GMT",
    "userIds": [
        {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard",
            "namespaceId": 6,
            "isDeletedClientSide": false
        },
        {
            "namespace": "ECID",
            "value": "1123A4D5690B32A",
            "type": "standard",
            "namespaceId": 4,
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Analytics",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Finished successfully."
            }
        },
        {
            "product": "Profile",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Success dataSetIds = [5dbb87aad37beb18a96feb61], Failed dataSetIds = []"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6054-200",
                "responseMsgDetail": "PARTIALLY COMPLETED- Data not found for some requests, check results for more info.",
                "results": {
                  "processed": ["1123A4D5690B32A"],
                  "ignored": ["dsmith@acme.com"]
                }
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| 屬性 | 說明 |
| --- | --- |
| `productStatusResponse` | 中的每個物件 `productResponses` 陣列包含有關特定作業當前狀態的資訊 [!DNL Experience Cloud] 應用程式。 |
| `productStatusResponse.status` | 作業的當前狀態類別。 請參閱下表以取得 [可用狀態類別](#status-categories) 以及它們的對應意義。 |
| `productStatusResponse.message` | 工作的特定狀態，與狀態類別相對應。 |
| `productStatusResponse.responseMsgCode` | 接收的產品回應訊息的標準代碼 [!DNL Privacy Service]. 此訊息的詳細資訊提供於 `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | 更詳細的工作狀態說明。 類似狀態的訊息可能因產品而異。 |
| `productStatusResponse.results` | 對於某些狀態，某些產品可能會傳回 `results` 提供未涵蓋的其他資訊的對象 `responseMsgDetail`. |
| `downloadURL` | 如果作業的狀態為 `complete`，此屬性會提供URL，以ZIP檔案形式下載工作結果。 作業完成後60天內可下載此檔案。 |

{style=&quot;table-layout:auto&quot;}

### 作業狀態類別 {#status-categories}

下表列出了不同的可能作業狀態類別及其相應含義：

| 狀態類別 | 含義 |
| -------------- | -------- |
| `complete` | 工作已完成，且（如果需要）檔案會從每個應用程式上傳。 |
| `processing` | 應用程式已確認該作業，且當前正在處理。 |
| `submitted` | 工作將提交至每個適用的應用程式。 |
| `error` | 處理作業時失敗 — 通過檢索單個作業詳細資訊，可獲得更具體的資訊。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>提交的工作可能會保留在 `processing` 狀態（如果其具有仍在處理的相依子作業）。

## 後續步驟

您現在知道如何使用 [!DNL Privacy Service] API。 有關如何使用用戶介面執行相同任務的資訊，請參閱 [Privacy ServiceUI概述](../ui/overview.md).
