---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 隱私權工作API端點
description: 瞭解如何使用Privacy Service API管理Experience Cloud應用程式的隱私權工作。
role: Developer
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: 0ffc9648fbc6e6aa3c43a7125f25a98452e8af9a
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 1%

---

# 隱私權工作端點

本文介紹如何使用API呼叫處理隱私權工作。 具體來說，它涵蓋了 `/job` 中的端點 [!DNL Privacy Service] API。 閱讀本指南前，請參閱 [快速入門手冊](./getting-started.md) 如需成功呼叫API所需的重要資訊，包括必要的標題以及如何讀取範例API呼叫。

>[!NOTE]
>
>如果您嘗試管理客戶的同意或選擇退出請求，請參閱 [同意端點指南](./consent.md).

## 列出所有工作 {#list}

您可以透過向以下網站發出GET請求，檢視貴組織內所有可用隱私權工作的清單： `/jobs` 端點。

**API格式**

此請求格式使用 `regulation` 上的查詢引數 `/jobs` 端點，因此開頭是問號(`?`)，如下所示。 列出資源時，Privacy Service API會傳回最多1000個工作並分頁回應。 使用其他查詢引數(`page`， `size`和日期篩選器)，以篩選回應。 您可以使用&amp;符號(`&`)。

>[!TIP]
>
>使用其他查詢引數進一步篩選特定查詢的結果。 例如，您可以探索在指定期間內已提交多少隱私權工作，以及使用它們的狀態 `status`， `fromDate`、和 `toDate` 查詢引數。

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
GET /jobs?regulation={REGULATION}&fromDate={FROMDATE}&toDate={TODATE}&status={STATUS}
```

| 參數 | 說明 |
| --- | --- |
| `{REGULATION}` | 要查詢的規則型別。 接受的值包括： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpa`</li><li>`cpra_usa`</li><li>`ctdpa`</li><li>`ctdpa_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`mhmda`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`ucpa_usa`</li><li>`vcdpa_usa`</li></ul><br>請參閱以下主題的概觀： [支援的法規](../regulations/overview.md) 以取得上述值代表的隱私權法規的詳細資訊。 |
| `{PAGE}` | 要顯示的資料頁（使用0編號）。 預設值為 `0`。 |
| `{SIZE}` | 每個頁面上顯示的結果數。 預設值為 `100` 最大值為 `1000`. 超過最大值會導致API傳回400程式碼錯誤。 |
| `{status}` | 預設行為是包含所有狀態。 如果您指定狀態型別，請求只會傳回符合該狀態型別的隱私權工作。 接受的值包括： <ul><li>`processing`</li><li>`complete`</li><li>`error`</li></ul> |
| `{toDate}` | 此引數會將結果限製為指定日期之前處理的結果。 從請求日期起，系統可以回顧45天。 但是，範圍不能超過30天。<br>它接受YYYY-MM-DD格式。 您提供的日期會解譯為以格林威治標準時間(GMT)表示的終止日期。<br>如果您未提供此引數(以及 `fromDate`)，則預設行為會傳回過去七天內資料的工作。 如果您使用 `toDate`，您也必須使用 `fromDate` 查詢引數。 如果您未同時使用兩者，呼叫會傳回400錯誤。 |
| `{fromDate}` | 此引數會將結果限製為指定日期之後處理的結果。 從請求日期起，系統可以回顧45天。 但是，範圍不能超過30天。<br>它接受YYYY-MM-DD格式。 您提供的日期會解譯為以格林威治標準時間(GMT)表示的請求來源日期。<br>如果您未提供此引數(以及 `toDate`)，則預設行為會傳回過去七天內資料的工作。 如果您使用 `fromDate`，您也必須使用 `toDate` 查詢引數。 如果您未同時使用兩者，呼叫會傳回400錯誤。 |
| `{filterDate}` | 此引數會將結果限製為指定日期處理的結果。 它接受YYYY-MM-DD格式。 系統可以回顧過去45天。 |

{style="table-layout:auto"}

<!-- Not released yet:
<li>`pdpd_vnm`</li> 
 -->

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

成功的回應會傳回工作清單，而每個工作都包含詳細資訊，例如 `jobId`. 在此範例中，回應會包含50個作業的清單，從結果的第三個頁面開始。

### 存取後續頁面

若要在分頁回應中擷取下一組結果，您必須對相同端點進行另一個API呼叫，同時增加 `page` 查詢引數依1。

## 建立隱私權工作 {#create-job}

>[!IMPORTANT]
>
>Privacy Service僅適用於資料主體和消費者權利要求。 不支援或允許將Privacy Service用於資料清理或維護的任何其他用途。 Adobe有法定義務須及時履行。 因此，不允許在Privacy Service上進行負載測試，因為這是僅限生產的環境，且會為有效隱私權請求建立不必要的待處理專案。
>
>現已設定每日硬性上傳限制，以協助防止濫用服務。 發現濫用系統的使用者將會停用其服務的存取權。 隨後將與他們舉行會議，討論他們的動作，並討論可接受的Privacy Service用途。

建立新工作請求之前，您必須先收集有關您要存取、刪除或選擇退出銷售的資料主體的識別資訊。 擁有必要的資料後，您必須在向發出的POST請求裝載中提供該資料 `/jobs` 端點。

>[!NOTE]
>
>相容的Adobe Experience Cloud應用程式使用不同的值來識別資料主體。 請參閱以下指南： [Privacy Service和Experience Cloud應用程式](../experience-cloud-apps.md) 以取得應用程式所需識別碼的詳細資訊。 如需判斷傳送至哪些ID的一般指引 [!DNL Privacy Service]，請參閱上的檔案 [隱私權請求中的身分資料](../identity-data.md).

此 [!DNL Privacy Service] API支援兩種針對個人資料的工作請求：

* [存取和/或刪除](#access-delete)：存取（讀取）或刪除個人資料。
* [選擇退出銷售](#opt-out)：將個人資料標示為不出售。

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
    "analyticsDeleteMethod": "anonymize",
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| 屬性 | 說明 |
| --- | --- |
| `companyContexts` **（必要）** | 包含貴組織驗證資訊的陣列。 每個列出的識別碼都包含下列屬性： <ul><li>`namespace`：識別碼的名稱空間。</li><li>`value`：識別碼的值。</li></ul>它是 **必填** 其中一個識別碼使用 `imsOrgId` 作為 `namespace`，及其 `value` 包含貴組織的唯一ID。 <br/><br/>其他識別碼可以是產品特定的公司限定詞(例如， `Campaign`)，可識別與屬於您組織的Adobe應用程式的整合。 可能的值包括帳戶名稱、使用者端代碼、租使用者ID或其他應用程式識別碼。 |
| `users` **（必要）** | 一個陣列，其中包含您要存取或刪除其資訊的至少一個使用者的集合。 單一請求中最多可提供1000位使用者。 每個使用者物件包含下列資訊： <ul><li>`key`：使用者的識別碼，用於限定回應資料中的個別作業ID。 為此值選擇唯一且易於識別的字串是最佳做法，以便日後可以輕鬆參考或查詢。</li><li>`action`：列出要對使用者資料採取的所需動作的陣列。 根據您要採取的動作，此陣列必須包括 `access`， `delete`，或兩者。</li><li>`userIDs`：使用者的身分識別集合。 單一使用者可擁有的身分數量限製為九個。 每個身分都包含 `namespace`， a `value`和名稱空間限定詞(`type`)。 請參閱 [附錄](appendix.md) 以取得這些必要屬性的詳細資訊。</li></ul> 如需的詳細說明，請參閱： `users` 和 `userIDs`，請參閱 [疑難排解指南](../troubleshooting-guide.md#user-ids). |
| `include` **（必要）** | 要包含在處理中的一系列Adobe產品。 如果此值遺失或空白，將會拒絕要求。 僅包含貴組織已整合的產品。 請參閱以下小節： [接受的產品值](appendix.md) 詳細資訊。 |
| `expandIDs` | 選擇性屬性，設定為時 `true`，代表應用程式中ID處理的最佳化(目前僅支援 [!DNL Analytics])。 如果省略，此值會預設為 `false`. |
| `priority` | Adobe Analytics使用的選用屬性，可設定處理請求的優先順序。 接受的值為 `normal` 和 `low`. 如果 `priority` 會省略，預設行為為 `normal`. |
| `analyticsDeleteMethod` | 選擇性屬性，指定Adobe Analytics處理個人資料的方式。 這個屬性接受兩個可能的值： <ul><li>`anonymize`：特定使用者ID集合所參考的所有資料都會設為匿名。 如果 `analyticsDeleteMethod` 會省略，此為預設行為。</li><li>`purge`：所有資料都會完全移除。</li></ul> |
| `mergePolicyId` | 對即時客戶個人檔案提出隱私權請求時(`profileService`)，您可以選擇提供特定 [合併原則](../../profile/merge-policies/overview.md) ，以便用於ID拼接。 透過指定合併原則，隱私權請求可在傳回客戶資料時包含對象資訊。 每個請求只能指定一個合併原則。 如果未提供合併原則，回應中不會包含分段資訊。 |
| `regulation` **（必要）** | 隱私權工作的法規。 接受下列值： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>請參閱以下主題的概觀： [支援的法規](../regulations/overview.md) 以取得上述值代表的隱私權法規的詳細資訊。 |

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

成功提交工作請求後，您可以繼續的下一個步驟 [檢查工作狀態](#check-status).

## 檢查工作的狀態 {#check-status}

您可以擷取特定工作的相關資訊，例如其目前的處理狀態，方法是加入該工作的 `jobId` 在GET請求的路徑中 `/jobs` 端點。

>[!IMPORTANT]
>
>先前建立之工作的資料只能在工作完成日期後30天內擷取。

**API格式**

```http
GET /jobs/{JOB_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{JOB_ID}` | 您要查閱之工作的ID。 此ID會傳回至 `jobId` 在成功的API回應中 [建立工作](#create-job) 和 [列出所有工作](#list). |

{style="table-layout:auto"}

**要求**

以下請求會擷取下列工作之詳細資訊： `jobId` 請求路徑中會提供。

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
| `productStatusResponse` | 內的每個物件 `productResponses` 陣列包含有關特定工作目前狀態的資訊 [!DNL Experience Cloud] 應用程式。 |
| `productStatusResponse.status` | 工作的目前狀態類別。 請參閱下表，瞭解以下清單： [可用狀態類別](#status-categories) 以及它們對應的意義。 |
| `productStatusResponse.message` | 工作的特定狀態，對應於狀態類別。 |
| `productStatusResponse.responseMsgCode` | 接收的產品回應訊息的標準代碼 [!DNL Privacy Service]. 訊息的詳細資訊提供在 `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | 有關工作狀態的更詳細說明。 類似狀態的訊息可能因產品而異。 |
| `productStatusResponse.results` | 針對特定狀態，部分產品可能會傳回 `results` 提供未涵蓋之其他資訊的物件。 `responseMsgDetail`. |
| `downloadURL` | 如果工作的狀態為 `complete`，此屬性會提供一個URL來將工作結果下載為ZIP檔案。 工作完成後60天內可下載此檔案。 |

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
>已提交的工作可能仍會保留在 `processing` 指出它是否有仍在處理的相依子工作。

## 後續步驟

您現在知道如何使用 [!DNL Privacy Service] API。 如需有關如何使用使用者介面執行相同工作的資訊，請參閱 [Privacy Service UI總覽](../ui/overview.md).
