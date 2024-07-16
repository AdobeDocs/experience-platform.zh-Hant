---
solution: Experience Platform
title: 評估及存取區段結果
type: Tutorial
description: 按照本教學課程瞭解如何使用Adobe Experience Platform分段服務API評估區段定義及存取分段結果。
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 1%

---

# 評估並存取區段定義結果

本檔案提供教學課程，說明如何使用[[!DNL Segmentation API]](../api/getting-started.md)來評估區段定義及存取這些結果。

## 快速入門

此教學課程需要您實際瞭解建立對象所涉及的各種[!DNL Adobe Experience Platform]服務。 在開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶設定檔。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：可讓您從[!DNL Real-Time Customer Profile]資料建立對象。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： Platform用來組織客戶體驗資料的標準化架構。 若要充分利用「細分」，請確定您的資料已根據[資料模型最佳實務](../../xdm/schema/best-practices.md)被擷取為設定檔和事件。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

### 必要的標頭

此教學課程也要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫[!DNL Platform] API。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- 授權：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的請求需要一個標頭，該標頭會指定將在其中執行操作的沙箱的名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有POST、PUT和PATCH請求都需要額外的標頭：

- Content-Type： application/json

## 評估區段定義 {#evaluate-a-segment}

開發、測試及儲存區段定義後，您就可以透過排定的評估或隨需評估，來評估區段定義。

[排程評估](#scheduled-evaluation) （也稱為「排程分段」）可讓您建立在特定時間執行匯出工作的週期性排程，而[隨選評估](#on-demand-evaluation)涉及建立區段工作以立即建立對象。 各步驟概述如下。

如果您尚未使用Segmentation API](./create-a-segment.md)教學課程完成[建立區段定義，或使用[區段產生器](../ui/segment-builder.md)建立區段定義，請先完成該步驟，再繼續本教學課程。

## 已排程的評估 {#scheduled-evaluation}

透過已排程的評估，您的組織可以建立週期性排程，以自動執行匯出作業。

>[!NOTE]
>
>針對[!DNL XDM Individual Profile]最多有五(5)個合併原則的沙箱，可啟用排定的評估。 如果您的組織在單一沙箱環境中有[!DNL XDM Individual Profile]的五個以上的合併原則，您將無法使用排程的評估。

### 建立排程

透過向`/config/schedules`端點發出POST要求，您可以建立排程並包含應觸發排程的特定時間。

您可以在[排程端點指南](../api/schedules.md#create)中找到有關使用此端點的詳細資訊

### 啟用排程

根據預設，除非建立(POST)要求內文中的`state`屬性設定為`active`，否則排程在建立時為非作用中。 您可以透過向`/config/schedules`端點發出PATCH請求並在路徑中包含排程的ID來啟用排程（將`state`設定為`active`）。

您可以在[排程端點指南](../api/schedules.md#update-state)中找到有關使用此端點的詳細資訊

### 更新排程時間

可以透過向`/config/schedules`端點發出PATCH請求並在路徑中包含排程的ID來更新排程計時。

您可以在[排程端點指南](../api/schedules.md#update-schedule)中找到有關使用此端點的詳細資訊

## 隨選評估

隨選評估可讓您建立區段工作，以便在您需要時產生對象。 與排程評估不同，這僅在請求時發生，並且不會重複發生。

### 建立區段工作

區段作業為非同步程式，可依需求建立對象區段。 它參考區段定義，以及控制[!DNL Real-Time Customer Profile]如何在您的設定檔片段中合併重疊屬性的任何合併原則。 成功完成區段作業後，您可以收集有關區段定義的各種資訊，例如處理期間可能發生的任何錯誤以及您對象的最終大小。 每次想要重新整理區段定義目前符合資格的對象時，都必須執行區段工作。

您可以對[!DNL Real-Time Customer Profile] API中的`/segment/jobs`端點發出POST要求，以建立新的區段作業。

您可以在[區段作業端點指南](../api/segment-jobs.md#create)中找到有關使用此端點的詳細資訊

### 查詢區段工作狀態

您可以針對特定區段工作使用`id`來執行查詢請求(GET)，以檢視工作的目前狀態。

您可以在[區段作業端點指南](../api/segment-jobs.md#get)中找到有關使用此端點的詳細資訊

## 解讀區段作業結果

成功執行區段作業時，會針對區段定義中包含的每個設定檔更新`segmentMembership`對應。 `segmentMembership`也會儲存擷取至[!DNL Platform]的任何預先評估對象，以允許與其他解決方案（例如[!DNL Adobe Audience Manager]）整合。

下列範例顯示每個個別設定檔記錄的`segmentMembership`屬性外觀：

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
| `lastQualificationTime` | 進行區段會籍判斷提示以及設定檔進入或退出區段定義時的時間戳記。 |
| `status` | 作為目前請求一部分的區段定義的參與狀態。 必須等於下列其中一個已知值： <ul><li>`realized`：實體符合區段定義的資格。</li><li>`exited`：實體正在結束區段定義。</li></ul> |

>[!NOTE]
>
>根據`lastQualificationTime`，任何處於`exited`狀態超過30天的區段會籍都將遭到刪除。

## 存取區段工作結果

區段工作的結果可透過兩種方式之一存取：您可以存取個別設定檔或匯出整個對象到資料集。

以下各節會更詳細地概述這些選項。

## 查詢設定檔

如果您知道要存取的特定設定檔，可以使用[!DNL Real-Time Customer Profile] API來存取。 使用設定檔API](../../profile/api/entities.md)教學課程的[存取即時客戶設定檔資料中，提供了存取個別設定檔的完整步驟。

## 匯出區段 {#export}

成功完成分段工作後（`status`屬性的值為「SUCCEEDED」），您就可以將對象匯出至資料集，以便對其進行存取和操作。

匯出對象時，需要執行下列步驟：

- [建立目標資料集](#create-a-target-dataset) — 建立資料集以保留對象成員。
- [在資料集中產生對象設定檔](#generate-profiles) — 根據區段作業的結果，以XDM個別設定檔填入資料集。
- [監視匯出進度](#monitor-export-progress) — 檢查匯出流程的目前進度。
- [讀取對象資料](#next-steps) — 擷取代表對象成員的結果XDM個別設定檔。

### 建立目標資料集 {#create-dataset}

匯出對象時，必須先建立目標資料集。 請務必正確設定資料集，以確保匯出成功。

重要考量事項之一是資料集所依據的結構描述（在以下API範例要求中為`schemaRef.id`）。 為了匯出區段定義，資料集必須以[!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`)為基礎。 聯合結構描述是系統產生的唯讀結構描述，其彙總共用相同類別的結構描述（在此例中為XDM個別設定檔類別）的欄位。 如需聯合檢視結構描述的詳細資訊，請參閱結構描述登入開發人員指南](../../xdm/api/getting-started.md)的[即時客戶設定檔區段。

建立必要資料集有兩個方法：

- **使用API：**&#x200B;本教學課程中遵循的步驟概述如何使用[!DNL Catalog] API建立參照[!DNL XDM Individual Profile Union Schema]的資料集。
- **使用UI：**&#x200B;若要使用[!DNL Adobe Experience Platform]使用者介面建立參考聯合結構描述的資料集，請依照[UI教學課程](../ui/overview.md)中的步驟操作，然後返回此教學課程，繼續進行[產生對象設定檔](#generate-profiles)的步驟。

如果您已有相容的資料集且知道其識別碼，您可以直接進行步驟，以[產生對象設定檔](#generate-profiles)。

**API格式**

```http
POST /dataSets
```

**要求**

以下請求會建立新資料集，在承載中提供設定引數。

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
| `schemaRef.id` | 與資料集建立關聯的聯合檢視（結構描述）的ID。 |

**回應**

成功的回應會傳回陣列，其中包含新建立資料集的唯讀、系統產生的唯一ID。 需要正確設定的資料集ID才能成功匯出對象成員。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 產生對象成員的設定檔 {#generate-profiles}

擁有聯合持續資料集後，您可以建立匯出作業，以持續將對象成員存放在資料集，方法是向[!DNL Real-Time Customer Profile] API中的`/export/jobs`端點發出POST請求，並提供您要匯出的區段定義的資料集ID和區段定義資訊。

您可以在[匯出作業端點指南](../api/export-jobs.md#create)中找到有關使用此端點的詳細資訊

### 監視匯出進度

匯出作業進行時，您可以透過向`/export/jobs`端點發出GET請求並在路徑中包含匯出作業的`id`來監視其狀態。 當`status`欄位傳回「SUCCEEDED」值時，匯出作業即已完成。

您可以在[匯出作業端點指南](../api/export-jobs.md#get)中找到有關使用此端點的詳細資訊

## 後續步驟

匯出成功完成後，您的資料便可在[!DNL Experience Platform]的[!DNL Data Lake]內使用。 然後，您可以使用[[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/)，使用與匯出相關聯的`batchId`來存取資料。 視區段定義的大小而定，資料可能會以區塊為單位，批次可能包含數個檔案。

如需如何使用[!DNL Data Access] API存取及下載批次檔案的逐步指示，請遵循[資料存取教學課程](../../data-access/tutorials/dataset-data.md)。

您也可以使用[!DNL Adobe Experience Platform Query Service]存取已成功匯出的區段定義資料。 使用UI或RESTful API，[!DNL Query Service]可讓您對[!DNL Data Lake]內的資料進行寫入、驗證及執行查詢。

如需如何查詢對象資料的詳細資訊，請檢閱[[!DNL Query Service]](../../query-service/home.md)上的檔案。
