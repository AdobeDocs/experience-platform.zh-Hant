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

本檔案提供的教學課程可協助您評估區段定義，並使用存取這些結果。 [[!DNL Segmentation API]](../api/getting-started.md).

## 快速入門

本教學課程需要您實際瞭解各種 [!DNL Adobe Experience Platform] 與建立對象相關的服務。 在開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶設定檔。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：可讓您從建立對象 [!DNL Real-Time Customer Profile] 資料。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：Platform組織客戶體驗資料的標準化架構。 為善用分段，請確保您的資料已根據 [資料模型化的最佳實務](../../xdm/schema/best-practices.md).
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，協助開發及改進數位體驗應用程式。

### 必要的標頭

本教學課程也要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] API。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- 授權：持有人 `{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 會隔離至特定的虛擬沙箱。 要求給 [!DNL Platform] API需要標頭，用以指定將進行作業的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有POST、PUT和PATCH請求都需要額外的標頭：

- Content-Type： application/json

## 評估區段定義 {#evaluate-a-segment}

開發、測試及儲存區段定義後，您就可以透過排定的評估或隨需評估，來評估區段定義。

[已排程的評估](#scheduled-evaluation) （也稱為「排程分段」）可讓您建立在特定時間執行匯出作業的週期性排程，而 [隨選評估](#on-demand-evaluation) 包括建立區段工作以立即建立對象。 各步驟概述如下。

如果您尚未完成 [使用分段API建立區段定義](./create-a-segment.md) 教學課程或建立區段定義，使用 [區段產生器](../ui/segment-builder.md)，請先觀看再繼續本教學課程。

## 已排程的評估 {#scheduled-evaluation}

透過已排程的評估，您的組織可以建立週期性排程，以自動執行匯出作業。

>[!NOTE]
>
>對於最多有五(5)個合併原則的沙箱，可啟用排定的評估。 [!DNL XDM Individual Profile]. 如果貴組織擁有五個以上的合併原則 [!DNL XDM Individual Profile] 在單一沙箱環境中，您將無法使用排程的評估。

### 建立排程

POST藉由向 `/config/schedules` 端點，您可以建立排程並包含應觸發排程的特定時間。

有關使用此端點的更多詳細資訊，請參閱 [排程端點指南](../api/schedules.md#create)

### 啟用排程

依預設，排程在建立時為非作用中，除非 `state` 屬性已設為 `active` 建立(POST)要求內文中。 您可以啟用排程(設定 `state` 至 `active`PATCH )，方式是向 `/config/schedules` 端點並在路徑中包含排程的ID。

有關使用此端點的更多詳細資訊，請參閱 [排程端點指南](../api/schedules.md#update-state)

### 更新排程時間

您可以透過向以下發出PATCH請求來更新排程計時： `/config/schedules` 端點並在路徑中包含排程的ID。

有關使用此端點的更多詳細資訊，請參閱 [排程端點指南](../api/schedules.md#update-schedule)

## 隨選評估

隨選評估可讓您建立區段工作，以便在您需要時產生對象。 與排程評估不同，這僅在請求時發生，並且不會重複發生。

### 建立區段工作

區段作業為非同步程式，可依需求建立對象區段。 它會參考區段定義，以及控制如何執行的任何合併原則 [!DNL Real-Time Customer Profile] 會合併您設定檔片段中的重疊屬性。 成功完成區段作業後，您可以收集有關區段定義的各種資訊，例如處理期間可能發生的任何錯誤以及您對象的最終大小。 每次想要重新整理區段定義目前符合資格的對象時，都必須執行區段工作。

您可以透過向以下網站發出POST請求，以建立新的區段作業： `/segment/jobs` 中的端點 [!DNL Real-Time Customer Profile] API。

有關使用此端點的更多詳細資訊，請參閱 [區段作業端點指南](../api/segment-jobs.md#create)

### 查詢區段工作狀態

您可以使用 `id` 針對特定區段工作執行查詢請求(GET)，以檢視工作的目前狀態。

有關使用此端點的更多詳細資訊，請參閱 [區段作業端點指南](../api/segment-jobs.md#get)

## 解讀區段作業結果

成功執行區段作業時， `segmentMembership` 會針對區段定義中包含的每個設定檔更新對應。 `segmentMembership` 也會儲存任何擷取到的預先評估對象 [!DNL Platform]，允許與其他解決方案整合，例如 [!DNL Adobe Audience Manager].

下列範例說明了 `segmentMembership` 屬性看起來像每個個別的設定檔記錄：

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
| `status` | 作為目前請求一部分的區段定義的參與狀態。 必須等於下列其中一個已知值： <ul><li>`realized`：實體符合區段定義的資格。</li><li>`exited`：實體正在退出區段定義。</li></ul> |

>[!NOTE]
>
>任何位於中的區段會籍 `exited` 超過30天的狀態，根據 `lastQualificationTime`，將會刪除。

## 存取區段工作結果

區段工作的結果可透過兩種方式之一存取：您可以存取個別設定檔或匯出整個對象到資料集。

以下各節會更詳細地概述這些選項。

## 查詢設定檔

如果您知道想要存取的特定設定檔，可以使用 [!DNL Real-Time Customer Profile] API。 存取個別設定檔的完整步驟，請參見 [使用設定檔API存取即時客戶設定檔資料](../../profile/api/entities.md) 教學課程。

## 匯出區段 {#export}

成功完成分段工作後( `status` 屬性為「SUCCEEDED」)，您可以將對象匯出至資料集，在其中存取對象並據以採取行動。

匯出對象時，需要執行下列步驟：

- [建立目標資料集](#create-a-target-dataset)  — 建立資料集以保留對象成員。
- [在資料集中產生對象設定檔](#generate-profiles)  — 根據區段作業的結果，以XDM個別設定檔填入資料集。
- [監視匯出進度](#monitor-export-progress)  — 檢查匯出程式的目前進度。
- [讀取對象資料](#next-steps)  — 擷取代表您對象成員的結果XDM個別設定檔。

### 建立目標資料集 {#create-dataset}

匯出對象時，必須先建立目標資料集。 請務必正確設定資料集，以確保匯出成功。

重要考量事項之一是資料集所根據的結構描述(`schemaRef.id` （位於以下的API範例請求中）。 為了匯出區段定義，資料集必須以 [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`)。 聯合結構描述是系統產生的唯讀結構描述，其彙總共用相同類別的結構描述（在此例中為XDM個別設定檔類別）的欄位。 如需聯合檢視結構描述的詳細資訊，請參閱 [Schema Registry開發人員指南的「即時客戶個人檔案」區段](../../xdm/api/getting-started.md).

建立必要資料集有兩個方法：

- **使用API：** 本教學課程後續步驟將概述如何建立參照 [!DNL XDM Individual Profile Union Schema] 使用 [!DNL Catalog] API。
- **使用UI：** 若要使用 [!DNL Adobe Experience Platform] 若要建立參考聯合結構的資料集，請依照以下步驟操作： [UI教學課程](../ui/overview.md) 然後返回本教學課程，繼續的步驟 [產生受眾設定檔](#generate-profiles).

如果您已經有相容的資料集並知道其ID，您可以直接進行步驟 [產生受眾設定檔](#generate-profiles).

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

擁有聯合儲存資料集後，您可以透過向以下專案發出POST請求，建立匯出工作以將對象成員儲存至資料集： `/export/jobs` 中的端點 [!DNL Real-Time Customer Profile] API並為您要匯出的區段定義提供資料集ID和區段定義資訊。

有關使用此端點的更多詳細資訊，請參閱 [匯出作業端點指南](../api/export-jobs.md#create)

### 監視匯出進度

匯出作業進行時，您可以透過向以下網站發出GET請求來監視其狀態： `/export/jobs` 端點，並包含 `id` 路徑中匯出作業的ID。 匯出作業於下列作業完成後完成： `status` 欄位會傳回「SUCCEEDED」值。

有關使用此端點的更多詳細資訊，請參閱 [匯出作業端點指南](../api/export-jobs.md#get)

## 後續步驟

匯出成功完成後，您的資料可在 [!DNL Data Lake] 在 [!DNL Experience Platform]. 然後，您可以使用 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 以使用存取資料 `batchId` 與匯出相關聯。 視區段定義的大小而定，資料可能會以區塊為單位，批次可能包含數個檔案。

如需如何使用 [!DNL Data Access] 若要存取和下載批次檔案的API，請遵循 [資料存取教學課程](../../data-access/tutorials/dataset-data.md).

您也可以使用存取已成功匯出的區段定義資料 [!DNL Adobe Experience Platform Query Service]. 使用UI或RESTful API， [!DNL Query Service] 可讓您針對以下範圍內的資料寫入、驗證及執行查詢： [!DNL Data Lake].

如需如何查詢受眾資料的詳細資訊，請參閱以下檔案： [[!DNL Query Service]](../../query-service/home.md).
