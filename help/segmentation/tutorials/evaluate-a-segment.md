---
keywords: Experience Platform；首頁；熱門主題；區段評估；區段服務；分段；評估區段；存取區段結果；評估和存取區段；
solution: Experience Platform
title: 評估和存取區段結果
type: Tutorial
description: 請依照本教學課程，了解如何使用Adobe Experience Platform區段服務API評估區段並存取區段結果。
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 0%

---

# 評估和存取區段結果

本檔案提供評估區段和使用存取區段結果的教學課程 [[!DNL Segmentation API]](../api/getting-started.md).

## 快速入門

本教學課程需要妥善了解 [!DNL Adobe Experience Platform] 與建立受眾區隔相關的服務。 開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的客戶設定檔。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):可讓您從 [!DNL Real-Time Customer Profile] 資料。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):Platform用來組織客戶體驗資料的標準化架構。 為了最能善用區段，請確定您的資料已根據 [資料模型最佳實務](../../xdm/schema/best-practices.md).
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

### 必要標題

本教學課程也要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] API。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：承載 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有POST、PUT和PATCH請求都需要額外的標題：

- 內容類型：application/json

## 評估區段 {#evaluate-a-segment}

開發、測試並儲存區段定義後，您就可以透過排程評估或隨需評估來評估區段。

[計畫評估](#scheduled-evaluation) （也稱為「排程分段」）可讓您建立在特定時間執行匯出作業的循環排程，但 [隨選評估](#on-demand-evaluation) 包括建立區段工作以立即建立對象。 各步驟的步驟如下所述。

如果您尚未完成 [使用區段API建立區段](./create-a-segment.md) 教學課程或使用 [區段產生器](../ui/overview.md)，請先完成此操作，再繼續本教學課程。

## 計畫評估 {#scheduled-evaluation}

透過排程評估，您的組織可建立循環排程以自動執行匯出作業。

>[!NOTE]
>
>可針對最多五(5)個合併原則的沙箱啟用排程評估 [!DNL XDM Individual Profile]. 如果貴組織有五個以上的合併政策 [!DNL XDM Individual Profile] 在單一沙箱環境中，您將無法使用排程的評估。

### 建立排程

向 `/config/schedules` 端點，您可以建立排程，並包含應觸發排程的特定時間。

有關使用此端點的更多詳細資訊，請參見 [schedules endpoint guide（計畫端點指南）](../api/schedules.md#create)

### 啟用排程

依預設，排程在建立時非作用中，除非 `state` 屬性設為 `active` 在建立(POST)請求內文中。 您可以啟用排程(設定 `state` to `active`)，向 `/config/schedules` 端點，並在路徑中納入排程的ID。

有關使用此端點的更多詳細資訊，請參見 [schedules endpoint guide（計畫端點指南）](../api/schedules.md#update-state)

### 更新排程時間

您可以透過向 `/config/schedules` 端點，並在路徑中納入排程的ID。

有關使用此端點的更多詳細資訊，請參見 [schedules endpoint guide（計畫端點指南）](../api/schedules.md#update-schedule)

## 隨選評估

隨需評估可讓您建立區段工作，以便隨時產生受眾區段。 與排程評估不同，這只會在要求時發生，且不會重複執行。

### 建立區段作業

區段工作是非同步程式，可依需求建立受眾區段。 它會參考區段定義，以及任何控制如何 [!DNL Real-Time Customer Profile] 合併您的設定檔片段的重疊屬性。 區段工作成功完成後，您可以收集區段的各種資訊，例如處理期間可能發生的任何錯誤，以及對象的最終大小。 每當您要重新整理目前符合區段定義資格的對象時，都需要執行區段工作。

您可以透過向 `/segment/jobs` 端點 [!DNL Real-Time Customer Profile] API。

有關使用此端點的更多詳細資訊，請參見 [區段作業端點指南](../api/segment-jobs.md#create)

### 查找段作業狀態

您可以使用 `id` ，以便執行查閱請求(GET)以檢視工作的目前狀態。

有關使用此端點的更多詳細資訊，請參見 [區段作業端點指南](../api/segment-jobs.md#get)

## 解譯區段結果

區段作業成功執行時， `segmentMembership` 區段中包含之每個設定檔的對應都會更新。 `segmentMembership` 也會儲存擷取至的任何預先評估對象區段 [!DNL Platform]，允許與其他解決方案(例如 [!DNL Adobe Audience Manager].

下列範例顯示 `segmentMembership` 屬性如同每個個別設定檔記錄：

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `lastQualificationTime` | 建立區段成員資格斷言以及設定檔輸入或退出區段時的時間戳記。 |
| `status` | 目前請求中區段參與率的狀態。 必須等於下列其中一個已知值： <ul><li>`realized`:實體符合區段資格。</li><li>`exited`:實體正在退出區段。</li></ul> |

>[!NOTE]
>
>任何位於 `exited` 狀態超過30天，根據 `lastQualificationTime`，將會遭刪除。

## 存取區段結果

您可透過下列兩種方式之一存取區段作業的結果：您可以存取個別設定檔，或將整個對象匯出至資料集。

以下各節將更詳細地介紹這些選項。

## 查詢設定檔

如果您知道要存取的特定設定檔，可以使用 [!DNL Real-Time Customer Profile] API。 存取個別設定檔的完整步驟可在 [使用設定檔API存取即時客戶設定檔資料](../../profile/api/entities.md) 教學課程。

## 匯出區段 {#export}

分段作業成功完成後( `status` 屬性為「SUCCEEDED」)，您可以將對象匯出至資料集，以便存取資料集並據以處理。

匯出對象需要下列步驟：

- [建立目標資料集](#create-a-target-dataset)  — 建立資料集以保留對象成員。
- [在資料集中產生對象設定檔](#generate-profiles)  — 根據區段工作的結果，以XDM個別設定檔填入資料集。
- [監視導出進度](#monitor-export-progress)  — 檢查導出過程的當前進度。
- [讀取受眾資料](#next-steps)  — 擷取代表您對象成員的產生XDM個別設定檔。

### 建立目標資料集 {#create-dataset}

匯出對象時，必須先建立目標資料集。 請務必正確設定資料集，以確保匯出成功。

其中一項主要考量事項為資料集所依據的結構(`schemaRef.id` （在以下的API範例請求中）。 若要匯出區段，資料集必須以 [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`)。 聯合結構是系統產生的唯讀結構，會匯總共用相同類別之結構的欄位（在此例中是XDM個別設定檔類別）。 如需聯合檢視結構的詳細資訊，請參閱 [Schema Registry開發人員指南的「Real-Time Customer Profile」部分](../../xdm/api/getting-started.md).

建立必要資料集的方式有兩種：

- **使用API:** 本教學課程中後續的步驟將概述如何建立參考資料集 [!DNL XDM Individual Profile Union Schema] 使用 [!DNL Catalog] API。
- **使用UI:** 若要使用 [!DNL Adobe Experience Platform] 使用者介面來建立參考聯合結構的資料集，請依照 [UI教學課程](../ui/overview.md) 接著，返回本教學課程以繼續進行 [產生對象設定檔](#generate-profiles).

如果您已有相容的資料集且知道其ID，可以直接繼續進行 [產生對象設定檔](#generate-profiles).

**API格式**

```http
POST /dataSets
```

**要求**

下列請求會建立新資料集，提供裝載中的設定參數。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 資料集的描述性名稱。 |
| `schemaRef.id` | 與資料集關聯的聯合檢視（結構）ID。 |

**回應**

成功的回應會傳回一個陣列，內含新建立資料集的唯讀、系統產生的唯一ID。 若要成功匯出受眾成員，需要正確設定的資料集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 產生對象成員的設定檔 {#generate-profiles}

在您擁有持續存在聯合的資料集後，您可以建立匯出工作，對 `/export/jobs` 端點 [!DNL Real-Time Customer Profile] API，並提供您要匯出之區段的資料集ID和區段資訊。

有關使用此端點的更多詳細資訊，請參見 [匯出作業端點指南](../api/export-jobs.md#create)

### 監視導出進度

作為匯出作業程式，您可以向 `/export/jobs` 端點和包含 `id` 的URL。 一旦 `status` 欄位返回值「SUCCEEDED」。

有關使用此端點的更多詳細資訊，請參見 [匯出作業端點指南](../api/export-jobs.md#get)

## 後續步驟

匯出成功後，您的資料即可在 [!DNL Data Lake] in [!DNL Experience Platform]. 然後，您就可以使用 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 若要存取資料，請使用 `batchId` 與匯出相關聯。 根據區段的大小，資料可能是區塊，而批次可能包含數個檔案。

如需如何使用的逐步指示 [!DNL Data Access] 若要存取和下載批次檔案，請遵循 [資料存取教學課程](../../data-access/tutorials/dataset-data.md).

您也可以使用 [!DNL Adobe Experience Platform Query Service]. 使用UI或RESTful API, [!DNL Query Service] 可讓您對 [!DNL Data Lake].

如需如何查詢受眾資料的詳細資訊，請參閱 [[!DNL Query Service]](../../query-service/home.md).
