---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 隱私權工作API端點
topic-legacy: developer guide
description: 瞭解如何使用Experience CloudAPI管理Privacy Service應用程式的隱私權工作。
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
translation-type: tm+mt
source-git-commit: e226990fc84926587308077b32b128bfe334e812
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 隱私權工作端點

本檔案涵蓋如何使用API呼叫的隱私權工作。 具體來說，它涵蓋[!DNL Privacy Service] API中`/job`端點的使用。 在閱讀本指南之前，請參閱[快速入門章節](./getting-started.md#getting-started)，以取得成功呼叫API所需的重要資訊，包括必要的標題和如何讀取範例API呼叫。

>[!NOTE]
>
>如果您嘗試管理客戶的同意或選擇退出請求，請參閱[同意端點指南](./consent.md)。

## 列出所有作業{#list}

您可以向`/jobs`端點提出GET請求，以檢視組織內所有可用隱私權工作的清單。

**API格式**

此請求格式在`/jobs`端點上使用`regulation`查詢參數，因此它以問號(`?`)開頭，如下所示。 回應會編頁，讓您使用其他查詢參數（`page`和`size`）來篩選回應。 您可以使用&amp;符號(`&`)來分隔多個參數。

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| 參數 | 說明 |
| --- | --- |
| `{REGULATION}` | 要查詢的規則類型。 接受的值包括： <ul><li>`gdpr` （歐盟）</li><li>`ccpa` （加州）</li><li>`lgpd_bra` (巴西)</li><li>`nzpa_nzl` (紐西蘭)</li><li>`pdpa_tha` (泰國)</li></ul> |
| `{PAGE}` | 要顯示的資料頁，使用基於0的編號。 預設值為 `0`。 |
| `{SIZE}` | 每個頁面上要顯示的結果數。 預設值為`1` ，最大值為`100`。 超過最大值會導致API傳回400碼錯誤。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會從頁面大小為50的第三頁開始，擷取IMS組織內所有工作的編頁清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**回應**

成功的響應返回作業清單，每個作業都包含詳細資訊，如`jobId`。 在此範例中，回應將包含50個工作的清單，從結果的第三頁開始。

### 存取後續頁面

若要在編頁回應中擷取下一組結果，您必須對相同端點進行另一個API呼叫，同時將`page`查詢參數增加1。

## 建立隱私權工作{#create-job}

在建立新工作請求之前，您必須先收集您要存取、刪除或選擇退出銷售之資料主體的相關識別資訊。 在您取得所需資料後，必須在`/jobs`端點之POST要求的裝載中提供該資料。

>[!NOTE]
>
>相容的Adobe Experience Cloud應用程式使用不同的值來識別資料主體。 有關應用程式所需標識符的詳細資訊，請參閱[Privacy Service和Experience Cloud應用程式](../experience-cloud-apps.md)上的指南。 如需決定要傳送至[!DNL Privacy Service]的ID的更一般指引，請參閱隱私權要求中關於[身分資料的檔案](../identity-data.md)。

[!DNL Privacy Service] API支援兩種個人資料的工作要求：

* [存取和／或刪除](#access-delete):存取（讀取）或刪除個人資料。
* [選擇退出銷售](#opt-out):將個人資料標示為不銷售。

>[!IMPORTANT]
>
>雖然存取和刪除請求可合併為單一API呼叫，但必須個別提出退出請求。

### 建立訪問／刪除作業{#access-delete}

本節說明如何使用API進行存取／刪除工作請求。

**API格式**

```http
POST /jobs
```

**要求**

下列請求會建立新的工作請求，由裝載中提供的屬性設定，如下所述。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
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
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| 屬性 | 說明 |
| --- | --- |
| `companyContexts` **(必填)** | 包含貴組織驗證資訊的陣列。 每個列出的識別碼都包含下列屬性： <ul><li>`namespace`:識別碼的名稱空間。</li><li>`value`:識別碼的值。</li></ul>其中一個識別碼使用`imsOrgId`作為`namespace`，其`value`包含IMS組織的唯一ID，這是&#x200B;**required**。 <br/><br/>其他識別碼可以是特定於產品的公司限定詞(例如 `Campaign`)，用於標識與屬於您組織的Adobe應用程式的整合。潛在值包括帳戶名稱、用戶端代碼、租用戶ID或其他應用程式識別碼。 |
| `users` **(必填)** | 包含至少一個用戶集合的陣列，您希望訪問或刪除其資訊。 在單一請求中最多可提供1000個使用者ID。 每個用戶對象都包含以下資訊： <ul><li>`key`:用於用戶的標識符，用於限定響應資料中的單獨作業ID。為此值選擇唯一、可輕鬆識別的字串是最佳實務，以便日後輕鬆參考或查閱。</li><li>`action`:列出對用戶資料採取所需操作的陣列。根據您要執行的操作，此陣列必須包括`access`、`delete`或兩者。</li><li>`userIDs`:使用者身分的集合。單一使用者可擁有的身分數目限制為9。 每個身分都由`namespace`、`value`和命名空間限定詞(`type`)組成。 如需這些必要屬性的詳細資訊，請參閱[附錄](appendix.md)。</li></ul> 如需`users`和`userIDs`的詳細說明，請參閱[疑難排解指南](../troubleshooting-guide.md#user-ids)。 |
| `include` **(必填)** | 要包含在您處理中的一系列Adobe產品。 如果此值遺失或空白，則會拒絕請求。 僅包含貴組織已整合的產品。 如需詳細資訊，請參閱附錄中[接受的產品值](appendix.md)一節。 |
| `expandIDs` | 當設為`true`時，此選用屬性代表處理應用程式中ID的最佳化（目前僅[!DNL Analytics]支援）。 若省略，此值預設為`false`。 |
| `priority` | Adobe Analytics使用的可選屬性，可設定處理請求的優先順序。 接受的值為`normal`和`low`。 如果省略`priority`，則預設行為為`normal`。 |
| `analyticsDeleteMethod` | 可選屬性，指定Adobe Analytics如何處理個人資料。 此屬性接受兩個可能的值： <ul><li>`anonymize`:指定使用者ID集合所參考的所有資料都會設為匿名。如果省略`analyticsDeleteMethod`，則此為預設行為。</li><li>`purge`:所有資料都會完全移除。</li></ul> |
| `regulation` **(必填)** | 隱私權工作的法規。 接受下列值： <ul><li>`gdpr` （歐盟）</li><li>`ccpa` （加州）</li><li>`lgpd_bra` (巴西)</li><li>`nzpa_nzl` (紐西蘭)</li><li>`pdpa_tha` (泰國)</li></ul> |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回新建立之工作的詳細資料。

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
| `jobId` | 作業的唯讀唯一系統產生的ID。 此值用於查找特定作業的下一步。 |

{style=&quot;table-layout:auto&quot;}

成功提交作業請求後，您可以繼續下一步[檢查作業狀態](#check-status)。

## 檢查作業的狀態{#check-status}

通過將特定作業的`jobId`包含在到`/jobs`端點的GET請求路徑中，可以檢索有關該作業的資訊，如其當前處理狀態。

>[!IMPORTANT]
>
>先前建立的作業的資料僅在作業完成日期的30天內可供檢索。

**API格式**

```http
GET /jobs/{JOB_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{JOB_ID}` | 您要查詢的工作ID。 此ID在[建立工作](#create-job)和[列出所有工作](#list)的成功API回應中傳回在`jobId`下。 |

{style=&quot;table-layout:auto&quot;}

**要求**

以下請求將檢索在請求路徑中提供`jobId`的作業的詳細資訊。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**回應**

成功的回應會傳回指定工作的詳細資料。

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
| `productStatusResponse` | `productResponses`陣列中的每個對象都包含有關特定[!DNL Experience Cloud]應用程式的作業當前狀態的資訊。 |
| `productStatusResponse.status` | 作業的當前狀態類別。 有關[可用狀態類別](#status-categories)及其對應含義的清單，請參見下表。 |
| `productStatusResponse.message` | 作業的特定狀態，對應於狀態類別。 |
| `productStatusResponse.responseMsgCode` | [!DNL Privacy Service]收到之產品回應訊息的標準程式碼。 消息的詳細資訊在`responseMsgDetail`下提供。 |
| `productStatusResponse.responseMsgDetail` | 對工作狀態的更詳細說明。 類似狀態的訊息可能會因產品而異。 |
| `productStatusResponse.results` | 對於某些狀態，某些產品可能會傳回`results`物件，提供`responseMsgDetail`未涵蓋的其他資訊。 |
| `downloadURL` | 如果作業的狀態為`complete`，此屬性會提供URL，以ZIP檔案形式下載作業結果。 此檔案可在工作完成後60天內下載。 |

{style=&quot;table-layout:auto&quot;}

### 作業狀態類別{#status-categories}

下表列出了不同的可能作業狀態類別及其對應含義：

| 狀態類別 | 意義 |
| -------------- | -------- |
| `complete` | 工作已完成，而且（如果需要）檔案會從每個應用程式上傳。 |
| `processing` | 應用程式已確認作業，並且正在處理。 |
| `submitted` | 工作會提交至每個適用的應用程式。 |
| `error` | 處理作業時發生故障——檢索單個作業詳細資訊可以獲得更具體的資訊。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>如果提交的作業具有仍在處理的從屬子作業，則該作業可能仍處於`processing`狀態。

## 後續步驟

您現在知道如何使用[!DNL Privacy Service] API來建立和監控隱私權工作。 有關如何使用用戶介面執行相同任務的資訊，請參閱[Privacy ServiceUI概述](../ui/overview.md)。
