---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 描述檔系統工作——即時客戶描述檔API
topic: guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 2%

---


# 描述系統作業端點（刪除請求）

Adobe Experience Platform可讓您從多個來源擷取資料，並為個別客戶建立強穩的個人檔案。 所吸收的 [!DNL Platform] 資料被儲存在 [!DNL Data Lake] 資料儲存 [!DNL Real-time Customer Profile] 器中。 有時可能需要從描述檔商店刪除資料集或批次，以移除不再需要或錯誤新增的資料。 這需要使 [!DNL Real-time Customer Profile] 用API來建立 [!DNL Profile] 系統工作(也稱為「[!DNL delete request]」)，如有需要，也可加以修改、監視或移除。

>[!NOTE]
>
>如果您嘗試從中刪除資料集或批處理 [!DNL Data Lake]，請訪問目錄 [服務概述](../../catalog/home.md) ，以獲得說明。

## 快速入門

本指南中使用的API端點是 [[!DNL即時客戶配置檔案API]的一部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)。 在繼續之前，請先閱讀快速入門 [指南](getting-started.md) ，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何 [!DNL Experience Platform] API所需之必要標題的重要資訊。

## 檢視刪除請求

刪除請求是長時間執行的非同步程式，這表示您的組織可能同時執行多個刪除請求。 為了查看您的組織當前正在運行的所有刪除請求，您可以對端點執行GET請 `/system/jobs` 求。

您也可以使用選用的查詢參數來篩選回應中傳回的刪除請求清單。 若要使用多個參數，請使用&amp;符號(&amp;)分隔每個參數。

**API格式**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `start` | 依照請求的建立時間，偏移傳回的結果頁面。 範例: *`start=4`* |
| `limit` | 限制傳回的結果數。 範例: *`limit=10`* |
| `page` | 依照請求的建立時間傳回特定的結果頁面。 範例: ***`page=2`*** |
| `sort` | 依特定欄位的升序(*`asc`*)或降序(**`desc`**)排序結果。 傳回多頁結果時，排序參數無法運作。 範例: `sort=batchId:asc` |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應包含「子系」陣列，每個刪除請求都包含該請求的詳細資料的物件。

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{IMS_ORG}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{IMS_ORG}",
      "dataSetId": "5c802d3cd83fc114b741c4b5",
      "jobType": "DELETE",
      "status": "PROCESSING",
      "metrics": "{\"recordsProcessed\":0,\"timeTakenInSec\":15}",
      "createEpoch": 1559025404,
      "updateEpoch": 1559025406
    }
  ]
}
```

| 屬性 | 說明 |
|---|---|
| `_page.count` | 請求總數。 此回應已針對空間截斷。 |
| `_page.next` | 如果有其他結果頁面存在，請以提供的值取代查閱請求中的ID值，以檢 [視下一頁](#view-a-specific-delete-request)`"next"` 結果。 |
| `jobType` | 要建立的作業類型。 在這種情況下，它將始終返回 `"DELETE"`。 |
| `status` | 刪除請求的狀態。 可能的值 `"NEW"`是 `"PROCESSING"`、 `"COMPLETED"`、 `"ERROR"`。 |
| `metrics` | 包含已處理的記錄數(`"recordsProcessed"`)和請求已處理的時間（秒），或請求完成所需時間(`"timeTakenInSec"`)的物件。 |

## 建立刪除請求 {#create-a-delete-request}

啟始新刪除請求是透過對端點的POST請求完成的， `/systems/jobs` 其中，要刪除的資料集或批次的ID在請求的正文中提供。

### 刪除資料集

若要刪除資料集，資料集ID必須包含在POST請求的正文中。 此動作會刪除指定資料集的ALL資料。 [!DNL Experience Platform] 允許您根據記錄和時間序列模式刪除資料集。

>[!CAUTION]
>
> 嘗試使用 [!DNL Profile][!DNL Experience Platform] UI刪除已啟用的資料集時，資料集會因擷取而停用，但在使用API建立刪除要求之前，資料集不會刪除。 如需詳細資訊，請參 [閱本文](#appendix) 件附錄。

**API格式**

```http
POST /system/jobs
```

**請求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| 屬性 | 說明 |
|---|---|
| `dataSetId` | **（必要）** ，您要刪除的資料集ID。 |

**回應**

成功的回應會傳回新建立之刪除要求的詳細資料，包括要求的唯一、系統產生的唯讀ID。 這可用來查詢請求並檢查其狀態。 在 **`status`** 建立請求時，請求會一直保留到 *`"NEW"`* 開始處理為止。 回 **`dataSetId`** 應中的應符合在請 ***`dataSetId`*** 求中傳送的。

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{IMS_ORG}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| 屬性 | 說明 |
|---|---|
| `id` | 刪除請求的唯一、系統產生的唯讀ID。 |
| `dataSetId` | 資料集的ID，如POST請求中所指定。 |

### 刪除批

若要刪除批，批ID必須包含在POST請求的正文中。 請注意，不能根據記錄結構描述刪除資料集的批處理。 只能刪除基於時間系列方案的資料集的批處理。

>[!NOTE]
>
> 無法根據記錄結構描述刪除資料集的批的原因是，記錄類型資料集批會覆蓋以前的記錄，因此無法「撤消」或刪除。 要根據記錄方案消除資料集錯誤批處理的影響，唯一的方法是使用正確的資料重新收錄批，以覆蓋錯誤的記錄。

有關記錄和時間序列行為的更多資訊，請參閱 [概述中有關XDM資料行為](../../xdm/home.md#data-behaviors) 的一 [!DNL XDM System] 節。

**API格式**

```http
POST /system/jobs
```

**請求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| 屬性 | 說明 |
|---|---|
| `batchId` | **（必要）** ，您要刪除的批次ID。 |

**回應**

成功的回應會傳回新建立之刪除要求的詳細資料，包括要求的唯一、系統產生的唯讀ID。 這可用來查詢請求並檢查其狀態。 在 `"status"` 建立請求時，請求會一直保留到 `"NEW"` 開始處理為止。 回 `"batchId"` 應中的應符合在請 `"batchId"` 求中傳送的。

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| 屬性 | 說明 |
|---|---|
| `id` | 刪除請求的唯一、系統產生的唯讀ID。 |
| `batchId` | 批次的ID，如POST請求中所指定。 |

如果您嘗試為記錄資料集批次啟動刪除請求，將會遇到400級錯誤，類似下列：

```json
{
    "requestId": "bc4eb29f-63a8-4653-9133-71238884bb81",
    "errors": {
        "400": [
            {
                "code": "500",
                "message": "Batch can only be specified for EE type 'a294e36d382649dab2cc6ad64a41b674'"
            }
        ]
    }
}
```

## 檢視特定的刪除要求 {#view-a-specific-delete-request}

若要檢視特定的刪除請求，包括詳細資訊（例如其狀態），您可以對端點執行查閱(GET)請求，並在路徑中包含刪除請求的 `/system/jobs` ID。

**API格式**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| 參數 | 說明 |
|---|---|
| `{DELETE_REQUEST_ID}` | **（必要）** ，您要檢視的刪除請求ID。 |

**請求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應會提供刪除請求的詳細資訊，包括其更新狀態。 回應中刪除請求的ID應與請求路徑中傳送的ID相符。

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| 屬性 | 說明 |
|---|---|
| `jobType` | 所建立作業的類型，在此情況下，它將始終返回 `"DELETE"`。 |
| `status` | 刪除請求的狀態。 Possible values: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | 一個陣列，包含已處理的記錄數(`"recordsProcessed"`)和請求已處理的時間（秒），或請求完成所需的時間(`"timeTakenInSec"`)。 |

刪除請求狀態一旦生效， `"COMPLETED"` 您就可以嘗試使用資料存取API存取已刪除的資料，以確認資料已被刪除。 有關如何使用Data Access API存取資料集和批次的指示，請參閱 [Data Access檔案](../../data-access/home.md)。

## 刪除刪除請求

[!DNL Experience Platform] 可讓您刪除先前的請求，這可能因為許多原因（包括刪除作業未完成或在處理階段卡住）而有用。 為了刪除刪除請求，您可以對端點執行DELETE請求，並包括 `/system/jobs` 要刪除到請求路徑的刪除請求的ID。

**API格式**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| 參數 | 說明 |
|---|---|
| {DELETE_REQUEST_ID} | 您要移除的刪除請求ID。 |

**請求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的刪除請求會傳回HTTP狀態200（確定）和空回應主體。 您可以執行GET請求以依其ID檢視刪除請求，以確認刪除請求。 這應該會傳回HTTP狀態404（找不到），表示刪除請求已移除。

## 後續步驟

現在，您已瞭解從中刪除資料集和批處理所涉及的步 [!DNL Profile Store] 驟 [!DNL Experience Platform]，因此您可以安全地刪除錯誤地添加的資料或您的組織不再需要的資料。 請注意，刪除請求無法撤消，因此您只應刪除您確信現在不需要且將來不需要的資料。

## 附錄 {#appendix}

以下資訊是從中刪除資料集的操作的補充 [!DNL Profile Store]。

### 使用 [!DNL Experience Platform] UI刪除資料集

使用使 [!DNL Experience Platform] 用者介面刪除已啟用的資料集時，會開啟對話 [!DNL Profile]方塊，詢問「您確定要從中刪除此資料集嗎 [!DNL Experience Data Lake]? 使用&#39;p[!DNL rofile systems jobs]&#39; API從中刪除此資 [!DNL Profile Service]料集。&quot;

按一 **[!UICONTROL 下UI中的]** 「刪除」會停用擷取資料集，但「不」會自動刪除後端的資料集。 若要永久刪除資料集，必須使用本指南中建立刪除請求的步驟手動 [建立刪除請求](#create-a-delete-request)。

下圖顯示嘗試使用UI刪除已啟用 [!DNL Profile]的資料集時的警告。

![](../images/delete-profile-dataset.png)

有關使用資料集的詳細資訊，請首先閱讀資料集 [概述](../../catalog/datasets/overview.md)。