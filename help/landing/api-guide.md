---
keywords: Experience Platform；首頁；熱門主題；Adobe Experience Platform;api指南；平台api指南；平台簡介；開發人員指南
solution: Experience Platform
title: 開始使用Adobe Experience PlatformAPI
topic: api guide
description: Adobe Experience Platform提供彼此緊密連結的API服務。 本指南包含可用服務、CRUD作業所需標題、錯誤訊息、Postman系列和範例API呼叫的相關資訊。
translation-type: tm+mt
source-git-commit: 85d2ae5ccf1b27baaafe839f1d3f00d588abe4fc
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 0%

---


# 開始使用Adobe Experience PlatformAPI

Adobe Experience Platform的發展理念是「API優先」。 使用Platform API，您可以程式設計方式對資料執行基本的CRUD（建立、讀取、更新、刪除）作業，例如設定計算屬性、存取資料／實體、匯出資料、刪除不需要的資料或批次等。

每個Experience Platform服務的API都共用相同的驗證標題集，並對其CRUD作業使用類似的語法。 以下指南概述開始使用Platform API的必要步驟。

## 驗證和標題

為成功呼叫平台端點，您必須完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程可提供Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

### 沙盒標題

Experience Platform中的所有資源都隔離到特定的虛擬沙盒。 對平台API的請求需要一個標題，該標題指定要在中執行操作的沙盒名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

如需平台中沙盒的詳細資訊，請參閱[沙盒概述檔案](../sandboxes/home.md)。

### 內容類型標題

所有在請求正文中包含裝載的請求(例如POST、PUT和PATCH呼叫)都必須包含`Content-Type`標題。 接受的值是每個API端點專屬的值。 如果端點需要特定的`Content-Type`值，則其值將顯示在[API指南針對個別平台服務](#api-guides)提供的範例API請求中。

## Experience PlatformAPI基礎

Adobe Experience PlatformAPI採用數種重要的基礎技術和語法，以有效管理平台資源。

若要進一步瞭解平台所運用的基礎API技術，包括範例JSON結構描述物件，請造訪[Experience PlatformAPI基礎](api-fundamentals.md)指南。

## Experience PlatformAPI的郵遞員集合

Postman是API開發的協作平台，可讓您使用預設變數來設定環境、共用API集合、簡化CRUD要求等。 大部分的平台API服務都有郵遞員系列，可用來協助進行API呼叫。

若要進一步瞭解Postman，包括如何設定環境、可用系列清單以及如何匯入系列，請造訪[平台Postman檔案](postman.md)。

## 讀取範例API呼叫{#sample-api}

請求格式會依使用的平台API而異。 瞭解如何建構API呼叫的最佳方式，是依循您所使用之特定平台服務檔案中提供的範例。

[!DNL Experience Platform]的檔案以兩種不同的方式顯示範例API呼叫。 首先，調用以&#x200B;**API格式**&#x200B;顯示，模板表示僅顯示操作(GET、POST、PUT、PATCH、DELETE)和所使用的端點（例如`/global/classes`）。 有些範本也會顯示變數的位置，以協助說明呼叫應如何制定，例如`GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`。

然後，呼叫在&#x200B;**Request**&#x200B;中顯示為cURL命令，其中包含成功與API互動所需的必要標題和完整「基本路徑」。 基本路徑應預先附加到所有端點。 例如，前述的`/global/classes`端點變為`https://platform.adobe.io/data/foundation/schemaregistry/global/classes`。 您會在整個檔案中看到API格式／請求模式，在對平台API進行自己的呼叫時，預期會使用範例請求中顯示的完整路徑。

### 範例API要求

以下是範例API要求，示範您在說明檔案中將會遇到的格式。

**API格式**

API格式顯示所使用的操作(GET)和端點。 變數會以大括弧表示（在本例中為`{CONTAINER_ID}`）。

```http
GET /{CONTAINER_ID}/classes
```

**請求**

在此範例請求中，API格式的變數會在請求路徑中指定實際值。 此外，所有必要的標題都會顯示為範例標題值或變數，其中應包含敏感資訊（例如安全性Token和存取ID）。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

此回應說明您在成功呼叫API後，會根據所傳送的請求收到哪些訊息。 有時候，回應會因空間而截斷，這表示您可能會看到範例中顯示的更多資訊或其他資訊。

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

[平台疑難排解指南](troubleshooting.md#errors-and-troubleshooting)提供您使用任何Experience Platform服務時可能遇到的錯誤清單。

有關各平台服務的故障排除指南，請參閱[服務故障排除目錄](troubleshooting.md#service-troubleshooting-directory)。

如需平台API中特定端點的詳細資訊，包括必要的標頭和請求主體，請參閱[平台API指南](#api-guides)。

## 平台API指南{#api-guides}

| API指南 | 說明 |
| --- | --- |
| [[!DNL Access Control] API指南](.././access-control/api/getting-started.md) | [!DNL Access Control] API端點可以檢索指定沙盒內特定資源上對用戶有效的當前策略。 所有其它訪問控制功能都通過[Adobe Admin Console](https://adminconsole.adobe.com/)提供。 |
| [批次擷取API指南](.././ingestion/batch-ingestion/api-overview.md) | Adobe Experience Platform[!DNL Data Ingestion] API可讓您將資料以批次檔案的形式內嵌至平台。 所吸收的資料可以是CRM系統中平面檔案（例如Parce檔案）的描述檔資料，或符合架構註冊表(XDM)中已知架構的資料。 |
| [[!DNL Catalog Service] API指南](.././catalog/api/getting-started.md) | [!DNL Catalog Service] API可讓開發人員管理Adobe Experience Platform的資料集中繼資料。 這包括資料位置、處理階段、處理期間發生的錯誤，以及資料報表。 |
| [[!DNL Data Access] API指南](.././data-access/api.md) | [!DNL Data Access] API可讓開發人員擷取Experience Platform中已收錄資料集的相關資訊。 這包括存取和下載資料集檔案、擷取標題資訊、列出失敗和成功的批次，以及下載預覽CSV / Parce檔案。 |
| [[!DNL Dataset Service] API指南](.././data-governance/labels/dataset-api.md) | 資料集服務API可讓您套用和編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集元資料的目錄服務API不同。 |
| [[!DNL Flow Service] API指南](.././sources/tutorials/api/create-dataset-base-connection.md) <br> （來源與目標） | [!DNL Flow Service] API用於收集和集中來自各種不同來源的資料，並用於建立和啟用資料至Adobe Experience Platform境內的不同目的地。 該服務提供REST風格的API，從中可連接所有受支援的源。 |
| [[!DNL Identity Service] API指南](.././identity-service/api/getting-started.md) | [!DNL Identity Service] API可讓開發人員使用Adobe Experience Platform的身分圖表，管理客戶的跨裝置、跨通道和近乎即時的身分識別。 |
| [[!DNL Observability Insights] API指南](.././observability/api/overview.md) | [!DNL Observability Insights] 是REST風格的API，可讓開發人員在Adobe Experience Platform公開關鍵的可觀測性度量。這些量度可提供平台使用統計資料、平台服務狀況檢查、歷史趨勢以及各種平台功能效能指標的深入資訊。 |
| [[!DNL Policy Service] API指南](.././data-governance/api/overview.md) <br> （資料管理） | [!DNL Policy Service] API可讓您建立和管理資料使用標籤和原則，以決定可針對包含特定資料使用標籤的資料採取哪些行銷動作。 若要將標籤套用至資料集和欄位，請參閱[[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md)指南 |
| [[!DNL Privacy Service] API指南](.././privacy-service/api/getting-started.md) | [!DNL Privacy Service] API可讓開發人員建立並管理客戶要求，以便跨Experience Cloud應用程式存取或刪除其個人資料，以符合法律隱私權規範。 |
| [[!DNL Query Service] API指南](.././query-service/api/getting-started.md) | [!DNL Query Service] API可讓開發人員使用標準SQL查詢其Adobe Experience Platform資料。 |
| [[!DNL Real-time Customer Profile] API指南](.././profile/api/overview.md) | 即時客戶描述檔API可讓開發人員探索和使用描述檔資料，包括檢視描述檔、建立和更新合併原則、匯出或取樣描述檔資料，以及刪除不再需要或錯誤新增的描述檔資料。 |
| [沙盒API指南](.././sandboxes/api/getting-started.md) | 沙盒API可讓開發人員以程式設計方式管理Adobe Experience Platform的獨立虛擬沙盒環境。 |
| [[!DNL Schema Registry] API指南](.././xdm/api/overview.md) <br> (XDM) | [!DNL Schema Registry] API可讓開發人員以程式設計方式管理Adobe Experience Platform內的所有架構和相關的Experience Data Model(XDM)資源。 |
| [[!DNL Segmentation Service] API指南](.././segmentation/api/overview.md) | [!DNL Segmentation Service] API可讓開發人員以程式設計方式管理Adobe Experience Platform的分段作業。 這包括建立區段並從您的即時客戶個人檔案資料產生受眾。 |
| [[!DNL Sensei Machine Learning] API指南](.././data-science-workspace/api/getting-started.md) <br> （資料科學工作區） | [!DNL Sensei Machine Learning] API為資料科學家提供機制，以組織和管理從演算法上線、實驗到服務部署的機器學習(ML)服務。 |

有關每項服務可用的特定端點和操作的詳細資訊，請參閱[API參考文檔](http://www.adobe.com/go/platform-api-reference-en)中的Adobe I/O。

## 後續步驟

本檔案介紹了必要的標題、可用的指南，並提供了範例API呼叫。 既然您已具備在Adobe Experience Platform進行API呼叫所需的標頭值，請從[平台API指南表](#api-guides)中選取您想要探索的API端點。

有關常見問題的解答，請參閱[平台疑難排解指南](troubleshooting.md)。

要設定郵遞員環境並探索可用的郵遞員系列，請參閱[平台郵遞員指南](postman.md)。

