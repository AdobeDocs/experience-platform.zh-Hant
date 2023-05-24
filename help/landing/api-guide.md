---
keywords: Experience Platform；首頁；熱門主題；Adobe Experience Platform;api指南；平台API指南；平台簡介；開發人員指南
solution: Experience Platform
title: Adobe Experience PlatformAPI入門
description: Adobe Experience Platform提供彼此緊密相連的API服務。 本指南包含有關可用服務、CRUD操作所需標頭、錯誤消息、Postman集合和示例API調用的資訊。
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# Adobe Experience PlatformAPI入門

Adobe Experience Platform是在&quot;API優先&quot;理念下發展的。 使用平台API，可以以寫程式方式對資料執行基本CRUD（建立、讀取、更新、刪除）操作，如配置計算屬性、訪問資料/實體、導出資料、刪除不需要的資料或批處理等。

每個Experience Platform服務的API都共用同一組身份驗證標頭，並對其CRUD操作使用相似的語法。 下面的指南概述了使用平台API入門的必要步驟。

## 驗證和頭

為了成功調用平台端點，需要完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成Experience Platform教程將提供API調用中每個必需標頭的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### 沙盒頭

Experience Platform中的所有資源都與特定的虛擬沙箱隔離。 對平台API的請求需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

有關平台中沙箱的詳細資訊，請參閱 [沙盒概述文檔](../sandboxes/home.md)。

### 內容類型標題

請求主體中具有負載的所有請求(如POST、PUT和PATCH呼叫)必須包括 `Content-Type` 標題。 接受的值特定於每個API終結點。 如果 `Content-Type` 端點需要值，其值將顯示在由提供的示例API請求中 [針對單個平台服務的API指南](#api-guides)。

## Experience PlatformAPI基礎

Adobe Experience Platform的API採用了若干基礎技術和語法，這些技術和語法對於有效管理平台資源非常重要。

要瞭解有關平台使用的基礎API技術（包括示例JSON架構對象）的詳細資訊，請訪問 [Experience PlatformAPI基礎](api-fundamentals.md) 的子菜單。

## PostmanExperience PlatformAPI集合

Postman是API開發的協作平台，允許您設定具有預設變數的環境、共用API集合、簡化CRUD請求等。 大多數平台API服務都有Postman集合，這些集合可用於幫助進行API調用。

要瞭解有關Postman的更多資訊，請訪問 [平台Postman文檔](postman.md)。

## 讀取示例API調用 {#sample-api}

請求格式因所使用的平台API而異。 學習如何構造API調用的最佳方法是，隨附您正在使用的特定平台服務文檔中提供的示例。

文檔 [!DNL Experience Platform] 以兩種不同的方式顯示示例API調用。 首先，在 **API格式**，只顯示操作(GET、POST、PUT、PATCH、DELETE)和所使用的端點的模板表示法(例如， `/global/classes`)。 某些模板還顯示了變數的位置，以幫助說明應如何構建調用，如 `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`。

然後，調用將在 **請求**，其中包括成功與API交互所需的必需標頭和完整的「基本路徑」。 基本路徑應預先置於所有端點。 例如， `/global/classes` 端點 `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`。 在整個文檔中，您將看到API格式/請求模式，並且在對平台API進行自己的調用時，應使用示例請求中顯示的完整路徑。

### 示例API請求

下面是一個示例API請求，它演示了在文檔中將遇到的格式。

**API格式**

API格式顯示操作(GET)和正在使用的終結點。 變數由大括弧表示(在本例中， `{CONTAINER_ID}`)。

```http
GET /{CONTAINER_ID}/classes
```

**要求**

在此示例請求中，API格式中的變數在請求路徑中給定實際值。 此外，所有必需的標頭都顯示為應包含敏感資訊（如安全令牌和訪問ID）的示例標頭值或變數。

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

該響應說明了在根據發送的請求成功調用API後您預期會收到的內容。 有時候，響應會被截斷為空格，這意味著您可能會看到示例中顯示的更多資訊或附加資訊。

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

的 [平台故障排除指南](troubleshooting.md#errors-and-troubleshooting) 提供了使用任何Experience Platform服務時可能遇到的錯誤的清單。

有關單個平台服務的故障排除指南，請參見 [服務疑難解答目錄](troubleshooting.md#service-troubleshooting-directory)。

有關平台API中特定終結點（包括所需標頭和請求主體）的詳細資訊，請參閱 [平台API指南](#api-guides)。

## 平台API指南 {#api-guides}

| API指南 | 說明 |
| --- | --- |
| [[!DNL Access Control] API指南](.././access-control/api/getting-started.md) | 的 [!DNL Access Control] API終結點可以檢索指定沙箱內給定資源上對用戶有效的當前策略。 通過 [Adobe Admin Console](https://adminconsole.adobe.com/)。 |
| [批量接收API指南](.././ingestion/batch-ingestion/api-overview.md) | Adobe Experience Platform [!DNL Data Ingestion] API允許您將資料作為批處理檔案插入平台。 正在攝取的資料可以是來自CRM系統中的平面檔案（如Parke檔案）的配置檔案資料，也可以是符合架構註冊(XDM)中已知架構的資料。 |
| [[!DNL Catalog Service] API指南](.././catalog/api/getting-started.md) | 的 [!DNL Catalog Service] API允許開發人員管理Adobe Experience Platform的資料集元資料。 這包括資料位置、處理階段、處理過程中發生的錯誤和資料報告。 |
| [[!DNL Data Access] API指南](.././data-access/api.md) | 的 [!DNL Data Access] API允許開發人員檢索Experience Platform內所接收資料集的資訊。 這包括訪問和下載資料集檔案、檢索頭資訊、列出失敗和成功的批處理，以及下載預覽CSV / Parce檔案。 |
| [[!DNL Dataset Service] API指南](.././data-governance/labels/dataset-api.md) | 資料集服務API允許您應用和編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集元資料的目錄服務API是分開的。 |
| [[!DNL Identity Service] API指南](.././identity-service/api/getting-started.md) | 的 [!DNL Identity Service] API允許開發人員使用Adobe Experience Platform的標識圖管理跨設備、跨通道和接近即時的客戶標識。 |
| [[!DNL Observability Insights] API指南](.././observability/api/overview.md) | [!DNL Observability Insights] 是REST風格的API，它允許開發人員在Adobe Experience Platform公開關鍵的可觀性度量。 這些指標提供了平台使用情況統計資訊、平台服務運行狀況檢查、歷史趨勢以及各種平台功能的效能指標。 |
| [[!DNL Policy Service] API指南](.././data-governance/api/overview.md) <br> （資料治理） | 的 [!DNL Policy Service] API允許您建立和管理資料使用標籤和策略，以確定可以針對包含某些資料使用標籤的資料採取哪些市場營銷操作。 要將標籤應用於資料集和欄位，請參閱 [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) 引導 |
| [[!DNL Privacy Service] API指南](.././privacy-service/api/getting-started.md) | 的 [!DNL Privacy Service] API允許開發人員建立和管理客戶請求，以便跨Experience Cloud應用程式訪問或刪除其個人資料，這符合法律隱私法規。 |
| [[!DNL Query Service] API指南](.././query-service/api/getting-started.md) | 的 [!DNL Query Service] API允許開發人員使用標準SQL查詢其Adobe Experience Platform資料。 |
| [[!DNL Real-Time Customer Profile] API指南](.././profile/api/overview.md) | 即時客戶配置檔案API允許開發人員瀏覽和使用配置檔案資料，包括查看配置檔案、建立和更新合併策略、導出或採樣配置檔案資料以及刪除不再需要或錯誤添加的配置檔案資料。 |
| [沙盒API指南](.././sandboxes/api/getting-started.md) | 沙盒API允許開發人員以寫程式方式管理Adobe Experience Platform的隔離虛擬沙盒環境。 |
| [[!DNL Schema Registry] API指南](.././xdm/api/overview.md) <br> (XDM) | 的 [!DNL Schema Registry] API允許開發人員以寫程式方式管理Adobe Experience Platform內的所有架構和相關的體驗資料模型(XDM)資源。 |
| [[!DNL Segmentation Service] API指南](.././segmentation/api/overview.md) | 的 [!DNL Segmentation Service] API允許開發人員以寫程式方式管理Adobe Experience Platform的分段操作。 這包括構建細分市場和從即時客戶概要資訊資料生成受眾。 |
| [[!DNL Sensei Machine Learning] API指南](.././data-science-workspace/api/getting-started.md) <br> （資料科學工作區） | 的 [!DNL Sensei Machine Learning] API為資料科學家提供了一種機制，用於組織和管理從算法上、實驗和服務部署到機器學習(ML)服務。 |

有關每個服務的特定終結點和操作的詳細資訊，請參閱 [API參考文檔](https://www.adobe.com/go/platform-api-reference-en) Adobe I/O。

## 後續步驟

本文檔介紹了所需的標題、可用指南，並提供了一個示例API調用。 現在，您具有在Adobe Experience Platform上進行API調用所需的標頭值，請從中選擇要瀏覽的API終結點 [平台API指南表](#api-guides)。

有關常見問題的回答，請參閱 [平台故障排除指南](troubleshooting.md)。

要設定Postman環境並探索可用的Postman收藏，請參閱 [Postman站台指南](postman.md)。
