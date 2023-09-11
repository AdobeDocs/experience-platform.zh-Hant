---
keywords: Experience Platform；首頁；熱門主題；Adobe Experience Platform；api指南；平台api指南；平台簡介；開發人員指南
solution: Experience Platform
title: Adobe Experience Platform API快速入門
description: Adobe Experience Platform提供的API服務彼此緊密連結。 本指南包含可用服務、CRUD作業所需標頭、錯誤訊息、Postman集合和範例API呼叫的相關資訊。
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: c728d63c22593ca56999dd0bb6679dea7de0e00a
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 0%

---

# Adobe Experience Platform API快速入門

Adobe Experience Platform是根據「API優先」的理念所開發。 使用Platform API，您可以利用程式設計方式針對資料執行基本CRUD （建立、讀取、更新、刪除）操作，例如設定計算屬性、存取資料/實體、匯出資料、刪除不需要的資料或批次等。

每個Experience Platform服務的API都共用相同的驗證標題集，並對其CRUD操作使用類似的語法。 下列指南概述開始使用Platform API的必要步驟。

## 驗證和標頭

為了成功呼叫Platform端點，您必須完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程，提供Experience Platform API呼叫中每個必要標題的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### 沙箱標頭

Experience Platform中的所有資源都會隔離至特定的虛擬沙箱。 對Platform API的請求需要標頭，該標頭會指定將在其中執行操作的沙箱名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

如需Platform沙箱的詳細資訊，請參閱 [沙箱概述檔案](../sandboxes/home.md).

### Content-type標頭

所有要求內文中具有裝載(例如POST、PUT和PATCH呼叫)都必須包含 `Content-Type` 標頭。 接受的值是每個API端點專屬的值。 若為特定 `Content-Type` 端點需要值，其值將顯示在提供的範例API請求中。 [適用於個別平台服務的API指南](#api-guides).

## Experience PlatformAPI基礎知識

Adobe Experience Platform API運用多種基礎技術和語法，這些技術和語法對於有效管理Platform資源非常重要。

若要進一步瞭解平台運用的基礎API技術，包括範例JSON結構描述物件，請造訪 [Experience PlatformAPI基礎知識](api-fundamentals.md) 指南。

## Experience Platform API的Postman集合

Postman是API開發的共同作業平台，可讓您使用預設變數設定環境、共用API集合、簡化CRUD請求等。 大部分的Platform API服務都有Postman集合，可用來協助進行API呼叫。

若要深入瞭解Postman，包括如何設定環境、可用集合清單以及如何匯入集合，請造訪 [Platform Postman檔案](postman.md).

## 讀取範例API呼叫 {#sample-api}

請求格式會因使用的平台API而異。 要瞭解如何架構API呼叫，最好的方式是遵循檔案中針對您使用的特定平台服務提供的範例。

的檔案 [!DNL Experience Platform] 以兩種不同的方式顯示API呼叫範例。 首先，呼叫會顯示在其 **API格式**，此範本表示法僅會顯示使用的操作(GET、POST、PUT、PATCH、DELETE)和端點(例如 `/global/classes`)。 有些範本也會顯示變數的位置，以說明呼叫的建構方式，例如 `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

然後，這些呼叫會顯示為cURL命令，在 **請求**，包括成功與API互動所需的必要標題和完整「基本路徑」。 基礎路徑應預先附加到所有端點。 例如，上述的 `/global/classes` 端點變成 `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. 您將在整份檔案中看到API格式/請求模式，並預期當您對Platform API發出自己的呼叫時，會使用範例請求中顯示的完整路徑。

### 範例API請求

以下範例API請求會示範您將在檔案中遇到的格式。

**API格式**

API格式會顯示使用的操作(GET)和端點。 變數會以大括弧表示(在此情況下， `{CONTAINER_ID}`)。

```http
GET /{CONTAINER_ID}/classes
```

**要求**

在此範例請求中，API格式的變數在請求路徑中被指定實際值。 此外，所有必要的標頭都會顯示為範例標頭值或變數，其中應包含敏感資訊（例如安全性權杖和存取ID）。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應會根據傳送的請求，說明在成功呼叫API後您會收到的內容。 有時候，回應會截斷空格，表示您可能會看到範例中顯示的詳細資訊或其他資訊。

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

## 錯誤訊息

此 [平台疑難排解指南](troubleshooting.md#errors-and-troubleshooting) 提供您使用任何Experience Platform服務時可能遇到的錯誤清單。

如需個別平台服務的疑難排解指南，請參閱 [服務疑難排解目錄](troubleshooting.md#service-troubleshooting-directory).

如需Platform API中特定端點的詳細資訊，包括必要的標題和請求內文，請參閱 [平台API指南](#api-guides).

## 平台API指南 {#api-guides}

| API指南 | 說明 |
| --- | --- |
| [[!DNL Access Control] API指南](.././access-control/api/getting-started.md) | 此 [!DNL Access Control] API端點可以擷取使用者在指定沙箱內的指定資源上生效的目前原則。 所有其他存取控制功能是透過 [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [批次擷取API指南](.././ingestion/batch-ingestion/api-overview.md) | Adobe Experience Platform [!DNL Data Ingestion] API可讓您將資料以批次檔案的形式擷取到Platform。 所擷取的資料可以是CRM系統中平面檔案（例如Parquet檔案）的設定檔資料，或是符合Schema Registry (XDM)中已知結構的資料。 |
| [[!DNL Catalog Service] API指南](.././catalog/api/getting-started.md) | 此 [!DNL Catalog Service] API可讓開發人員管理Adobe Experience Platform中的資料集中繼資料。 這包括資料位置、處理階段、處理期間發生的錯誤以及資料報表。 |
| [[!DNL Data Access] API指南](.././data-access/api.md) | 此 [!DNL Data Access] API可讓開發人員擷取Experience Platform內擷取資料集的資訊。 這包括存取和下載資料集檔案、擷取標題資訊、列出失敗和成功的批次，以及下載預覽CSV / Parquet檔案。 |
| [[!DNL Dataset Service] API指南](.././data-governance/labels/dataset-api.md) | 資料集服務API可讓您套用及編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集中繼資料的目錄服務API不同。 |
| [[!DNL Edge Network Server] API指南](../server-api/overview.md) | 此 [!DNL Edge Network Server API] 可用於各種資料收集、個人化、廣告和行銷使用案例。 此 [!DNL Server API] 可用於伺服器， [!DNL IoT] 裝置、機上盒和其他各種裝置。 |
| [[!DNL Identity Service] API指南](.././identity-service/api/getting-started.md) | 此 [!DNL Identity Service] API可讓開發人員在Adobe Experience Platform中使用身分圖表，管理跨裝置、跨頻道及幾乎即時的客戶身分識別。 |
| [[!DNL Observability Insights] API指南](.././observability/api/overview.md) | [!DNL Observability Insights] 是RESTful API，可讓開發人員在Adobe Experience Platform中公開關鍵可觀察性量度。 這些量度提供平台使用統計資料、Platform服務健康情況檢查、歷史趨勢和各種Platform功能績效指標的深入分析。 |
| [[!DNL Policy Service] API指南](.././data-governance/api/overview.md) <br> （資料控管） | 此 [!DNL Policy Service] API可讓您建立和管理資料使用標籤和原則，以決定可以對包含特定資料使用標籤的資料採取哪些行銷動作。 若要將標籤套用至資料集和欄位，請參閱 [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) 指南 |
| [[!DNL Privacy Service] API指南](.././privacy-service/api/getting-started.md) | 此 [!DNL Privacy Service] API可讓開發人員根據隱私權法規，建立和管理客戶請求，以便在Experience Cloud應用程式中存取或刪除其個人資料。 |
| [[!DNL Query Service] API指南](.././query-service/api/getting-started.md) | 此 [!DNL Query Service] API可讓開發人員使用標準SQL查詢其Adobe Experience Platform資料。 |
| [[!DNL Real-Time Customer Profile] API指南](.././profile/api/overview.md) | 即時客戶設定檔API可讓開發人員探索和使用設定檔資料，包括檢視設定檔、建立和更新合併原則、匯出或取樣設定檔資料，以及刪除不再需要或錯誤新增的設定檔資料。 |
| [Sandbox API指南](.././sandboxes/api/getting-started.md) | 沙箱API可讓開發人員以程式設計方式管理Adobe Experience Platform中的隔離虛擬沙箱環境。 |
| [[!DNL Schema Registry] API指南](.././xdm/api/overview.md) <br> (XDM) | 此 [!DNL Schema Registry] API可讓開發人員以程式設計方式管理Adobe Experience Platform中的所有結構描述和相關的Experience Data Model (XDM)資源。 |
| [[!DNL Segmentation Service] API指南](.././segmentation/api/overview.md) | 此 [!DNL Segmentation Service] API可讓開發人員以程式設計方式管理Adobe Experience Platform中的細分作業。 這包括建立區段，以及從您的即時客戶設定檔資料產生對象。 |
| [[!DNL Sensei Machine Learning] API指南](.././data-science-workspace/api/getting-started.md) <br> （資料科學工作區） | 此 [!DNL Sensei Machine Learning] API為資料科學家提供了一種機制，可組織和管理機器學習(ML)服務，從演演算法上線、實驗到服務部署。 |

如需每個服務可用的特定端點和作業的詳細資訊，請參閱 [API參考檔案](https://www.adobe.com/go/platform-api-reference-en) 在Adobe I/O上。

## 後續步驟

本檔案介紹了必要的標頭、可用的指南，並提供API呼叫的範例。 您現在擁有在Adobe Experience Platform上進行API呼叫所需的標頭值，請從以下位置選取您要探索的API端點： [平台API指南表格](#api-guides).

若需常見問題的解答，請參閱 [平台疑難排解指南](troubleshooting.md).

若要設定Postman環境並探索可用的Postman集合，請參閱 [Platform Postman指南](postman.md).
