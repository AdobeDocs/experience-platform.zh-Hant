---
keywords: Experience Platform；首頁；熱門主題；區段評估；區段服務；分段；評估區段；存取區段結果；評估和存取區段；
solution: Experience Platform
title: 評估和存取區段結果
topic-legacy: tutorial
type: Tutorial
description: 請依照本教學課程，了解如何使用Adobe Experience Platform區段服務API評估區段並存取區段結果。
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 453e120fa20232533289ee5ff34821ce8c0c310b
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 0%

---

# 評估和存取區段結果

本檔案提供使用[[!DNL Segmentation API]](../api/getting-started.md)評估區段及存取區段結果的教學課程。

## 快速入門

本教學課程需要妥善了解建立受眾區段時涉及的各種[!DNL Adobe Experience Platform]服務。 開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的客戶設定檔。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):可讓您從資料建立受眾 [!DNL Real-time Customer Profile] 區段。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):Platform用來組織客戶體驗資料的標準化架構。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

### 必要標題

本教學課程也需要您完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫[!DNL Platform] API。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權：承載`{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都與特定虛擬沙箱隔離。 對[!DNL Platform] API的請求需要標題，以指定要在中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有POST、PUT和PATCH請求都需要額外的標題：

- 內容類型：application/json

## 評估區段

開發、測試並儲存區段定義後，您就可以透過排程評估或隨需評估來評估區段。

[排程評估](#scheduled-evaluation) （也稱為「排程區段」）可讓您建立在特定時間執行匯出作業的循環排程，而 [隨需](#on-demand-evaluation) 評估則涉及建立區段工作以立即建立對象。各步驟的步驟如下所述。

如果您尚未完成[使用區段API](./create-a-segment.md)教學課程建立區段，或使用[區段產生器](../ui/overview.md)建立區段定義，請先完成此操作，再繼續進行本教學課程。

## 計畫評估 {#scheduled-evaluation}

透過排程的評估，您的IMS組織可以建立循環排程以自動執行匯出作業。

>[!NOTE]
>
>對於[!DNL XDM Individual Profile]，最多可為五(5)個合併原則的沙箱啟用排程評估。 如果貴組織在單一沙箱環境中有超過五個[!DNL XDM Individual Profile]的合併原則，則無法使用排程的評估。

### 建立排程

通過向`/config/schedules`端點發出POST請求，可以建立調度並包括應觸發該調度的特定時間。

有關使用此端點的更多詳細資訊，請參見[schedules endpoint guide](../api/schedules.md#create)

### 啟用排程

預設情況下，建立時，排程會非作用中，除非在建立(POST)請求正文中將`state`屬性設定為`active`。 您可以向`/config/schedules`端點發出PATCH請求，並在路徑中包含調度的ID，以啟用調度（將`state`設定為`active`）。

有關使用此端點的更多詳細資訊，請參見[schedules endpoint guide](../api/schedules.md#update-state)

### 更新排程時間

向`/config/schedules`端點發出PATCH請求並在路徑中包含排程的ID，可以更新排程計時。

有關使用此端點的更多詳細資訊，請參見[schedules endpoint guide](../api/schedules.md#update-schedule)

## 隨選評估

隨需評估可讓您建立區段工作，以便隨時產生受眾區段。 與排程評估不同，這只會在要求時發生，且不會重複執行。

### 建立區段作業

區段工作是建立新受眾區段的非同步程式。 它會參考區段定義，以及任何控制[!DNL Real-time Customer Profile]如何合併設定檔片段之重疊屬性的合併原則。 區段工作成功完成後，您可以收集區段的各種資訊，例如處理期間可能發生的任何錯誤，以及對象的最終大小。

您可以透過向[!DNL Real-time Customer Profile] API中的`/segment/jobs`端點提出POST要求，以建立新的區段作業。

有關使用此端點的更多詳細資訊，請參見[segment作業端點指南](../api/segment-jobs.md#create)


### 查找段作業狀態

您可以對特定區段作業使用`id`來執行查閱請求(GET)，以檢視作業的目前狀態。

有關使用此端點的更多詳細資訊，請參見[segment作業端點指南](../api/segment-jobs.md#get)

## 解譯區段結果

成功執行區段作業時，會針對包含在區段中的每個設定檔更新`segmentMembership`對應。 `segmentMembership` 也會儲存擷取至的任何預先評估對象區段，以 [!DNL Platform]便與其他解決方案（例如） [!DNL Adobe Audience Manager]整合。

下列範例顯示每個個別設定檔記錄的`segmentMembership`屬性看起來是什麼樣子：

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
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
| `status` | 目前請求中區段參與率的狀態。 必須等於下列其中一個已知值： <ul><li>`existing`:實體繼續在分部中。</li><li>`realized`:實體正在輸入區段。</li><li>`exited`:實體正在退出區段。</li></ul> |

## 存取區段結果

您可透過下列兩種方式之一存取區段作業的結果：您可以存取個別設定檔，或將整個對象匯出至資料集。

以下各節將更詳細地介紹這些選項。

## 查詢設定檔

如果您知道要存取的特定設定檔，可使用[!DNL Real-time Customer Profile] API進行存取。 使用設定檔API](../../profile/api/entities.md)教學課程的[存取即時客戶設定檔資料，提供存取個別設定檔的完整步驟。

## 匯出區段 {#export}

分段工作成功完成後（`status`屬性的值為「SUCCEEDED」），您可以將對象匯出至資料集，以便存取資料集並加以處理。

匯出對象需要下列步驟：

- [建立目標資料集](#create-a-target-dataset)  — 建立資料集以保留對象成員。
- [在資料集中產生受眾設定檔](#generate-profiles-for-audience-members)  — 根據區段工作的結果，為資料集填入XDM個別設定檔。
- [監控匯出進度](#monitor-export-progress)  — 檢查匯出程式的目前進度。
- [讀取對象資料](#next-steps)  — 擷取代表對象成員的產生XDM個別設定檔。

### 建立目標資料集

匯出對象時，必須先建立目標資料集。 請務必正確設定資料集，以確保匯出成功。

其中一項主要考量事項為資料集所依據的結構（以下API範例請求中為`schemaRef.id`）。 若要匯出區段，資料集必須以[!DNL XDM Individual Profile Union Schema](`https://ns.adobe.com/xdm/context/profile__union`)為基礎。 聯合結構是系統產生的唯讀結構，會匯總共用相同類別之結構的欄位（在此例中是XDM個別設定檔類別）。 有關聯合查看架構的詳細資訊，請參閱Schema Registry開發人員指南](../../xdm/api/getting-started.md)的[ Real-time Customer Profile（即時客戶配置檔案）部分。

建立必要資料集的方式有兩種：

- **使用API:** 本教學課程後續步驟概述如何建立使用API參考 [!DNL XDM Individual Profile Union Schema] 的資料 [!DNL Catalog] 集。
- **使用UI:** 若要使用使 [!DNL Adobe Experience Platform] 用者介面建立參考聯合結構的資料集，請依照UI教學課程中的步驟操作，然後回到本教學課程，繼續執行產生受眾設定檔 [的步驟](../ui/overview.md)  [](#generate-xdm-profiles-for-audience-members)。

如果您已有相容的資料集且知道其ID，則可直接進入[產生對象設定檔](#generate-xdm-profiles-for-audience-members)的步驟。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

在您擁有持續存在的資料集後，您可以建立匯出工作，在[!DNL Real-time Customer Profile] API中向`/export/jobs`端點提出POST要求，並針對您要匯出的區段提供資料集ID和區段資訊，以保留對象成員至資料集。

有關使用此端點的更多詳細資訊，請參見[export jobs endpoint guide](../api/export-jobs.md#create)

### 監視導出進度

作為導出作業進程，可以通過向`/export/jobs`端點發出GET請求並在路徑中包括導出作業的`id`來監視其狀態。 `status`欄位返回值「SUCCEEDED」後，導出作業即告完成。

有關使用此端點的更多詳細資訊，請參見[export jobs endpoint guide](../api/export-jobs.md#get)

## 後續步驟

匯出成功後，您的資料即可在[!DNL Experience Platform]的[!DNL Data Lake]內使用。 然後，您可以使用[[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)，使用與匯出相關聯的`batchId`存取資料。 根據區段的大小，資料可能是區塊，而批次可能包含數個檔案。

有關如何使用[!DNL Data Access] API訪問和下載批處理檔案的逐步說明，請遵循[資料訪問教程](../../data-access/tutorials/dataset-data.md)。

您也可以使用[!DNL Adobe Experience Platform Query Service]存取成功匯出的區段資料。 使用UI或RESTful API [!DNL Query Service]可讓您對[!DNL Data Lake]內的資料寫入、驗證及執行查詢。

如需如何查詢受眾資料的詳細資訊，請檢閱[[!DNL Query Service]](../../query-service/home.md)上的檔案。
