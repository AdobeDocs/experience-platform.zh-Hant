---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 隱私作業API終結點
description: 瞭解如何使用Experience CloudAPI管理Privacy Service應用程式的隱私作業。
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 1%

---

# 隱私作業終結點

本文檔介紹如何使用API調用處理隱私作業。 具體來說，它包括 `/job` 端點 [!DNL Privacy Service] API。 閱讀本指南前，請參閱 [入門指南](./getting-started.md) 要成功調用API，您需要瞭解的重要資訊，包括必需的標頭以及如何讀取示例API調用。

>[!NOTE]
>
>如果您試圖管理客戶的同意或退出請求，請參閱 [同意端點指南](./consent.md)。

## 列出所有作業 {#list}

您可以通過向以下站點發出GET請求來查看組織中所有可用隱私作業的清單： `/jobs` 端點。

**API格式**

此請求格式使用 `regulation` 查詢參數 `/jobs` 端點，因此它以問號(`?`)，如下所示。 響應已分頁，允許您使用其他查詢參數(`page` 和 `size`)以篩選響應。 可以使用和符號分隔多個參數(`&`)。

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| 參數 | 說明 |
| --- | --- |
| `{REGULATION}` | 要查詢的規則類型。 接受的值包括： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>請參閱 [支援的法規](../regulations/overview.md) 的子菜單。 |
| `{PAGE}` | 要顯示的資料頁，使用基於0的編號。 預設值為 `0`。 |
| `{SIZE}` | 要在每頁上顯示的結果數。 預設值為 `1` 最大值是 `100`。 超過最大值將導致API返回400代碼錯誤。 |

{style="table-layout:auto"}

**要求**

以下請求從頁面大小為50的第三頁開始檢索組織中所有作業的分頁清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的響應返回作業清單，每個作業都包含詳細資訊，如 `jobId`。 在本示例中，響應將包含從結果第三頁開始的50個作業的清單。

### 訪問後續頁

要在分頁響應中獲取下一組結果，必須對同一端點進行另一個API調用，同時增加 `page` 查詢參數按1。

## 建立隱私作業 {#create-job}

>[!IMPORTANT]
>
>Privacy Service僅用於資料主題和消費者權利請求。 不支援或不允許使用Privacy Service進行資料清理或維護。 Adobe有法律義務及時履行這些義務。 因此，不允許對Privacy Service進行負載測試，因為它是僅生產環境，並會建立有效隱私請求的不必要的積壓。
>
>現在已設定硬性每日上載限制，以幫助防止濫用服務。 發現濫用系統的用戶將禁用其對服務的訪問權限。 隨後將與他們舉行會議，討論他們的行動並討論可接受的Privacy Service用途。

在建立新作業請求之前，必須首先收集有關要訪問、刪除或選擇不銷售其資料的資料主題的標識資訊。 一旦您擁有了所需資料，則必須在POST請求的負載中提供該資料 `/jobs` 端點。

>[!NOTE]
>
>相容的Adobe Experience Cloud應用程式使用不同的值來識別資料主題。 請參閱上的指南 [Privacy Service和Experience Cloud應用程式](../experience-cloud-apps.md) 的子菜單。 有關確定要發送到的ID的更一般指導 [!DNL Privacy Service]，請參閱上的文檔 [隱私請求中的身份資料](../identity-data.md)。

的 [!DNL Privacy Service] API支援兩種類型的個人資料作業請求：

* [訪問和/或刪除](#access-delete):訪問（讀取）或刪除個人資料。
* [退出銷售](#opt-out):將個人資料標籤為不銷售。

>[!IMPORTANT]
>
>雖然訪問和刪除請求可以合併為單個API調用，但是選擇退出請求必須單獨進行。

### 建立訪問/刪除作業 {#access-delete}

本節演示如何使用API進行訪問/刪除作業請求。

**API格式**

```http
POST /jobs
```

**要求**

以下請求將建立新作業請求，該請求由負載中提供的屬性進行配置，如下所述。

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
| `companyContexts` **(必填)** | 包含組織驗證資訊的陣列。 每個列出的標識符包括以下屬性： <ul><li>`namespace`:標識符的命名空間。</li><li>`value`:標識符的值。</li></ul>是 **要求** 其中一個標識符使用 `imsOrgId` 作為 `namespace`, `value` 包含組織的唯一ID。 <br/><br/>其他標識符可以是特定於產品的公司限定符(例如， `Campaign`)，它標識與屬於您組織的Adobe應用程式的整合。 潛在值包括帳戶名、客戶端代碼、租戶ID或其他應用程式標識符。 |
| `users` **(必填)** | 包含至少一個用戶集合的陣列，您要訪問或刪除其資訊。 在單個請求中最多可提供1000個用戶ID。 每個用戶對象都包含以下資訊： <ul><li>`key`:用於限定響應資料中的單獨作業ID的用戶的標識符。 最好為此值選擇一個唯一且易於識別的字串，以便以後可以輕鬆地引用或查找它。</li><li>`action`:一個陣列，它列出了對用戶資料執行的所需操作。 根據您要執行的操作，此陣列必須包括 `access`。 `delete`，或兩者兼有。</li><li>`userIDs`:用戶的標識集合。 單個用戶可以擁有的標識數限制為9。 每個標識都由 `namespace`的 `value`，和命名空間限定符(`type`)。 查看 [附錄](appendix.md) 的子菜單。</li></ul> 有關 `users` 和 `userIDs`，請參見 [故障排除指南](../troubleshooting-guide.md#user-ids)。 |
| `include` **(必填)** | 要包含在您的處理中的Adobe產品陣列。 如果此值缺失或為空，則請求將被拒絕。 僅包括您的組織與之整合的產品。 請參閱 [接受的產品值](appendix.md) 的雙曲餘切值。 |
| `expandIDs` | 設定為時的可選屬性 `true`，表示處理應用程式中ID的優化(當前僅受 [!DNL Analytics])。 如果省略，此值預設為 `false`。 |
| `priority` | Adobe Analytics使用的可選屬性，用於設定處理請求的優先順序。 接受的值為 `normal` 和 `low`。 如果 `priority` 省略，預設行為為 `normal`。 |
| `analyticsDeleteMethod` | 一個可選屬性，指定Adobe Analytics應如何處理個人資料。 此屬性接受兩個可能的值： <ul><li>`anonymize`:給定的用戶ID集合引用的所有資料都是匿名的。 如果 `analyticsDeleteMethod` 省略，這是預設行為。</li><li>`purge`:所有資料都被完全刪除。</li></ul> |
| `mergePolicyId` | 對即時客戶配置檔案(`profileService`)，可以選擇提供特定 [合併策略](../../profile/merge-policies/overview.md) 你想用於ID縫合。 通過指定合併策略，隱私請求可以在返回客戶資料時包括段資訊。 每個請求只能指定一個合併策略。 如果未提供合併策略，則分段資訊不包括在響應中。 |
| `regulation` **(必填)** | 隱私工作的規定。 接受以下值： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>請參閱 [支援的法規](../regulations/overview.md) 的子菜單。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回新建立作業的詳細資訊。

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
| `jobId` | 作業的只讀、唯一的系統生成ID。 該值用於查找特定作業的下一步。 |

{style="table-layout:auto"}

成功提交作業請求後，您可以繼續下一步 [檢查作業的狀態](#check-status)。

## 檢查作業的狀態 {#check-status}

您可以通過包括特定作業的來檢索有關特定作業的資訊，如其當前處理狀態 `jobId` 在GET請求到 `/jobs` 端點。

>[!IMPORTANT]
>
>先前建立的作業的資料僅在作業完成日期後30天內可供檢索。

**API格式**

```http
GET /jobs/{JOB_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{JOB_ID}` | 要查找的作業的ID。 此ID在 `jobId` 成功的API響應 [建立作業](#create-job) 和 [列出所有作業](#list)。 |

{style="table-layout:auto"}

**要求**

以下請求檢索其 `jobId` 在請求路徑中提供。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的響應返回指定作業的詳細資訊。

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
| `productStatusResponse` | 中的每個對象 `productResponses` 陣列包含有關特定作業的當前狀態的資訊 [!DNL Experience Cloud] 的子菜單。 |
| `productStatusResponse.status` | 作業的當前狀態類別。 請參閱下表，瞭解 [可用狀態類別](#status-categories) 以及它們的對應含義。 |
| `productStatusResponse.message` | 作業的特定狀態，對應於狀態類別。 |
| `productStatusResponse.responseMsgCode` | 接收的產品響應消息的標準代碼 [!DNL Privacy Service]。 消息的詳細資訊如下 `responseMsgDetail`。 |
| `productStatusResponse.responseMsgDetail` | 作業狀態的更詳細說明。 類似狀態的消息可能因產品而異。 |
| `productStatusResponse.results` | 對於某些狀態，某些產品可能返回 `results` 提供未包含的附加資訊的對象 `responseMsgDetail`。 |
| `downloadURL` | 如果作業的狀態為 `complete`，此屬性提供URL以將作業結果作為ZIP檔案下載。 此檔案可在作業完成後60天內下載。 |

{style="table-layout:auto"}

### 作業狀態類別 {#status-categories}

下表列出了不同的可能作業狀態類別及其相應含義：

| 狀態類別 | 含義 |
| -------------- | -------- |
| `complete` | 作業已完成，並且（如果需要）從每個應用程式上載檔案。 |
| `processing` | 應用程式已確認該作業，並且當前正在處理。 |
| `submitted` | 作業將提交到每個適用的應用程式。 |
| `error` | 處理作業時出現了故障 — 通過檢索單個作業詳細資訊可獲取更具體的資訊。 |

{style="table-layout:auto"}

>[!NOTE]
>
>提交的作業可能仍在 `processing` 狀態：如果它具有仍在處理的從屬子作業。

## 後續步驟

您現在知道如何使用 [!DNL Privacy Service] API。 有關如何使用用戶介面執行相同任務的資訊，請參閱 [Privacy ServiceUI概述](../ui/overview.md)。
