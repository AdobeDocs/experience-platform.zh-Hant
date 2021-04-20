---
keywords: Experience Platform; home；熱門主題；分段評價；分段服務；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；
solution: Experience Platform
title: 評估並存取區段結果
topic: tutorial
type: Tutorial
description: 請依照本教學課程學習如何使用Adobe Experience Platform區段服務API來評估區段並存取區段結果。
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
translation-type: tm+mt
source-git-commit: 87729e4996b0b2ac26e1a0abaa80af717825f9e6
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# 評估並存取區段結果

本檔案提供使用[[!DNL Segmentation API]](../api/getting-started.md)評估區段及存取區段結果的教學課程。

## 快速入門

本教學課程需要對建立觀眾區隔時涉及的各種[!DNL Adobe Experience Platform]服務有深入的瞭解。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料即時提供統一的客戶個人檔案。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):可讓您從資料建立受眾 [!DNL Real-time Customer Profile] 細分。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):平台組織客戶體驗資料的標準化架構。
- [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

### 必要的標題

本教學課程還要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫[!DNL Platform] API。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

- 授權：載體`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的請求需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

所有POST、PUT和PATCH請求都需要額外的標題：

- 內容類型：application/json

## 評估區段

開發、測試和儲存區段定義後，您就可以透過排程評估或隨選評估來評估區段。

[排程評估](#scheduled-evaluation) （也稱為「排程區段」）可讓您建立在特定時間執行匯出工作的循環排程，而 [隨選](#on-demand-evaluation) 評估則包括建立區段工作以立即建立觀眾。以下列出各步驟。

如果您尚未完成[使用區段API](./create-a-segment.md)教學課程建立區段，或使用[區段產生器](../ui/overview.md)建立區段定義，請先執行此動作，再繼續本教學課程。

## 計畫評估{#scheduled-evaluation}

透過排程評估，您的IMS組織可以建立循環排程，以自動執行匯出工作。

>[!NOTE]
>
>對於[!DNL XDM Individual Profile]最多可啟用五(5)個合併策略的沙盒，可啟用計畫評估。 如果您的組織在單一沙盒環境中有超過5個[!DNL XDM Individual Profile]的合併原則，您將無法使用排程的評估。

### 建立排程

通過向`/config/schedules`端點發出POST請求，可以建立一個調度並包括應觸發該調度的特定時間。

有關使用此端點的詳細資訊，請參閱[計畫端點指南](../api/schedules.md#create)

### 啟用排程

預設情況下，建立計畫時將處於非活動狀態，除非在建立(POST)請求主體中將`state`屬性設定為`active`。 通過向`/config/schedules`端點發出PATCH請求並在路徑中包括調度的ID，可以啟用調度（將`state`設定為`active`）。

有關使用此端點的詳細資訊，請參閱[計畫端點指南](../api/schedules.md#update-state)

### 更新計畫時間

通過向`/config/schedules`端點發出PATCH請求並在路徑中包括調度的ID，可以更新調度時間。

有關使用此端點的詳細資訊，請參閱[計畫端點指南](../api/schedules.md#update-schedule)

## 隨選評估

隨選評估可讓您建立區段工作，以便在需要時產生對象區段。 與排程評估不同，這只會在要求時發生，且不會重複發生。

### 建立區段工作

區段工作是建立新讀者區段的非同步程式。 它參考區段定義，以及控制[!DNL Real-time Customer Profile]如何合併描述檔片段中重疊屬性的任何合併原則。 當區段工作成功完成時，您可以收集區段的各種資訊，例如處理期間可能發生的任何錯誤，以及您的受眾的最終規模。

您可以通過向[!DNL Real-time Customer Profile] API中的`/segment/jobs`端點發出POST請求來建立新的段作業。

有關使用此端點的詳細資訊，請參閱[segment作業端點指南](../api/segment-jobs.md#create)


### 查找段作業狀態

您可以針對特定區段工作使用`id`來執行查閱請求(GET)，以檢視工作的目前狀態。

有關使用此端點的詳細資訊，請參閱[segment作業端點指南](../api/segment-jobs.md#get)

## 解譯區段結果

當區段作業成功執行時，會針對區段內每個描述檔更新`segmentMembership`對應。 `segmentMembership` 此外，還會儲存任何已預先評估的受眾細分，這些細分會 [!DNL Platform]納入其中，以便與其他解決方案整合 [!DNL Adobe Audience Manager]。

以下範例顯示每個個別描述檔記錄的`segmentMembership`屬性外觀：

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
| `lastQualificationTime` | 斷言區段成員資格及設定檔輸入或退出區段時的時間戳記。 |
| `status` | 目前請求中區段參與率的狀態。 必須等於下列其中一個已知值： <ul><li>`existing`:實體繼續在分部中。</li><li>`realized`:實體正在輸入區段。</li><li>`exited`:實體正在退出區段。</li></ul> |

## 存取區段結果

可以通過以下兩種方式之一訪問段作業的結果：您可以存取個別設定檔，或將整個對象匯出至資料集。

以下幾節將更詳細地概述這些選項。

## 查找配置檔案

如果您知道要存取的特定描述檔，則可使用[!DNL Real-time Customer Profile] API進行存取。 使用Profile API](../../profile/api/entities.md)教學課程存取即時客戶個人檔案資料中提供存取個別個人檔案的完整步驟。[

## 匯出區段{#export}

分段工作成功完成後（`status`屬性的值為&quot;SUCCEEDED&quot;），您可以將對象匯出至資料集，供您存取並執行操作。

匯出您的觀眾需要下列步驟：

- [建立目標資料集](#create-a-target-dataset) -建立資料集以容納對象成員。
- [在資料集中產生觀眾設定檔](#generate-profiles-for-audience-members) -根據區段工作的結果，以XDM個別設定檔填入資料集。
- [監視導出進度](#monitor-export-progress) -檢查導出進程的當前進度。
- [讀取觀眾資料](#next-steps) -擷取產生的XDM個人設定檔，代表觀眾的成員。

### 建立目標資料集

匯出對象時，必須先建立目標資料集。 請務必正確設定資料集，以確保匯出成功。

主要考量事項之一是資料集所依據的架構（以下API範例請求中的`schemaRef.id`）。 若要匯出區段，資料集必須以[!DNL XDM Individual Profile Union Schema](`https://ns.adobe.com/xdm/context/profile__union`)為基礎。 聯合模式是系統生成的只讀模式，它聚合共用相同類的模式的欄位（在本例中為XDM Individual Profile類）。 有關聯合視圖方案的詳細資訊，請參閱方案註冊表開發人員指南](../../xdm/api/getting-started.md)的[即時客戶配置檔案部分。

建立必要資料集有兩種方式：

- **使用API：本** 教學課程中後續的步驟概述如何建立使用API參考 [!DNL XDM Individual Profile Union Schema] 的資 [!DNL Catalog] 料集。
- **使用UI：若要** 使用 [!DNL Adobe Experience Platform] 者介面來建立參照聯合架構的資料集，請依照 [UI教學課程中的步驟進行，然後返回本教學課程，以繼續產生觀眾](../ui/overview.md) 設定檔的步驟 [](#generate-xdm-profiles-for-audience-members)。

如果您已擁有相容的資料集並知道其ID，則可直接執行[產生觀眾設定檔的步驟](#generate-xdm-profiles-for-audience-members)。

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
    },
    "fileDescription": {
        "persisted": true
    }
}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 資料集的描述性名稱。 |
| `schemaRef.id` | 資料集將與之關聯的聯合檢視（結構）ID。 |
| `fileDescription.persisted` | 布爾值，設為`true`時，可讓資料集持續存留在聯合檢視中。 |

**回應**

成功的回應會傳回包含新建立資料集之唯讀、系統產生之唯一ID的陣列。 若要成功匯出觀眾成員，需要正確設定的資料集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 為觀眾成員產生個人檔案{#generate-profiles}

在您擁有持續統一的資料集後，您可以建立匯出工作，將觀眾成員持續存留至資料集，方法是向[!DNL Real-time Customer Profile] API的`/export/jobs`端點提出POST要求，並提供您要匯出之區段的資料集ID和區段資訊。

有關使用此端點的詳細資訊，請參閱[導出作業端點指南](../api/export-jobs.md#create)

### 監視導出進度

作為導出作業進程，可以通過向`/export/jobs`端點發出GET請求並在路徑中包括導出作業的`id`來監視其狀態。 在`status`欄位返回值&quot;SUCCEEDED&quot;後，導出作業即完成。

有關使用此端點的詳細資訊，請參閱[導出作業端點指南](../api/export-jobs.md#get)

## 後續步驟

匯出成功後，您的資料就可在[!DNL Experience Platform]的[!DNL Data Lake]中使用。 然後，您可以使用[[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)，使用與導出關聯的`batchId`訪問資料。 視區段大小而定，資料可能以區塊為單位，而批次可能由數個檔案組成。

有關如何使用[!DNL Data Access] API來存取和下載批處理檔案的逐步說明，請遵循[資料存取教程](../../data-access/tutorials/dataset-data.md)。

您也可以使用[!DNL Adobe Experience Platform Query Service]存取成功匯出的區段資料。 使用UI或REST風格的API, [!DNL Query Service]可讓您編寫、驗證和執行[!DNL Data Lake]中資料的查詢。

有關如何查詢受眾資料的更多資訊，請參閱[[!DNL Query Service]](../../query-service/home.md)上的檔案。
