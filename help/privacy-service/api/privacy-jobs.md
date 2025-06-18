---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 隱私權工作API端點
description: 瞭解如何使用Privacy Service API管理Experience Cloud應用程式的隱私權工作。
role: Developer
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: c2394035dd6bd4fe6dbb443e4db13934a27066a6
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 1%

---

# 隱私權工作端點

>[!IMPORTANT]
>
>為了支援不斷增加的美國州隱私權法，Privacy Service正在變更其`regulation_type`值。 使用包含從&#x200B;**2025年6月12日**&#x200B;開始之狀態縮寫（例如`ucpa_ut_usa`）的新值。 較舊的值（例如，`ucpa_usa`）在&#x200B;**2025年7月28日**&#x200B;之後停止運作。
>
>在此期限之前更新您的整合，以避免請求失敗。

本文介紹如何使用API呼叫處理隱私權工作。 具體來說，它涵蓋[!DNL Privacy Service] API中`/job`端點的使用。 閱讀本指南之前，請參閱[快速入門手冊](./getting-started.md)以取得成功呼叫API所需瞭解的重要資訊，包括必要的標頭以及如何讀取範例API呼叫。

>[!NOTE]
>
>如果您嘗試管理客戶的同意或選擇退出請求，請參閱[同意端點指南](./consent.md)。

## 列出所有工作 {#list}

您可以透過向`/jobs`端點發出GET請求，檢視組織內所有可用隱私權工作的清單。

**API格式**

此要求格式在`/jobs`端點上使用`regulation`查詢引數，因此它以問號(`?`)開頭，如下所示。 列出資源時，Privacy Service API會傳回最多1000個工作並分頁回應。 使用其他查詢引數（`page`、`size`和日期篩選器）來篩選回應。 您可以使用&amp;符號(`&`)來分隔多個引數。

>[!TIP]
>
>使用其他查詢引數進一步篩選特定查詢的結果。 例如，您可以探索在指定期間內已提交多少隱私權工作，以及使用`status`、`fromDate`和`toDate`查詢引數的其狀態為何。

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
GET /jobs?regulation={REGULATION}&fromDate={FROMDATE}&toDate={TODATE}&status={STATUS}
```

| 參數 | 說明 |
| --- | --- |
| `{REGULATION}` | 要查詢的規則型別。 接受的值包括： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpa_co_usa`</li><li>`cpra_ca_usa`</li><li>`ctdpa_ct_usa`</li><li>`dpdpa_de_usa`</li><li>`fdbr_fl_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`icdpa_ia_usa`</li><li>`lgpd_bra`</li><li>`mcdpa_mn_usa`</li><li>`mcdpa_mt_usa`</li><li>`mhmda_wa_usa`</li><li>`ndpa_ne_usa`</li><li>`nhpa_nh_usa`</li><li>`njdpa_nj_usa`</li><li>`nzpa_nzl`</li><li>`ocpa_or_usa`</li><li>`pdpa_tha`</li><li>`ql25_qc_can`</li><li>`tdpsa_tx_usa`</li><li>`tipa_tn_usa`</li><li>`ucpa_ut_usa`</li><li>`vcdpa_va_usa`</li></ul><br>如需上述值所代表隱私權法規的詳細資訊，請參閱[支援法規](../regulations/overview.md)的概觀。 |
| `{PAGE}` | 要顯示的資料頁（使用0編號）。 預設值為 `0`。 |
| `{SIZE}` | 每個頁面上顯示的結果數。 預設值為`100`，最大值為`1000`。 超過最大值會導致API傳回400程式碼錯誤。 |
| `{status}` | 預設行為是包含所有狀態。 如果您指定狀態型別，請求只會傳回符合該狀態型別的隱私權工作。 接受的值包括： <ul><li>`processing`</li><li>`complete`</li><li>`error`</li></ul> |
| `{toDate}` | 此引數會將結果限製為指定日期之前處理的結果。 從請求日期起，系統可以回顧45天。 但是，範圍不能超過30天。<br>它接受YYYY-MM-DD格式。 您提供的日期會解譯為以格林威治標準時間(GMT)表示的終止日期。<br>如果您未提供此引數（以及相對應的`fromDate`），預設行為會傳回過去七天資料傳回的工作。 如果您使用`toDate`，您也必須使用`fromDate`查詢引數。 如果您未同時使用兩者，呼叫會傳回400錯誤。 |
| `{fromDate}` | 此引數會將結果限製為指定日期之後處理的結果。 從請求日期起，系統可以回顧45天。 但是，範圍不能超過30天。<br>它接受YYYY-MM-DD格式。 您提供的日期會解譯為以格林威治標準時間(GMT)表示的請求來源日期。<br>如果您未提供此引數（以及相對應的`toDate`），預設行為會傳回過去七天資料傳回的工作。 如果您使用`fromDate`，您也必須使用`toDate`查詢引數。 如果您未同時使用兩者，呼叫會傳回400錯誤。 |
| `{filterDate}` | 此引數會將結果限製為指定日期處理的結果。 它接受YYYY-MM-DD格式。 系統可以回顧過去45天。 |

{style="table-layout:auto"}

**要求**

下列請求會從頁面大小為50的第三個頁面開始，擷取組織內所有工作的分頁清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的回應會傳回工作清單，每個工作都包含詳細資訊，例如其`jobId`。 在此範例中，回應會包含50個作業的清單，從結果的第三個頁面開始。

### 存取後續頁面

若要擷取分頁回應中的下一組結果，您必須對相同端點進行另一個API呼叫，同時將`page`查詢引數增加1。

## 建立隱私權工作 {#create-job}

>[!IMPORTANT]
>
>Privacy Service僅適用於資料主體和消費者權利要求。 不支援或允許將Privacy Service用於資料清理或維護的任何其他用途。 Adobe有法定義務須及時履行。 因此，不允許在Privacy Service上進行載入測試，因為這是僅限生產的環境，且會為有效隱私權請求建立不必要的待處理專案。
>
>現已設定每日硬性上傳限制，以協助防止濫用服務。 發現濫用系統的使用者將會停用其服務的存取權。 隨後將與他們舉行會議，討論他們的動作，並討論Privacy Service的可接受用途。

建立新工作請求之前，您必須先收集有關您要存取、刪除或選擇退出銷售的資料主體的識別資訊。 擁有必要的資料後，必須在POST要求的裝載中提供該資料給`/jobs`端點。

>[!NOTE]
>
>相容的Adobe Experience Cloud應用程式使用不同的值來識別資料主體。 請參閱[Privacy Service和Experience Cloud應用程式](../experience-cloud-apps.md)的指南，以取得應用程式所需識別碼的詳細資訊。 如需決定要將哪些ID傳送至[!DNL Privacy Service]的更一般指引，請參閱隱私權要求[&#128279;](../identity-data.md)中身分資料的檔案。

[!DNL Privacy Service] API支援兩種針對個人資料的工作請求：

* [存取和/或刪除](#access-delete)：存取（讀取）或刪除個人資料。
* [選擇退出銷售](#opt-out)：將個人資料標示為不銷售。

>[!IMPORTANT]
>
>雖然存取和刪除請求可以合併為單一API呼叫，但必須個別提出選擇退出請求。

### 建立存取/刪除工作 {#access-delete}

本節將示範如何使用API提出存取/刪除工作請求。

**API格式**

```http
POST /jobs
```

**要求**

以下請求會建立新的作業請求，由承載中提供的屬性設定，如下所述。

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
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| 屬性 | 說明 |
| --- | --- |
| `companyContexts` **（必要）** | 包含貴組織驗證資訊的陣列。 每個列出的識別碼都包含下列屬性： <ul><li>`namespace`：識別碼的名稱空間。</li><li>`value`：識別碼的值。</li></ul>**必要**&#x200B;其中一個識別碼使用`imsOrgId`做為其`namespace`，其`value`包含您組織的唯一識別碼。 <br/><br/>其他識別碼可以是產品特定的公司限定詞（例如，`Campaign`），用於識別與屬於您組織的Adobe應用程式的整合。 可能的值包括帳戶名稱、使用者端代碼、租使用者ID或其他應用程式識別碼。 |
| `users` **（必要）** | 一個陣列，其中包含您要存取或刪除其資訊的至少一個使用者的集合。 單一請求中最多可提供1000位使用者。 每個使用者物件包含下列資訊： <ul><li>`key`：用於限定回應資料中個別工作ID的使用者識別碼。 為此值選擇唯一且易於識別的字串是最佳做法，以便日後可以輕鬆參考或查詢。</li><li>`action`：列出要對使用者資料採取的所需動作的陣列。 根據您要採取的動作，此陣列必須包含`access`、`delete`或兩者。</li><li>`userIDs`：使用者的身分識別集合。 單一使用者可擁有的身分數量限製為九個。 每個身分都包含`namespace`、`value`和名稱空間限定詞(`type`)。 如需這些必要屬性的詳細資訊，請參閱[附錄](appendix.md)。</li></ul> 如需`users`和`userIDs`的更詳細說明，請參閱[疑難排解指南](../troubleshooting-guide.md#user-ids)。 |
| `include` **（必要）** | 要包含在處理中的一系列Adobe產品。 如果此值遺失或空白，將會拒絕要求。 僅包含貴組織已整合的產品。 如需詳細資訊，請參閱附錄中有關[接受產品值](appendix.md)的章節。 |
| `expandIDs` | 選擇性屬性，當設為`true`時，代表處理應用程式中ID的最佳化（目前僅由[!DNL Analytics]支援）。 如果省略，此值會預設為`false`。 |
| `priority` | Adobe Analytics使用的選用屬性，可設定處理請求的優先順序。 接受的值為 `normal` 和 `low`。如果省略`priority`，預設行為是`normal`。 |
| `mergePolicyId` | 針對Real-time Customer Profile (`profileService`)提出隱私權要求時，您可以選擇提供要用於ID拼接的特定[合併原則](../../profile/merge-policies/overview.md)的ID。 透過指定合併原則，隱私權請求可在傳回客戶資料時包含對象資訊。 每個請求只能指定一個合併原則。 如果未提供合併原則，回應中不會包含分段資訊。 |
| `regulation` **（必要）** | 隱私權工作的法規。 接受下列值： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>如需上述值所代表隱私權法規的詳細資訊，請參閱[支援法規](../regulations/overview.md)的概觀。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回新建立工作的詳細資訊。

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
| `jobId` | 唯讀，系統為作業產生的唯一ID。 此值用於查詢特定工作的下一個步驟。 |

{style="table-layout:auto"}

成功提交工作請求後，您可以繼續下一步驟[檢查工作狀態](#check-status)。

## 檢查工作的狀態 {#check-status}

您可以在GET要求到`/jobs`端點的路徑中包含特定工作的`jobId`，以擷取其相關資訊，例如其目前處理狀態。

>[!IMPORTANT]
>
>先前建立之工作的資料只能在工作完成日期後30天內擷取。

**API格式**

```http
GET /jobs/{JOB_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{JOB_ID}` | 您要查閱之工作的ID。 在[建立工作](#create-job)和[列出所有工作](#list)的成功API回應中，此ID在`jobId`下傳回。 |

{style="table-layout:auto"}

**要求**

下列請求會擷取其請求路徑中提供`jobId`之工作的詳細資料。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的回應會傳回指定工作的詳細資訊。

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
| `productStatusResponse` | `productResponses`陣列中的每個物件都包含與特定[!DNL Experience Cloud]應用程式相關之工作目前狀態的資訊。 |
| `productStatusResponse.status` | 工作的目前狀態類別。 請參閱下表以取得[可用狀態類別](#status-categories)及其對應含義的清單。 |
| `productStatusResponse.message` | 工作的特定狀態，對應於狀態類別。 |
| `productStatusResponse.responseMsgCode` | 由[!DNL Privacy Service]接收的產品回應訊息的標準代碼。 已在`responseMsgDetail`下提供訊息的詳細資料。 |
| `productStatusResponse.responseMsgDetail` | 有關工作狀態的更詳細說明。 類似狀態的訊息可能因產品而異。 |
| `productStatusResponse.results` | 針對特定狀態，某些產品可能會傳回`results`物件，該物件提供`responseMsgDetail`未涵蓋的其他資訊。 |
| `downloadURL` | 如果工作的狀態為`complete`，此屬性會提供URL以將工作結果下載為ZIP檔。 工作完成後60天內可下載此檔案。 |

{style="table-layout:auto"}

### 工作狀態類別 {#status-categories}

下表列出不同的可能工作狀態類別及其對應含義：

| 狀態類別 | 含義 |
| -------------- | -------- |
| `complete` | 工作已完成，且會從每個應用程式上傳檔案（如有需要）。 |
| `processing` | 應用程式已確認工作且目前正在處理中。 |
| `submitted` | 工作已提交給每個適用的應用程式。 |
| `error` | 處理作業時某些失敗 — 擷取個別作業詳細資料可取得更具體的資訊。 |

{style="table-layout:auto"}

>[!NOTE]
>
>如果送出的工作具有仍在處理的相依子工作，則該工作可能維持在`processing`狀態。

## 後續步驟

您現在知道如何使用[!DNL Privacy Service] API建立及監控隱私權工作。 如需有關如何使用使用者介面執行相同工作的資訊，請參閱[Privacy Service UI總覽](../ui/overview.md)。
