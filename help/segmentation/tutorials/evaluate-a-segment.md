---
keywords: Experience Platform;home;popular topics;segment evaluation;Segmentation Service;segmentation;Segmentation;evaluate a segment;access segment results;evaluate and access segment;
solution: Experience Platform
title: 評估區段
topic: tutorial
description: 本檔案提供使用區段API評估區段及存取區段結果的教學課程。
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 0%

---


# 評估並存取區段結果

本檔案提供使用 [[!DNL區段API]評估區段及存取區段結果的教學課程](../api/getting-started.md)。

## 快速入門

本教學課程需要對建立觀眾區隔時 [!DNL Adobe Experience Platform] 涉及的各種服務有充份的瞭解。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [[!DNL即時客戶基本資料]](../../profile/home.md):根據來自多個來源的匯整資料，即時提供統一的客戶個人檔案。
- [[!DNL Adobe Experience Platform分段服務]](../home.md):可讓您從資料建立受眾 [!DNL Real-time Customer Profile] 區段。
- [[!DNL體驗資料模型(XDM)]](../../xdm/home.md):平台組織客戶體驗資料的標準化架構。
- [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

### 必要的標題

本教學課程也要求您完成驗 [證教學課程](../../tutorials/authentication.md) ，才能成功呼叫 [!DNL Platform] API。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權：生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的 [!DNL Platform] 請求需要一個標題，該標題指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

所有POST、PUT和PATCH請求都需要附加標題：

- 內容類型：application/json

## 評估區段

開發、測試和儲存區段定義後，您就可以透過排程評估或隨選評估來評估區段。

[排程評估](#scheduled-evaluation)[](#on-demand-evaluation) （也稱為「排程的區段」）可讓您建立在特定時間執行匯出工作的循環排程，而隨選評估則涉及建立區段工作以立即建立觀眾。 以下列出各步驟。

如果您尚未使用「區段API [」教學課程建立區段](./create-a-segment.md)[](../ui/overview.md)，或使用「區段產生器」建立區段定義，請先執行此步驟，然後再繼續本教學課程。

## 排程的評估 {#scheduled-evaluation}

透過排程評估，您的IMS組織可以建立循環排程，以自動執行匯出工作。

>[!NOTE]
>
>對於最多5(5)個合併策略的沙盒，可啟用計畫評估 [!DNL XDM Individual Profile]。 如果貴組織在單一沙盒環境中有5 [!DNL XDM Individual Profile] 種以上的合併原則，您將無法使用排程的評估。

### 建立排程

通過向端點發出POST請 `/config/schedules` 求，您可以建立調度並包括應觸發該調度的特定時間。

有關使用此端點的詳細資訊，請參閱計畫端 [點指南](../api/schedules.md#create)

### 啟用排程

預設情況下，建立計畫時，除非將屬 `state` 性設定為建立(POST) `active` 請求主體中，否則該計畫處於非活動狀態。 通過向端點發出PATCH請求並在路徑中包 `state``active``/config/schedules` 括調度的ID，可以啟用調度（將設定為）。

有關使用此端點的詳細資訊，請參閱計畫端 [點指南](../api/schedules.md#update-state)

### 更新計畫時間

通過向端點發出PATCH請求並在路徑中包 `/config/schedules` 含調度的ID，可以更新調度時間。

有關使用此端點的詳細資訊，請參閱計畫端 [點指南](../api/schedules.md#update-schedule)

## 隨選評估

隨選評估可讓您建立區段工作，以便在需要時產生對象區段。 與排程評估不同，這只會在要求時發生，且不會重複發生。

### 建立區段工作

區段工作是建立新讀者區段的非同步程式。 它參考區段定義，以及控制如何合併描述檔片段之 [!DNL Real-time Customer Profile] 間重疊屬性的任何合併原則。 當區段工作成功完成時，您可以收集區段的各種資訊，例如處理期間可能發生的任何錯誤，以及您的受眾的最終規模。

您可以向API中的端點提出POST請求，以建立 `/segment/jobs` 新的區段 [!DNL Real-time Customer Profile] 工作。

有關使用此端點的詳細資訊，請參閱段作業端 [點指南](../api/segment-jobs.md#create)


### 查找段作業狀態

您可以使用 `id` 特定區段工作來執行查閱請求(GET)，以檢視工作的目前狀態。

有關使用此端點的詳細資訊，請參閱段作業端 [點指南](../api/segment-jobs.md#get)

## 解譯區段結果

當區段工作成功執行時，會針 `segmentMembership` 對區段內的每個描述檔更新地圖。 `segmentMembership` 此外，還會儲存任何已預先評估的受眾細分，這些細分會 [!DNL Platform]納入其中，以便與其他解決方案整合 [!DNL Adobe Audience Manager]。

以下範例顯示每個個 `segmentMembership` 別描述檔記錄的屬性外觀：

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

如果您知道要存取的特定描述檔，可使用 [!DNL Real-time Customer Profile] API。 使用「描述檔API」教學課程的「存取即時客戶描述檔」資料中，提供存取個 [別描述檔的完整步驟](../../profile/api/entities.md) 。

## 匯出區段 {#export}

分段工作成功完成(屬性的值為 `status` 「成功」)後，您可將對象匯出至資料集，供您存取及操作。

匯出您的觀眾需要下列步驟：

- [建立目標資料集](#create-a-target-dataset) -建立資料集以容納對象成員。
- [在資料集中產生觀眾設定檔](#generate-profiles-for-audience-members) -根據區段工作的結果，以XDM個別設定檔填入資料集。
- [監視導出進度](#monitor-export-progress) -檢查導出進程的當前進度。
- [讀取觀眾資料](#next-steps) -擷取產生的XDM個人設定檔，代表觀眾的成員。

### 建立目標資料集

匯出對象時，必須先建立目標資料集。 請務必正確設定資料集，以確保匯出成功。

主要考量事項之一是資料集所依據的架構(在下`schemaRef.id` 面的API範例請求中)。 若要匯出區段，資料集必須以( [!DNL XDM Individual Profile Union Schema]`https://ns.adobe.com/xdm/context/profile__union`)為基礎。 聯合模式是系統生成的只讀模式，它聚合共用相同類的模式的欄位（在本例中為XDM Individual Profile類）。 有關聯合視圖方案的詳細資訊，請參閱 [方案註冊開發人員指南的「即時客戶概要檔案」部分](../../xdm/api/getting-started.md)。

建立必要資料集有兩種方式：

- **使用API:** 本教學課程中後續的步驟概述如何建立使用API參考 [!DNL XDM Individual Profile Union Schema] 的資 [!DNL Catalog] 料集。
- **使用UI:** 若要使用 [!DNL Adobe Experience Platform] 使用者介面來建立參照聯合架構的資料集，請依照 [UI教學課程中的步驟進行，然後返回本教學課程，以繼續產生觀眾設定檔](../ui/overview.md) 的步驟 [](#generate-xdm-profiles-for-audience-members)。

如果您已擁有相容的資料集並知道其ID，則可直接執行步驟，以產生觀 [眾設定檔](#generate-xdm-profiles-for-audience-members)。

**API格式**

```http
POST /dataSets
```

**請求**

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
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 資料集的描述性名稱。 |
| `schemaRef.id` | 資料集將與之關聯的聯合檢視（結構）ID。 |
| `fileDescription.persisted` | 布爾值，設定為 `true`時，可讓資料集在聯合檢視中持續存在。 |

**回應**

成功的回應會傳回包含新建立資料集之唯讀、系統產生之唯一ID的陣列。 若要成功匯出觀眾成員，需要正確設定的資料集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 為觀眾成員產生個人檔案 {#generate-profiles}

在您擁有持續結合的資料集後，您可以建立匯出工作，透過對 `/export/jobs`[!DNL Real-time Customer Profile] API中的端點提出POST要求，並針對您要匯出的區段提供資料集ID和區段資訊，將觀眾成員持續存留至資料集。

有關使用此端點的詳細資訊，請參閱導出作業端 [點指南。](../api/export-jobs.md#create)

### 監視導出進度

作為導出作業進程，您可以通過向端點發出GET請求並在路徑中包 `/export/jobs` 括導出作 `id` 業來監視其狀態。 一旦欄位傳回值&quot;SUCCEEDED&quot;, `status` 匯出工作就會完成。

有關使用此端點的詳細資訊，請參閱導出作業端 [點指南。](../api/export-jobs.md#get)

## 後續步驟

成功完成導出後，您的資料即可在中 [!DNL Data Lake] 使用 [!DNL Experience Platform]。 然後，您可以使用 [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) ，使用與導出關聯的 `batchId` 訪問資料。 視區段大小而定，資料可能以區塊為單位，而批次可能由數個檔案組成。

如需如何使用 [!DNL Data Access] API存取和下載批次檔案的逐步指示，請遵循資料存取 [教學課程](../../data-access/tutorials/dataset-data.md)。

您也可以使用存取成功匯出的區段資料 [!DNL Adobe Experience Platform Query Service]。 使用UI或RESTful API, [!DNL Query Service] 可讓您編寫、驗證及執行查詢中的資料 [!DNL Data Lake]。

有關如何查詢觀眾資料的更多資訊，請參閱 [[!DNL查詢服務]的檔案](../../query-service/home.md)。
